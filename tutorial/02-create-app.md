<!-- markdownlint-disable MD002 MD041 -->

Para empezar, cree un nuevo proyecto nativo de reAct.

1. Abra la interfaz de la línea de comandos (CLI) en un directorio donde desee crear el proyecto. Ejecute el siguiente comando para ejecutar la herramienta [reAct-Native-CLI](https://github.com/facebook/react-native) y cree un nuevo proyecto nativo reAct.

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. **Opcional:** Ejecute el proyecto para comprobar que el entorno de desarrollo está configurado correctamente. En la CLI, cambie el directorio al directorio **GraphTutorial** que acaba de crear y ejecute uno de los siguientes comandos.

    - Para iOS:`npx react-native run-ios`
    - Para Android: iniciar una instancia del emulador de Android y ejecutar`npx react-native run-android`

## <a name="install-dependencies"></a>Instalar dependencias

Antes de continuar, instale algunas dependencias adicionales que usará más adelante.

- [reAct-navegación](https://reactnavigation.org) para controlar la navegación entre vistas en la aplicación.
- [reAct-Native-gesto-controlador](https://github.com/kmagiera/react-native-gesture-handler), [reAct-nativo-área-seguridad-área-contexto](https://github.com/th3rdwave/react-native-safe-area-context), [reAct-pantallas nativas](https://github.com/kmagiera/react-native-screens), [reAct-nativo-reanimate](https://github.com/kmagiera/react-native-reanimated)y [vista enmascarada](https://github.com/react-native-community/react-native-masked-view) requerida por reAct-Navigation.
- [reAct-Native-Elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) y [reAct-Native-vector-Icons](https://github.com/oblador/react-native-vector-icons) para proporcionar iconos para la interfaz de usuario.
- [reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) para controlar la autenticación y la administración de tokens.
- [almacenamiento asincrónico](https://github.com/react-native-community/react-native-async-storage) para proporcionar almacenamiento para los tokens.
- [momento](https://momentjs.com) para controlar el análisis y la comparación de fechas y horas.
- [Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.

1. Abra la CLI en el directorio raíz del proyecto nativo reAct.
1. Ejecute el comando siguiente.

    ```Shell
    npm install @react-navigation/native@5.1.5 @react-navigation/drawer@5.4.1 @react-navigation/stack@5.2.10
    npm install @react-native-community/masked-view@0.1.7 react-native-safe-area-context@0.7.3
    npm install react-native-reanimated@1.8.0 react-native-screens@2.4.0 @react-native-community/async-storage@1.9.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 react-native-gesture-handler@1.6.1
    npm install react-native-app-auth@5.1.1 moment@2.24.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>Vincular y configurar dependencias para iOS

> [!NOTE]
> Si no tiene como objetivo iOS, puede omitir esta sección.

1. Abra la CLI en el directorio **GraphTutorial/iOS** .
1. Ejecute el comando siguiente.

    ```Shell
    pod install
    ```

1. Abra el archivo **GraphTutorial/iOS/GraphTutorial/info. plist** en un editor de texto. Agregue la siguiente línea justo antes de `</dict>` la última línea del archivo.

    ```xml
    <key>UIAppFonts</key>
    <array>
      <string>AntDesign.ttf</string>
      <string>Entypo.ttf</string>
      <string>EvilIcons.ttf</string>
      <string>Feather.ttf</string>
      <string>FontAwesome.ttf</string>
      <string>FontAwesome5_Brands.ttf</string>
      <string>FontAwesome5_Regular.ttf</string>
      <string>FontAwesome5_Solid.ttf</string>
      <string>Foundation.ttf</string>
      <string>Ionicons.ttf</string>
      <string>MaterialIcons.ttf</string>
      <string>MaterialCommunityIcons.ttf</string>
      <string>SimpleLineIcons.ttf</string>
      <string>Octicons.ttf</string>
      <string>Zocial.ttf</string>
    </array>
    ```

1. Abra el archivo **GraphTutorial/iOS/GraphTutorial/AppDelegate. h** en un editor de texto. Reemplace su contenido por lo siguiente.

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a>Configurar dependencias para Android

> [!NOTE]
> Si no tiene como objetivo Android, puede omitir esta sección.

1. Abra el archivo **GraphTutorial/Android/App/Build. Gradle** en un editor.
1. Busque la `defaultConfig` entrada y agregue la siguiente propiedad en `defaultConfig`.

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    La `defaultConfig` entrada debe ser similar a la siguiente.

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. Agregue la siguiente línea al final del archivo.

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. Guarde el archivo.

## <a name="design-the-app"></a>Diseñar la aplicación

La aplicación usará un [cajón de navegación](https://reactnavigation.org/docs/drawer-based-navigation.html) para navegar entre distintas vistas. En este paso, creará las vistas básicas que usa la aplicación e implementará el cajón de navegación.

### <a name="create-views"></a>Crear vistas

En esta sección, creará las vistas de la aplicación para admitir un [flujo de autenticación](https://reactnavigation.org/docs/auth-flow).

1. Abra **GraphTutorial/index. js** y agregue lo siguiente a la parte superior del archivo, antes de cualquier `import` otra instrucción.

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **pantallas**.
1. Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **HomeScreen. TSX**. Agregue el siguiente código al archivo.

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

    const Stack = createStackNavigator();
    const UserState = React.createContext({userLoading: true, userName: ''});

    type HomeScreenState = {
      userLoading: boolean;
      userName: string;
    }

    const HomeComponent = () => {
      const userState = React.useContext(UserState);

      return (
        <View style={styles.container}>
          <ActivityIndicator animating={userState.userLoading} size='large' />
          {userState.userLoading ? null: <Text>Hello {userState.userName}!</Text>}
        </View>
      );
    }

    export default class HomeScreen extends React.Component {

      state: HomeScreenState = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <UserState.Provider value={this.state}>
              <Stack.Navigator screenOptions={headerOptions}>
                <Stack.Screen name='Home'
                  component={HomeComponent}
                  options={{
                    title: 'Welcome',
                    headerLeft: () => <DrawerToggle/>
                  }} />
              </Stack.Navigator>
          </UserState.Provider>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **CalendarScreen. TSX**. Agregue el siguiente código al archivo.

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

    const Stack = createStackNavigator();

    // Temporary placeholder view
    const CalendarComponent = () => (
      <View style={styles.container}>
        <Text>Calendar</Text>
      </View>
    );

    export default class CalendarScreen extends React.Component {

      render() {
        return (
          <Stack.Navigator screenOptions={ headerOptions }>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                title: 'Calendar',
                headerLeft: () => <DrawerToggle/>
              }} />
          </Stack.Navigator>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **SignInScreen. TSX**. Agregue el siguiente código al archivo.

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import React from 'react';
    import {
      Alert,
      Button,
      StyleSheet,
      View,
    } from 'react-native';
    import { NavigationContext } from '@react-navigation/native';

    export default class SignInScreen extends React.Component {
      static contextType = NavigationContext;

      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        const navigation = this.context;

        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [ { name: 'Main' } ]
        });
      };

      render() {
        const navigation = this.context;
        navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });

        return (
          <View style={styles.container}>
            <Button title='Sign In' onPress={this._signInAsync}/>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **AuthLoadingScreen. TSX**. Agregue el siguiente código al archivo.

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a>Crear un cajón de navegación

En esta sección, creará un menú para la aplicación y actualizará la aplicación para que use reAct-Navigation para moverse entre las pantallas.

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **menús**.
1. Cree un archivo nuevo en el directorio **GraphTutorial o menus** denominado **HeaderComponents. TSX**. Agregue el siguiente código al archivo.

    :::code language="typescript" source="../demo/GraphTutorial/menus/HeaderComponents.tsx" id="HeaderComponentSnippet":::

1. Cree un archivo nuevo en el directorio **GraphTutorial o menus** denominado **DrawerMenu. TSX**. Agregue el siguiente código al archivo.

    ```typescript
    import React, { FC } from 'react';
    import {
      Alert,
      Image,
      StyleSheet,
      Text,
      View,
      ImageSourcePropType
    } from 'react-native';
    import {
      createDrawerNavigator,
      DrawerContentScrollView,
      DrawerItem,
      DrawerItemList,
      DrawerContentComponentProps
    } from '@react-navigation/drawer';
    import { NavigationContext } from '@react-navigation/native';

    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuState = {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
    }

    const CustomDrawerContent: FC<CustomDrawerContentProps> = props => (
      <DrawerContentScrollView {...props}>
          <View style={styles.profileView}>
            <Image source={props.userPhoto}
              resizeMode='contain'
              style={styles.profilePhoto} />
            <Text style={styles.profileUserName}>{props.userName}</Text>
            <Text style={styles.profileEmail}>{props.userEmail}</Text>
          </View>
          <DrawerItemList {...props} />
          <DrawerItem label='Sign Out' onPress={props.signOut}/>
      </DrawerContentScrollView>
    );

    export default class DrawerMenuContent extends React.Component {
      static contextType = NavigationContext;

      state: DrawerMenuState = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        const navigation = this.context;
        // Sign out
        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [{ name: 'SignIn' }]
        });
      }

      render() {
        const navigation = this.context;
        navigation.setOptions({
          headerShown: false,
        });

        return (
          <Drawer.Navigator
            drawerType='front'
            drawerContent={props => (
              <CustomDrawerContent {...props}
                userName={this.state.userName}
                userEmail={this.state.userEmail}
                userPhoto={this.state.userPhoto}
                signOut={this._signOut} />
            )}>
            <Drawer.Screen name='Home'
              component={HomeScreen}
              options={{drawerLabel: 'Home'}} />
            <Drawer.Screen name='Calendar'
              component={CalendarScreen}
              options={{drawerLabel: 'Calendar'}} />
          </Drawer.Navigator>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      profileView: {
        alignItems: 'center',
        padding: 10
      },
      profilePhoto: {
        width: 80,
        height: 80,
        borderRadius: 40
      },
      profileUserName: {
        fontWeight: '700'
      },
      profileEmail: {
        fontWeight: '200',
        fontSize: 10
      }
    });
    ```

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **images**.
1. Agregue una imagen de perfil predeterminada con el nombre **no-Profile-PIC. png** en este directorio. Puede usar cualquier imagen que quiera o usar la que se [muestra en este ejemplo](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).

1. Abra el archivo **GraphTutorial/app. TSX** y reemplace todo el contenido por lo siguiente.

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AppSnippet":::

1. Guarde todos los cambios.

1. Vuelva a cargar la aplicación en el emulador.

El menú de la aplicación debe funcionar para navegar entre los dos fragmentos y cambiar cuando Puntee **en los botones iniciar sesión** o **Cerrar sesión** .

![Capturas de pantallas de la aplicación en Android](./images/android-app-screens.png)

![Capturas de pantallas de la aplicación en iOS](./images/ios-app-screens.png)
