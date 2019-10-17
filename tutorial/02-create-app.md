<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="02a3c-101">Para empezar, cree un nuevo proyecto nativo de reAct.</span><span class="sxs-lookup"><span data-stu-id="02a3c-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="02a3c-102">Abra la interfaz de la línea de comandos (CLI) en un directorio donde desee crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="02a3c-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="02a3c-103">Ejecute el siguiente comando para instalar la herramienta [reAct-Native-CLI](https://github.com/facebook/react-native) y crear un nuevo proyecto nativo reAct.</span><span class="sxs-lookup"><span data-stu-id="02a3c-103">Run the following command to install the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npm install -g react-native-cli
    react-native init GraphTutorial
    ```

1. <span data-ttu-id="02a3c-104">**Opcional:** Ejecute el proyecto para comprobar que el entorno de desarrollo está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="02a3c-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="02a3c-105">En la CLI, cambie el directorio al directorio **GraphTutorial** que acaba de crear y ejecute uno de los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="02a3c-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="02a3c-106">Para iOS:`react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="02a3c-106">For iOS: `react-native run-ios`</span></span>
    - <span data-ttu-id="02a3c-107">Para Android: iniciar una instancia del emulador de Android y ejecutar`react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="02a3c-107">For Android: Launch an Android emulator instance and run `react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="02a3c-108">Instalar dependencias</span><span class="sxs-lookup"><span data-stu-id="02a3c-108">Install dependencies</span></span>

<span data-ttu-id="02a3c-109">Antes de continuar, instale algunas dependencias adicionales que usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="02a3c-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="02a3c-110">[reAct-navegación](https://reactnavigation.org) para controlar la navegación entre vistas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="02a3c-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="02a3c-111">[reAct-Native-gesto-controlador](https://github.com/kmagiera/react-native-gesture-handler) y [reAct-nativo-reanimate](https://github.com/kmagiera/react-native-reanimated), requerido por reAct-Navigation.</span><span class="sxs-lookup"><span data-stu-id="02a3c-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler) and [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), required by react-navigation.</span></span>
- <span data-ttu-id="02a3c-112">[reAct-Native-Elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) y [reAct-Native-vector-Icons](https://github.com/oblador/react-native-vector-icons) para proporcionar iconos para la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="02a3c-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="02a3c-113">[reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) para controlar la autenticación y la administración de tokens.</span><span class="sxs-lookup"><span data-stu-id="02a3c-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="02a3c-114">[momento](https://momentjs.com) para controlar el análisis y la comparación de fechas y horas.</span><span class="sxs-lookup"><span data-stu-id="02a3c-114">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="02a3c-115">[Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="02a3c-115">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="02a3c-116">Abra la CLI en el directorio raíz del proyecto nativo reAct.</span><span class="sxs-lookup"><span data-stu-id="02a3c-116">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="02a3c-117">Ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="02a3c-117">Run the following command.</span></span>

    ```Shell
    npm install react-navigation@3.11.1 react-native-gesture-handler@1.3.0 react-native-reanimated@1.1.0
    npm install react-native-elements@1.1.0 react-native-vector-icons@6.6.0 moment@2.24.0
    npm install react-native-app-auth@4.4.0 @microsoft/microsoft-graph-client@1.7.0
    react-native link react-native-vector-icons
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="02a3c-118">Vincular y configurar dependencias para iOS</span><span class="sxs-lookup"><span data-stu-id="02a3c-118">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="02a3c-119">Si no tiene como objetivo iOS, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="02a3c-119">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="02a3c-120">Abra la CLI en el directorio **GraphTutorial/iOS** .</span><span class="sxs-lookup"><span data-stu-id="02a3c-120">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="02a3c-121">Ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="02a3c-121">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="02a3c-122">Abra el archivo **GraphTutorial/iOS/GraphTutorial/AppDelegate. h** en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="02a3c-122">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="02a3c-123">Reemplace su contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="02a3c-123">Replace its contents with the following.</span></span>

    ```obj-c
    #import <React/RCTBridgeDelegate.h>
    #import <UIKit/UIKit.h>
    #import "RNAppAuthAuthorizationFlowManager.h"

    @interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, RNAppAuthAuthorizationFlowManager>

    @property (nonatomic, strong) UIWindow *window;
    @property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate> authorizationFlowManagerDelegate;

    @end
    ```

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="02a3c-124">Configurar dependencias para Android</span><span class="sxs-lookup"><span data-stu-id="02a3c-124">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="02a3c-125">Si no tiene como objetivo Android, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="02a3c-125">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="02a3c-126">Abra el archivo **GraphTutorial/Android/App/Build. Gradle** en un editor.</span><span class="sxs-lookup"><span data-stu-id="02a3c-126">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="02a3c-127">Busque la `defaultConfig` entrada y agregue la siguiente propiedad en `defaultConfig`.</span><span class="sxs-lookup"><span data-stu-id="02a3c-127">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

1. <span data-ttu-id="02a3c-128">Guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="02a3c-128">Save the file.</span></span> <span data-ttu-id="02a3c-129">La `defaultConfig` entrada debe ser similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="02a3c-129">The `defaultConfig` entry should look similar to the following.</span></span>

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

## <a name="design-the-app"></a><span data-ttu-id="02a3c-130">Diseñar la aplicación</span><span class="sxs-lookup"><span data-stu-id="02a3c-130">Design the app</span></span>

<span data-ttu-id="02a3c-131">La aplicación usará un [cajón de navegación](https://reactnavigation.org/docs/drawer-based-navigation.html) para navegar entre distintas vistas.</span><span class="sxs-lookup"><span data-stu-id="02a3c-131">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="02a3c-132">En este paso, creará las vistas básicas que usa la aplicación e implementará el cajón de navegación.</span><span class="sxs-lookup"><span data-stu-id="02a3c-132">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="02a3c-133">Crear vistas</span><span class="sxs-lookup"><span data-stu-id="02a3c-133">Create views</span></span>

<span data-ttu-id="02a3c-134">En esta sección, creará las vistas de la aplicación para admitir un [flujo de autenticación](https://reactnavigation.org/docs/auth-flow.html).</span><span class="sxs-lookup"><span data-stu-id="02a3c-134">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow.html).</span></span>

1. <span data-ttu-id="02a3c-135">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **views**.</span><span class="sxs-lookup"><span data-stu-id="02a3c-135">Create a new directory in the **GraphTutorial** directory named **views**.</span></span>
1. <span data-ttu-id="02a3c-136">Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **HomeScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="02a3c-136">Create a new file in the **GraphTutorial/views** directory named **HomeScreen.js**.</span></span> <span data-ttu-id="02a3c-137">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="02a3c-137">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="02a3c-138">Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **CalendarScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="02a3c-138">Create a new file in the **GraphTutorial/views** directory named **CalendarScreen.js**.</span></span> <span data-ttu-id="02a3c-139">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="02a3c-139">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="02a3c-140">Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **SignInScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="02a3c-140">Create a new file in the **GraphTutorial/views** directory named **SignInScreen.js**.</span></span> <span data-ttu-id="02a3c-141">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="02a3c-141">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="02a3c-142">Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **AuthLoadingScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="02a3c-142">Create a new file in the **GraphTutorial/views** directory named **AuthLoadingScreen.js**.</span></span> <span data-ttu-id="02a3c-143">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="02a3c-143">Add the following code to the file.</span></span>

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

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="02a3c-144">Crear un cajón de navegación</span><span class="sxs-lookup"><span data-stu-id="02a3c-144">Create a navigation drawer</span></span>

<span data-ttu-id="02a3c-145">En esta sección, creará un menú para la aplicación y actualizará la aplicación para que use reAct-Navigation para moverse entre las pantallas.</span><span class="sxs-lookup"><span data-stu-id="02a3c-145">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="02a3c-146">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **menús**.</span><span class="sxs-lookup"><span data-stu-id="02a3c-146">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="02a3c-147">Cree un archivo nuevo en el directorio **GraphTutorial/menus** denominado **DrawerMenu. js**.</span><span class="sxs-lookup"><span data-stu-id="02a3c-147">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.js**.</span></span> <span data-ttu-id="02a3c-148">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="02a3c-148">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="02a3c-149">Abra el archivo **GraphTutorial/app. js** y reemplace todo el contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="02a3c-149">Open the **GraphTutorial/App.js** file and replace the entire contents with the following.</span></span>

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
    ```

1. <span data-ttu-id="02a3c-150">Guarde todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="02a3c-150">Save all of your changes.</span></span>

1. <span data-ttu-id="02a3c-151">Vuelva a cargar la aplicación en el emulador.</span><span class="sxs-lookup"><span data-stu-id="02a3c-151">Reload the application in your emulator.</span></span>

<span data-ttu-id="02a3c-152">El menú de la aplicación debe funcionar para navegar entre los dos fragmentos y cambiar cuando Puntee **en los botones iniciar sesión** o **Cerrar sesión** .</span><span class="sxs-lookup"><span data-stu-id="02a3c-152">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![Capturas de pantallas de la aplicación en Android](./images/android-app-screens.png)

![Capturas de pantallas de la aplicación en iOS](./images/ios-app-screens.png)

> [!NOTE]
> <span data-ttu-id="02a3c-155">Es posible que reciba advertencias al ejecutar la aplicación sobre almacenamiento asíncrono o componentWillUpdate.</span><span class="sxs-lookup"><span data-stu-id="02a3c-155">You may receive warnings when running the app about Async Storage or componentWillUpdate.</span></span> <span data-ttu-id="02a3c-156">Para los fines de este tutorial, puede descartar esas advertencias.</span><span class="sxs-lookup"><span data-stu-id="02a3c-156">For the purposes of this tutorial, you can dismiss those warnings.</span></span>
