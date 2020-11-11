<!-- markdownlint-disable MD002 MD041 -->

Para empezar, cree un nuevo proyecto nativo de reAct.

1. Abra la interfaz de la línea de comandos (CLI) en un directorio donde desee crear el proyecto. Ejecute el siguiente comando para ejecutar la herramienta [reAct-Native-CLI](https://github.com/facebook/react-native) y cree un nuevo proyecto nativo reAct.

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. **Opcional:** Ejecute el proyecto para comprobar que el entorno de desarrollo está configurado correctamente. En la CLI, cambie el directorio al directorio **GraphTutorial** que acaba de crear y ejecute uno de los siguientes comandos.

    - Para iOS: `npx react-native run-ios`
    - Para Android: iniciar una instancia del emulador de Android y ejecutar `npx react-native run-android`

## <a name="install-dependencies"></a>Instalar dependencias

Antes de continuar, instale algunas dependencias adicionales que usará más adelante.

- [reAct-navegación](https://reactnavigation.org) para controlar la navegación entre vistas en la aplicación.
- [reAct-Native-gesto-controlador](https://github.com/kmagiera/react-native-gesture-handler), [reAct-nativo-área-seguridad-área-contexto](https://github.com/th3rdwave/react-native-safe-area-context), [reAct-pantallas nativas](https://github.com/kmagiera/react-native-screens), [reAct-nativo-reanimate](https://github.com/kmagiera/react-native-reanimated)y [vista enmascarada](https://github.com/react-native-community/react-native-masked-view) requerida por reAct-Navigation.
- [reAct-Native-Elements](https://reactnativeelements.com/docs/) y [reAct-Native-vector-Icons](https://github.com/oblador/react-native-vector-icons) para proporcionar iconos para la interfaz de usuario.
- [reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) para controlar la autenticación y la administración de tokens.
- [almacenamiento asincrónico](https://react-native-async-storage.github.io/async-storage/docs/install) para proporcionar almacenamiento para los tokens.
- [DateTimePicker](https://github.com/react-native-datetimepicker/datetimepicker) para agregar selectores de fecha y hora a la interfaz de usuario.
- [momento](https://momentjs.com) para controlar el análisis y la comparación de fechas y horas.
- [Windows-IANA](https://github.com/rubenillodo/windows-iana) para traducir zonas horarias de Windows al formato IANA.
- [Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.

1. Abra la CLI en el directorio raíz del proyecto nativo reAct.
1. Ejecute el comando siguiente.

    ```Shell
    npm install @react-navigation/native@5.8.8 @react-navigation/drawer@5.11.1 @react-navigation/stack@5.12.5
    npm install @react-native-community/masked-view@0.1.10 react-native-safe-area-context@3.1.8 windows-iana
    npm install react-native-reanimated@1.13.1 react-native-screens@2.14.0 @react-native-async-storage/async-storage@1.13.2
    npm install react-native-elements@2.3.2 react-native-vector-icons@7.1.0 react-native-gesture-handler@1.8.0
    npm install react-native-app-auth@6.0.1 moment@2.29.1 moment-timezone @microsoft/microsoft-graph-client@2.1.1
    npm install @react-native-community/datetimepicker@3.0.4
    npm install @microsoft/microsoft-graph-types --save-dev
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>Vincular y configurar dependencias para iOS

> [!NOTE]
> Si no tiene como objetivo iOS, puede omitir esta sección.

1. Abra la CLI en el directorio **GraphTutorial/iOS** .
1. Ejecute el comando siguiente.

    ```Shell
    pod install
    ```

1. Abra el archivo **GraphTutorial/iOS/GraphTutorial/info. plist** en un editor de texto. Agregue la siguiente línea justo antes de la última `</dict>` línea del archivo.

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
1. Busque la `defaultConfig` entrada y agregue la siguiente propiedad en `defaultConfig` .

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

1. Abra **GraphTutorial/index.js** y agregue lo siguiente a la parte superior del archivo, antes de cualquier otra `import` instrucción.

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. Cree un archivo nuevo en el directorio **GraphTutorial** denominado **contexto. TSX** y agregue el código siguiente.

    :::code language="typescript" source="../demo/GraphTutorial/AuthContext.tsx" id="AuthContextSnippet":::

1. Cree un nuevo archivo en el directorio **GraphTutorial** denominado **UserContext. TSX** y agregue el código siguiente.

    :::code language="typescript" source="../demo/GraphTutorial/UserContext.tsx" id="UserContextSnippet":::

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **pantallas**.
1. Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **HomeScreen. TSX**. Agregue el siguiente código al archivo.

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="HomeScreenSnippet":::

1. Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **CalendarScreen. TSX**. Agregue el siguiente código al archivo.

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

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
          <Stack.Navigator>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                headerShown: false
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
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';

    type SignInProps = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default class SignInScreen extends React.Component<SignInProps> {
      static contextType = AuthContext;

      _signInAsync = async () => {
        await this.context.signIn();
      };

      componentDidMount() {
        this.props.navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });
      }

      render() {
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
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';
    import { UserContext } from '../UserContext';
    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuProps = {
      navigation: StackNavigationProp<ParamListBase>;
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

    export default class DrawerMenuContent extends React.Component<DrawerMenuProps> {
      static contextType = AuthContext;

      state = {
        // TEMPORARY
        userLoading: true,
        userFirstName: 'Adele',
        userFullName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userTimeZone: 'UTC',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        this.context.signOut();
      }

      async componentDidMount() {
        this.props.navigation.setOptions({
          headerShown: false,
        });
      }

      render() {
        const userLoaded = !this.state.userLoading;

        return (
          <UserContext.Provider value={this.state}>
            <Drawer.Navigator
              drawerType='front'
              screenOptions={{
                headerStyle: {
                  backgroundColor: '#276b80'
                },
                headerTintColor: 'white'
              }}
              drawerContent={props => (
                <CustomDrawerContent {...props}
                  userName={this.state.userFullName}
                  userEmail={this.state.userEmail}
                  userPhoto={this.state.userPhoto}
                  signOut={this._signOut} />
              )}>
              <Drawer.Screen name='Home'
                component={HomeScreen}
                options={{drawerLabel: 'Home', headerTitle: 'Welcome'}} />
              { userLoaded &&
                <Drawer.Screen name='Calendar'
                  component={CalendarScreen}
                  options={{drawerLabel: 'Calendar'}} />
              }
            </Drawer.Navigator>
          </UserContext.Provider>
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
1. Agregue una imagen de perfil predeterminada con el nombre **no-profile-pic.png** en este directorio. Puede usar cualquier imagen que quiera o usar la que se [muestra en este ejemplo](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).

1. Abra el archivo **GraphTutorial/app. TSX** y reemplace todo el contenido por lo siguiente.

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import * as React from 'react';
    import { NavigationContainer, ParamListBase } from '@react-navigation/native';
    import { createStackNavigator, StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from './AuthContext';
    import SignInScreen from './screens/SignInScreen';
    import DrawerMenuContent from './menus/DrawerMenu'
    import AuthLoadingScreen from './screens/AuthLoadingScreen';

    const Stack = createStackNavigator();

    type Props = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default function App({ navigation }: Props) {
      const [state, dispatch] = React.useReducer(
        (prevState: any, action: any) => {
          switch (action.type) {
            case 'RESTORE_TOKEN':
              return {
                ...prevState,
                userToken: action.token,
                isLoading: false
              };
            case 'SIGN_IN':
              return {
                ...prevState,
                isSignOut: false,
                userToken: action.token
              }
            case 'SIGN_OUT':
              return {
                ...prevState,
                isSignOut: true,
                userToken: null
              }
          }
        },
        {
          isLoading: true,
          isSignOut: false,
          userToken: null
        }
      );

      React.useEffect(() => {
        const bootstrapAsync = async () => {
          let userToken = null;
          // TEMPORARY
          dispatch({ type: 'RESTORE_TOKEN', token: userToken });
        };

        bootstrapAsync();
      }, []);

      const authContext = React.useMemo(
        () => ({
          signIn: async () => {
            dispatch({ type: 'SIGN_IN', token: 'placeholder-token' });
          },
          signOut: async () => {
            dispatch({ type: 'SIGN_OUT' });
          }
        }),
        []
      );

      return (
        <AuthContext.Provider value={authContext}>
          <NavigationContainer>
            <Stack.Navigator>
              {state.isLoading ? (
                <Stack.Screen name="Loading" component={AuthLoadingScreen} />
              ) : state.userToken == null ? (
                <Stack.Screen name="SignIn" component={SignInScreen} />
              ) : (
                <Stack.Screen name="Main" component={DrawerMenuContent} />
              )}
            </Stack.Navigator>
          </NavigationContainer>
        </AuthContext.Provider>
      );
    }
    ```

1. Guarde todos los cambios.

1. Vuelva a cargar la aplicación en el emulador.

El menú de la aplicación debe funcionar para navegar entre los dos fragmentos y cambiar cuando Puntee **en los botones iniciar sesión** o **Cerrar sesión** .

![Capturas de pantallas de la aplicación en Android](./images/android-app-screens.png)

![Capturas de pantallas de la aplicación en iOS](./images/ios-app-screens.png)
