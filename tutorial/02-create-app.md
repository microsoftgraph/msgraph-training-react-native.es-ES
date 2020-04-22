<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9573b-101">Para empezar, cree un nuevo proyecto nativo de reAct.</span><span class="sxs-lookup"><span data-stu-id="9573b-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="9573b-102">Abra la interfaz de la línea de comandos (CLI) en un directorio donde desee crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9573b-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="9573b-103">Ejecute el siguiente comando para ejecutar la herramienta [reAct-Native-CLI](https://github.com/facebook/react-native) y cree un nuevo proyecto nativo reAct.</span><span class="sxs-lookup"><span data-stu-id="9573b-103">Run the following command to run the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. <span data-ttu-id="9573b-104">**Opcional:** Ejecute el proyecto para comprobar que el entorno de desarrollo está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9573b-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="9573b-105">En la CLI, cambie el directorio al directorio **GraphTutorial** que acaba de crear y ejecute uno de los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="9573b-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="9573b-106">Para iOS:`npx react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="9573b-106">For iOS: `npx react-native run-ios`</span></span>
    - <span data-ttu-id="9573b-107">Para Android: iniciar una instancia del emulador de Android y ejecutar`npx react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="9573b-107">For Android: Launch an Android emulator instance and run `npx react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="9573b-108">Instalar dependencias</span><span class="sxs-lookup"><span data-stu-id="9573b-108">Install dependencies</span></span>

<span data-ttu-id="9573b-109">Antes de continuar, instale algunas dependencias adicionales que usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="9573b-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="9573b-110">[reAct-navegación](https://reactnavigation.org) para controlar la navegación entre vistas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9573b-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="9573b-111">[reAct-Native-gesto-controlador](https://github.com/kmagiera/react-native-gesture-handler), [reAct-nativo-área-seguridad-área-contexto](https://github.com/th3rdwave/react-native-safe-area-context), [reAct-pantallas nativas](https://github.com/kmagiera/react-native-screens), [reAct-nativo-reanimate](https://github.com/kmagiera/react-native-reanimated)y [vista enmascarada](https://github.com/react-native-community/react-native-masked-view) requerida por reAct-Navigation.</span><span class="sxs-lookup"><span data-stu-id="9573b-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler), [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context), [react-native-screens](https://github.com/kmagiera/react-native-screens), [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), and [masked-view](https://github.com/react-native-community/react-native-masked-view) required by react-navigation.</span></span>
- <span data-ttu-id="9573b-112">[reAct-Native-Elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) y [reAct-Native-vector-Icons](https://github.com/oblador/react-native-vector-icons) para proporcionar iconos para la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="9573b-112">[react-native-elements](https://react-native-training.github.io/react-native-elements/docs/getting_started.html) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="9573b-113">[reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) para controlar la autenticación y la administración de tokens.</span><span class="sxs-lookup"><span data-stu-id="9573b-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="9573b-114">[almacenamiento asincrónico](https://github.com/react-native-community/react-native-async-storage) para proporcionar almacenamiento para los tokens.</span><span class="sxs-lookup"><span data-stu-id="9573b-114">[async-storage](https://github.com/react-native-community/react-native-async-storage) to provide storage for tokens.</span></span>
- <span data-ttu-id="9573b-115">[momento](https://momentjs.com) para controlar el análisis y la comparación de fechas y horas.</span><span class="sxs-lookup"><span data-stu-id="9573b-115">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="9573b-116">[Microsoft-Graph-Client](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="9573b-116">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="9573b-117">Abra la CLI en el directorio raíz del proyecto nativo reAct.</span><span class="sxs-lookup"><span data-stu-id="9573b-117">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="9573b-118">Ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="9573b-118">Run the following command.</span></span>

    ```Shell
    npm install @react-navigation/native@5.1.5 @react-navigation/drawer@5.4.1 @react-navigation/stack@5.2.10
    npm install @react-native-community/masked-view@0.1.7 react-native-safe-area-context@0.7.3
    npm install react-native-reanimated@1.8.0 react-native-screens@2.4.0 @react-native-community/async-storage@1.9.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 react-native-gesture-handler@1.6.1
    npm install react-native-app-auth@5.1.1 moment@2.24.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="9573b-119">Vincular y configurar dependencias para iOS</span><span class="sxs-lookup"><span data-stu-id="9573b-119">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="9573b-120">Si no tiene como objetivo iOS, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="9573b-120">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="9573b-121">Abra la CLI en el directorio **GraphTutorial/iOS** .</span><span class="sxs-lookup"><span data-stu-id="9573b-121">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="9573b-122">Ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="9573b-122">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="9573b-123">Abra el archivo **GraphTutorial/iOS/GraphTutorial/info. plist** en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="9573b-123">Open the **GraphTutorial/ios/GraphTutorial/Info.plist** file in a text editor.</span></span> <span data-ttu-id="9573b-124">Agregue la siguiente línea justo antes de `</dict>` la última línea del archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-124">Add the following just before the last `</dict>` line in the file.</span></span>

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

1. <span data-ttu-id="9573b-125">Abra el archivo **GraphTutorial/iOS/GraphTutorial/AppDelegate. h** en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="9573b-125">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="9573b-126">Reemplace su contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9573b-126">Replace its contents with the following.</span></span>

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="9573b-127">Configurar dependencias para Android</span><span class="sxs-lookup"><span data-stu-id="9573b-127">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="9573b-128">Si no tiene como objetivo Android, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="9573b-128">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="9573b-129">Abra el archivo **GraphTutorial/Android/App/Build. Gradle** en un editor.</span><span class="sxs-lookup"><span data-stu-id="9573b-129">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="9573b-130">Busque la `defaultConfig` entrada y agregue la siguiente propiedad en `defaultConfig`.</span><span class="sxs-lookup"><span data-stu-id="9573b-130">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    <span data-ttu-id="9573b-131">La `defaultConfig` entrada debe ser similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="9573b-131">The `defaultConfig` entry should look similar to the following.</span></span>

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. <span data-ttu-id="9573b-132">Agregue la siguiente línea al final del archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-132">Add the following line to the end of the file.</span></span>

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. <span data-ttu-id="9573b-133">Guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-133">Save the file.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="9573b-134">Diseñar la aplicación</span><span class="sxs-lookup"><span data-stu-id="9573b-134">Design the app</span></span>

<span data-ttu-id="9573b-135">La aplicación usará un [cajón de navegación](https://reactnavigation.org/docs/drawer-based-navigation.html) para navegar entre distintas vistas.</span><span class="sxs-lookup"><span data-stu-id="9573b-135">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="9573b-136">En este paso, creará las vistas básicas que usa la aplicación e implementará el cajón de navegación.</span><span class="sxs-lookup"><span data-stu-id="9573b-136">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="9573b-137">Crear vistas</span><span class="sxs-lookup"><span data-stu-id="9573b-137">Create views</span></span>

<span data-ttu-id="9573b-138">En esta sección, creará las vistas de la aplicación para admitir un [flujo de autenticación](https://reactnavigation.org/docs/auth-flow).</span><span class="sxs-lookup"><span data-stu-id="9573b-138">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow).</span></span>

1. <span data-ttu-id="9573b-139">Abra **GraphTutorial/index. js** y agregue lo siguiente a la parte superior del archivo, antes de cualquier `import` otra instrucción.</span><span class="sxs-lookup"><span data-stu-id="9573b-139">Open **GraphTutorial/index.js** and add the following to the top of the file, before any other `import` statements.</span></span>

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. <span data-ttu-id="9573b-140">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **pantallas**.</span><span class="sxs-lookup"><span data-stu-id="9573b-140">Create a new directory in the **GraphTutorial** directory named **screens**.</span></span>
1. <span data-ttu-id="9573b-141">Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **HomeScreen. TSX**.</span><span class="sxs-lookup"><span data-stu-id="9573b-141">Create a new file in the **GraphTutorial/screens** directory named **HomeScreen.tsx**.</span></span> <span data-ttu-id="9573b-142">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-142">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="9573b-143">Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **CalendarScreen. TSX**.</span><span class="sxs-lookup"><span data-stu-id="9573b-143">Create a new file in the **GraphTutorial/screens** directory named **CalendarScreen.tsx**.</span></span> <span data-ttu-id="9573b-144">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-144">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="9573b-145">Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **SignInScreen. TSX**.</span><span class="sxs-lookup"><span data-stu-id="9573b-145">Create a new file in the **GraphTutorial/screens** directory named **SignInScreen.tsx**.</span></span> <span data-ttu-id="9573b-146">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-146">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="9573b-147">Cree un archivo nuevo en el directorio **GraphTutorial/Screens** denominado **AuthLoadingScreen. TSX**.</span><span class="sxs-lookup"><span data-stu-id="9573b-147">Create a new file in the **GraphTutorial/screens** directory named **AuthLoadingScreen.tsx**.</span></span> <span data-ttu-id="9573b-148">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-148">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="9573b-149">Crear un cajón de navegación</span><span class="sxs-lookup"><span data-stu-id="9573b-149">Create a navigation drawer</span></span>

<span data-ttu-id="9573b-150">En esta sección, creará un menú para la aplicación y actualizará la aplicación para que use reAct-Navigation para moverse entre las pantallas.</span><span class="sxs-lookup"><span data-stu-id="9573b-150">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="9573b-151">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **menús**.</span><span class="sxs-lookup"><span data-stu-id="9573b-151">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>
1. <span data-ttu-id="9573b-152">Cree un archivo nuevo en el directorio **GraphTutorial o menus** denominado **HeaderComponents. TSX**.</span><span class="sxs-lookup"><span data-stu-id="9573b-152">Create a new file in the **GraphTutorial/menus** directory named **HeaderComponents.tsx**.</span></span> <span data-ttu-id="9573b-153">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-153">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/HeaderComponents.tsx" id="HeaderComponentSnippet":::

1. <span data-ttu-id="9573b-154">Cree un archivo nuevo en el directorio **GraphTutorial o menus** denominado **DrawerMenu. TSX**.</span><span class="sxs-lookup"><span data-stu-id="9573b-154">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.tsx**.</span></span> <span data-ttu-id="9573b-155">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="9573b-155">Add the following code to the file.</span></span>

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

1. <span data-ttu-id="9573b-156">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **images**.</span><span class="sxs-lookup"><span data-stu-id="9573b-156">Create a new directory in the **GraphTutorial** directory named **images**.</span></span>
1. <span data-ttu-id="9573b-157">Agregue una imagen de perfil predeterminada con el nombre **no-Profile-PIC. png** en este directorio.</span><span class="sxs-lookup"><span data-stu-id="9573b-157">Add a default profile image named **no-profile-pic.png** in this directory.</span></span> <span data-ttu-id="9573b-158">Puede usar cualquier imagen que quiera o usar la que se [muestra en este ejemplo](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).</span><span class="sxs-lookup"><span data-stu-id="9573b-158">You can use any image you like, or use [the one from this sample](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).</span></span>

1. <span data-ttu-id="9573b-159">Abra el archivo **GraphTutorial/app. TSX** y reemplace todo el contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9573b-159">Open the **GraphTutorial/App.tsx** file and replace the entire contents with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AppSnippet":::

1. <span data-ttu-id="9573b-160">Guarde todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="9573b-160">Save all of your changes.</span></span>

1. <span data-ttu-id="9573b-161">Vuelva a cargar la aplicación en el emulador.</span><span class="sxs-lookup"><span data-stu-id="9573b-161">Reload the application in your emulator.</span></span>

<span data-ttu-id="9573b-162">El menú de la aplicación debe funcionar para navegar entre los dos fragmentos y cambiar cuando Puntee **en los botones iniciar sesión** o **Cerrar sesión** .</span><span class="sxs-lookup"><span data-stu-id="9573b-162">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![Capturas de pantallas de la aplicación en Android](./images/android-app-screens.png)

![Capturas de pantallas de la aplicación en iOS](./images/ios-app-screens.png)
