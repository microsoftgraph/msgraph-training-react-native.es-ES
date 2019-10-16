<!-- markdownlint-disable MD002 MD041 -->

Para empezar, cree un nuevo proyecto nativo de reAct.

1. Abra la interfaz de la línea de comandos (CLI) en un directorio donde desee crear el proyecto. Ejecute el siguiente comando para instalar la herramienta [reAct-Native-CLI](https://github.com/facebook/react-native) y crear un nuevo proyecto nativo reAct.

    ```Shell
    npm install -g react-native-cli
    react-native init GraphTutorial
    ```

1. **Opcional:** Ejecute el proyecto para comprobar que el entorno de desarrollo está configurado correctamente. En la CLI, cambie el directorio al directorio **GraphTutorial** que acaba de crear y ejecute uno de los siguientes comandos.

    - Para iOS:`react-native run-ios`
    - Para Android: iniciar una instancia del emulador de Android y ejecutar`react-native run-android`

## <a name="install-dependencies"></a>Instalar dependencias

Antes de continuar, instale algunas dependencias adicionales que usará más adelante.

- [reAct-navegación](https://reactnavigation.org) para controlar la navegación entre vistas en la aplicación.
- [reAct-Native-gesto-controlador](https://github.com/kmagiera/react-native-gesture-handler) y [reAct-nativo-reanimate](https://github.com/kmagiera/react-native-reanimated), requerido por reAct-Navigation.
- [reAct-Native-Elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) y [reAct-Native-vector-Icons](https://github.com/oblador/react-native-vector-icons) para proporcionar iconos para la interfaz de usuario.
- [reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) para controlar la autenticación y la administración de tokens.
- [momento](https://momentjs.com) para controlar el análisis y la comparación de fechas y horas.
- [Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.

1. Abra la CLI en el directorio raíz del proyecto nativo reAct.
1. Ejecute el comando siguiente.

    ```Shell
    npm install react-navigation@3.11.1 react-native-gesture-handler@1.3.0 react-native-reanimated@1.1.0
    npm install react-native-elements@1.1.0 react-native-vector-icons@6.6.0 moment@2.24.0
    npm install react-native-app-auth@4.4.0 @microsoft/microsoft-graph-client@1.7.0
    react-native link react-native-vector-icons
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>Vincular y configurar dependencias para iOS

> [!NOTE]
> Si no tiene como objetivo iOS, puede omitir esta sección.

1. Abra la CLI en el directorio **GraphTutorial/iOS** .
1. Ejecute el comando siguiente.

    ```Shell
    pod install
    ```

1. Abra el archivo **GraphTutorial/iOS/GraphTutorial/AppDelegate. h** en un editor de texto. Reemplace su contenido por lo siguiente.

    ```obj-c
    #import <React/RCTBridgeDelegate.h>
    #import <UIKit/UIKit.h>
    #import "RNAppAuthAuthorizationFlowManager.h"

    @interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, RNAppAuthAuthorizationFlowManager>

    @property (nonatomic, strong) UIWindow *window;
    @property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate> authorizationFlowManagerDelegate;

    @end
    ```

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

1. Guarde el archivo. La `defaultConfig` entrada debe ser similar a la siguiente.

    ```Gradle
    defaultConfig {
        applicationId "com.graphtutorial"
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode 1
        versionName "1.0"
        manifestPlaceholders = [
            appAuthRedirectScheme: 'graphtutorial'
        ]
    }
    ```

## <a name="design-the-app"></a>Diseñar la aplicación

La aplicación usará un [cajón de navegación](https://reactnavigation.org/docs/drawer-based-navigation.html) para navegar entre distintas vistas. En este paso, creará las vistas básicas que usa la aplicación e implementará el cajón de navegación.

### <a name="create-views"></a>Crear vistas

En esta sección, creará las vistas de la aplicación para admitir un [flujo de autenticación](https://reactnavigation.org/docs/auth-flow.html).

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **views**.
1. Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **HomeScreen. js**. Agregue el siguiente código al archivo.

    ```JSX
    import React from 'react';
    import {
      ActivityIndicator,
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';

    export default class HomeScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Welcome',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      state = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <View style={styles.container}>
            <ActivityIndicator animating={this.state.userLoading} size='large' />
            {this.state.userLoading ? null: <Text>Hello {this.state.userName}!</Text>}
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

1. Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **CalendarScreen. js**. Agregue el siguiente código al archivo.

    ```JSX
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';

    export default class CalendarScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Calendar',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      // Temporary placeholder view
      render() {
        return (
          <View style={styles.container}>
            <Text>Calendar</Text>
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

1. Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **SignInScreen. js**. Agregue el siguiente código al archivo.

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import React from 'react';
    import {
      Button,
      StyleSheet,
      View,
    } from 'react-native';

    export default class SignInScreen extends React.Component {
      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        // TEMPORARY
        this.props.navigation.navigate('App');
      };

      render() {
        return (
          <View style={styles.container}>
            <Button title="Sign In" onPress={this._signInAsync}/>
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

1. Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **AuthLoadingScreen. js**. Agregue el siguiente código al archivo.

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import React from 'react';
    import {
      ActivityIndicator,
      AsyncStorage,
      Text,
      StyleSheet,
      View,
    } from 'react-native';

    export default class AuthLoadingScreen extends React.Component {

      componentDidMount() {
        this._bootstrapAsync();
      }

      // Fetch the token from storage then navigate to our appropriate place
      // NOTE: Production apps should protect user tokens in secure storage.
      _bootstrapAsync = async () => {
        const userToken = await AsyncStorage.getItem('userToken');

        // This will switch to the App screen or Auth screen and this loading
        // screen will be unmounted and thrown away.
        this.props.navigation.navigate(userToken ? 'App' : 'Auth');
      };

      render() {
        return (
          <View style={styles.container}>
            <ActivityIndicator size='large' />
            <Text style={styles.statusText}>Logging in...</Text>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      },
      statusText: {
        marginTop: 10
      }
    });
    ```

### <a name="create-a-navigation-drawer"></a>Crear un cajón de navegación

En esta sección, creará un menú para la aplicación y actualizará la aplicación para que use reAct-Navigation para moverse entre las pantallas.

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **menús**.
1. Cree un archivo nuevo en el directorio **GraphTutorial/menus** denominado **DrawerMenu. js**. Agregue el siguiente código al archivo.

    ```JSX
    import React from 'react';
    import {
      Image,
      SafeAreaView,
      ScrollView,
      StyleSheet,
      Text,
      View
    } from 'react-native';
    import { DrawerItems } from 'react-navigation';

    export default class DrawerMenuContent extends React.Component {

      state = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      // Check if user tapped on the Sign Out button and
      // sign the user out
      _onItemPressed = async (route) => {
        if (route.route.routeName !== 'Sign Out') {
          this.props.onItemPress(route);
          return;
        }

        // Sign out
        // TEMPORARY
        this.props.navigation.navigate('Auth');
      }

      render() {
        return (
          <ScrollView>
            <SafeAreaView style={styles.container}
              forceInset={{ top: 'always', horizontal: 'never' }}>
              <View style={styles.profileView}>
                <Image source={this.state.userPhoto}
                  resizeMode='contain'
                  style={styles.profilePhoto} />
                <Text style={styles.profileUserName}>{this.state.userName}</Text>
                <Text style={styles.profileEmail}>{this.state.userEmail}</Text>
              </View>
              <DrawerItems {...this.props}
                onItemPress={this._onItemPressed}/>
            </SafeAreaView>
          </ScrollView>
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

1. Abra el archivo **GraphTutorial/app. js** y reemplace todo el contenido por lo siguiente.

    ```JSX
    // Adapted from https://reactnavigation.org/docs/auth-flow.html
    import {
      createSwitchNavigator,
      createStackNavigator,
      createDrawerNavigator,
      createAppContainer } from "react-navigation";

    import AuthLoadingScreen from './views/AuthLoadingScreen';
    import SignInScreen from './views/SignInScreen';
    import HomeScreen from './views/HomeScreen';
    import CalendarScreen from './views/CalendarScreen';
    import DrawerMenuContent from './menus/DrawerMenu';

    const headerOptions = {
      defaultNavigationOptions: {
        headerStyle: {
          backgroundColor: '#276b80'
        },
        headerTintColor: 'white'
      }
    };

    const AuthStack = createStackNavigator(
      {
        SignIn: SignInScreen
      },
      headerOptions
    );

    const AppDrawer = createDrawerNavigator(
      {
        Home: createStackNavigator({ Home: HomeScreen }, headerOptions),
        Calendar: createStackNavigator({ Calendar: CalendarScreen }, headerOptions),
        'Sign Out': 'SignOut'
      },
      {
        hideStatusBar: false,
        contentComponent: DrawerMenuContent
      }
    );

    export default createAppContainer(createSwitchNavigator(
      {
        AuthLoading: AuthLoadingScreen,
        App: AppDrawer,
        Auth: AuthStack
      },
      {
        initialRouteName: 'AuthLoading'
      }
    ));

1. Save all of your changes.

1. Reload the application in your emulator.

The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.

![Screenshots of the application on Android](./images/android-app-screens.png)

![Screenshots of the application on iOS](./images/ios-app-screens.png)

> [!NOTE]
> You may receive warnings when running the app about Async Storage or componentWillUpdate. For the purposes of this tutorial, you can dismiss those warnings.
