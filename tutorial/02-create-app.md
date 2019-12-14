<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="84f07-101">Para empezar, cree un nuevo proyecto nativo de reAct.</span><span class="sxs-lookup"><span data-stu-id="84f07-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="84f07-102">Abra la interfaz de la línea de comandos (CLI) en un directorio donde desee crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="84f07-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="84f07-103">Ejecute el siguiente comando para ejecutar la herramienta [reAct-Native-CLI](https://github.com/facebook/react-native) y cree un nuevo proyecto nativo reAct.</span><span class="sxs-lookup"><span data-stu-id="84f07-103">Run the following command to run the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npx react-native init GraphTutorial
    ```

1. <span data-ttu-id="84f07-104">**Opcional:** Ejecute el proyecto para comprobar que el entorno de desarrollo está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="84f07-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="84f07-105">En la CLI, cambie el directorio al directorio **GraphTutorial** que acaba de crear y ejecute uno de los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="84f07-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="84f07-106">Para iOS:`npx react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="84f07-106">For iOS: `npx react-native run-ios`</span></span>
    - <span data-ttu-id="84f07-107">Para Android: iniciar una instancia del emulador de Android y ejecutar`npx react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="84f07-107">For Android: Launch an Android emulator instance and run `npx react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="84f07-108">Instalar dependencias</span><span class="sxs-lookup"><span data-stu-id="84f07-108">Install dependencies</span></span>

<span data-ttu-id="84f07-109">Antes de continuar, instale algunas dependencias adicionales que usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="84f07-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="84f07-110">[reAct-navegación](https://reactnavigation.org) para controlar la navegación entre vistas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="84f07-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="84f07-111">[reAct-Native-gesto-controlador](https://github.com/kmagiera/react-native-gesture-handler) y [reAct-nativo-reanimate](https://github.com/kmagiera/react-native-reanimated), requerido por reAct-Navigation.</span><span class="sxs-lookup"><span data-stu-id="84f07-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler) and [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), required by react-navigation.</span></span>
- <span data-ttu-id="84f07-112">[reAct-Native-Elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) y [reAct-Native-vector-Icons](https://github.com/oblador/react-native-vector-icons) para proporcionar iconos para la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="84f07-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="84f07-113">[reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) para controlar la autenticación y la administración de tokens.</span><span class="sxs-lookup"><span data-stu-id="84f07-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="84f07-114">[momento](https://momentjs.com) para controlar el análisis y la comparación de fechas y horas.</span><span class="sxs-lookup"><span data-stu-id="84f07-114">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="84f07-115">[Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="84f07-115">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="84f07-116">Abra la CLI en el directorio raíz del proyecto nativo reAct.</span><span class="sxs-lookup"><span data-stu-id="84f07-116">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="84f07-117">Ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="84f07-117">Run the following command.</span></span>

    ```Shell
    npm install react-navigation@3.11.1 react-native-gesture-handler@1.5.2 react-native-reanimated@1.4.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 moment@2.24.0
    npm install react-native-app-auth@4.4.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="84f07-118">Vincular y configurar dependencias para iOS</span><span class="sxs-lookup"><span data-stu-id="84f07-118">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="84f07-119">Si no tiene como objetivo iOS, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="84f07-119">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="84f07-120">Abra la CLI en el directorio **GraphTutorial/iOS** .</span><span class="sxs-lookup"><span data-stu-id="84f07-120">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="84f07-121">Ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="84f07-121">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="84f07-122">Abra el archivo **GraphTutorial/iOS/GraphTutorial/info. plist** en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="84f07-122">Open the **GraphTutorial/ios/GraphTutorial/Info.plist** file in a text editor.</span></span> <span data-ttu-id="84f07-123">Agregue la siguiente línea justo antes de `</dict>` la última línea del archivo.</span><span class="sxs-lookup"><span data-stu-id="84f07-123">Add the following just before the last `</dict>` line in the file.</span></span>

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

1. <span data-ttu-id="84f07-124">Abra el archivo **GraphTutorial/iOS/GraphTutorial/AppDelegate. h** en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="84f07-124">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="84f07-125">Reemplace su contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="84f07-125">Replace its contents with the following.</span></span>

    ```obj-c
    #import <React/RCTBridgeDelegate.h>
    #import <UIKit/UIKit.h>
    #import "RNAppAuthAuthorizationFlowManager.h"

    @interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, RNAppAuthAuthorizationFlowManager>

    @property (nonatomic, strong) UIWindow *window;
    @property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate> authorizationFlowManagerDelegate;

    @end
    ```

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="84f07-126">Configurar dependencias para Android</span><span class="sxs-lookup"><span data-stu-id="84f07-126">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="84f07-127">Si no tiene como objetivo Android, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="84f07-127">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="84f07-128">Abra el archivo **GraphTutorial/Android/App/Build. Gradle** en un editor.</span><span class="sxs-lookup"><span data-stu-id="84f07-128">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="84f07-129">Busque la `defaultConfig` entrada y agregue la siguiente propiedad en `defaultConfig`.</span><span class="sxs-lookup"><span data-stu-id="84f07-129">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    <span data-ttu-id="84f07-130">La `defaultConfig` entrada debe ser similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="84f07-130">The `defaultConfig` entry should look similar to the following.</span></span>

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

1. <span data-ttu-id="84f07-131">Agregue la siguiente línea al final del archivo.</span><span class="sxs-lookup"><span data-stu-id="84f07-131">Add the following line to the end of the file.</span></span>

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. <span data-ttu-id="84f07-132">Guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="84f07-132">Save the file.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="84f07-133">Diseñar la aplicación</span><span class="sxs-lookup"><span data-stu-id="84f07-133">Design the app</span></span>

<span data-ttu-id="84f07-134">La aplicación usará un [cajón de navegación](https://reactnavigation.org/docs/drawer-based-navigation.html) para navegar entre distintas vistas.</span><span class="sxs-lookup"><span data-stu-id="84f07-134">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="84f07-135">En este paso, creará las vistas básicas que usa la aplicación e implementará el cajón de navegación.</span><span class="sxs-lookup"><span data-stu-id="84f07-135">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="84f07-136">Crear vistas</span><span class="sxs-lookup"><span data-stu-id="84f07-136">Create views</span></span>

<span data-ttu-id="84f07-137">En esta sección, creará las vistas de la aplicación para admitir un [flujo de autenticación](https://reactnavigation.org/docs/auth-flow.html).</span><span class="sxs-lookup"><span data-stu-id="84f07-137">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow.html).</span></span>

1. <span data-ttu-id="84f07-138">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **views**.</span><span class="sxs-lookup"><span data-stu-id="84f07-138">Create a new directory in the **GraphTutorial** directory named **views**.</span></span>
1. <span data-ttu-id="84f07-139">Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **HomeScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="84f07-139">Create a new file in the **GraphTutorial/views** directory named **HomeScreen.js**.</span></span> <span data-ttu-id="84f07-140">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="84f07-140">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="84f07-141">Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **CalendarScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="84f07-141">Create a new file in the **GraphTutorial/views** directory named **CalendarScreen.js**.</span></span> <span data-ttu-id="84f07-142">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="84f07-142">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="84f07-143">Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **SignInScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="84f07-143">Create a new file in the **GraphTutorial/views** directory named **SignInScreen.js**.</span></span> <span data-ttu-id="84f07-144">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="84f07-144">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="84f07-145">Cree un nuevo archivo en el directorio **GraphTutorial/views** denominado **AuthLoadingScreen. js**.</span><span class="sxs-lookup"><span data-stu-id="84f07-145">Create a new file in the **GraphTutorial/views** directory named **AuthLoadingScreen.js**.</span></span> <span data-ttu-id="84f07-146">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="84f07-146">Add the following code to the file.</span></span>

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

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="84f07-147">Crear un cajón de navegación</span><span class="sxs-lookup"><span data-stu-id="84f07-147">Create a navigation drawer</span></span>

<span data-ttu-id="84f07-148">En esta sección, creará un menú para la aplicación y actualizará la aplicación para que use reAct-Navigation para moverse entre las pantallas.</span><span class="sxs-lookup"><span data-stu-id="84f07-148">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="84f07-149">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **menús**.</span><span class="sxs-lookup"><span data-stu-id="84f07-149">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="84f07-150">Cree un archivo nuevo en el directorio **GraphTutorial/menus** denominado **DrawerMenu. js**.</span><span class="sxs-lookup"><span data-stu-id="84f07-150">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.js**.</span></span> <span data-ttu-id="84f07-151">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="84f07-151">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="84f07-152">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **images**.</span><span class="sxs-lookup"><span data-stu-id="84f07-152">Create a new directory in the **GraphTutorial** directory named **images**.</span></span>
1. <span data-ttu-id="84f07-153">Agregue una imagen de perfil predeterminada con el nombre **no-Profile-PIC. png** en este directorio.</span><span class="sxs-lookup"><span data-stu-id="84f07-153">Add a default profile image named **no-profile-pic.png** in this directory.</span></span> <span data-ttu-id="84f07-154">Puede usar cualquier imagen que quiera o usar la que se [muestra en este ejemplo](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demos/01-create-app/GraphTutorial/images/no-profile-pic.png).</span><span class="sxs-lookup"><span data-stu-id="84f07-154">You can use any image you like, or use [the one from this sample](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demos/01-create-app/GraphTutorial/images/no-profile-pic.png).</span></span>

1. <span data-ttu-id="84f07-155">Abra el archivo **GraphTutorial/app. js** y reemplace todo el contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="84f07-155">Open the **GraphTutorial/App.js** file and replace the entire contents with the following.</span></span>

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

1. <span data-ttu-id="84f07-156">Guarde todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="84f07-156">Save all of your changes.</span></span>

1. <span data-ttu-id="84f07-157">Vuelva a cargar la aplicación en el emulador.</span><span class="sxs-lookup"><span data-stu-id="84f07-157">Reload the application in your emulator.</span></span>

<span data-ttu-id="84f07-158">El menú de la aplicación debe funcionar para navegar entre los dos fragmentos y cambiar cuando Puntee **en los botones iniciar sesión** o **Cerrar sesión** .</span><span class="sxs-lookup"><span data-stu-id="84f07-158">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![Capturas de pantallas de la aplicación en Android](./images/android-app-screens.png)

![Capturas de pantallas de la aplicación en iOS](./images/ios-app-screens.png)

> [!NOTE]
> <span data-ttu-id="84f07-161">Es posible que reciba advertencias al ejecutar la aplicación sobre almacenamiento asíncrono o componentWillUpdate.</span><span class="sxs-lookup"><span data-stu-id="84f07-161">You may receive warnings when running the app about Async Storage or componentWillUpdate.</span></span> <span data-ttu-id="84f07-162">Para los fines de este tutorial, puede descartar esas advertencias.</span><span class="sxs-lookup"><span data-stu-id="84f07-162">For the purposes of this tutorial, you can dismiss those warnings.</span></span>
