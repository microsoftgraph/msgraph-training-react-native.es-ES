<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="a06d5-101">En este ejercicio, ampliará la aplicación del ejercicio anterior para admitir la autenticación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a06d5-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="a06d5-102">Esto es necesario para obtener el token de acceso de OAuth necesario para llamar a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="a06d5-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="a06d5-103">Para ello, integrará la biblioteca de [reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a06d5-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="a06d5-104">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **auth**.</span><span class="sxs-lookup"><span data-stu-id="a06d5-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="a06d5-105">Cree un archivo nuevo en el directorio **GraphTutorial/auth** denominado **AuthConfig. js**.</span><span class="sxs-lookup"><span data-stu-id="a06d5-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.js**.</span></span> <span data-ttu-id="a06d5-106">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="a06d5-106">Add the following code to the file.</span></span>

    ```js
    export const AuthConfig = {
      appId = 'YOUR_APP_ID_HERE',
      appScopes = [
        'openid',
        'offline_access',
        'profile',
        'User.Read',
        'Calendars.Read'
      ]
    };
    ```

    <span data-ttu-id="a06d5-107">Reemplace `YOUR_APP_ID_HERE` por el identificador de la aplicación del registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a06d5-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a06d5-108">Si usa un control de código fuente como GIT, ahora sería un buen momento para excluir el archivo **AuthConfig. js** del control de código fuente para evitar la pérdida inadvertida del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a06d5-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="a06d5-109">Implementar el inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a06d5-109">Implement sign-in</span></span>

<span data-ttu-id="a06d5-110">En esta sección, creará una clase auxiliar de autenticación y actualizará la aplicación para iniciar sesión y cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="a06d5-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="a06d5-111">Cree un archivo nuevo en el directorio **GraphTutorial/auth** denominado **AuthManager. js**.</span><span class="sxs-lookup"><span data-stu-id="a06d5-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.js**.</span></span> <span data-ttu-id="a06d5-112">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="a06d5-112">Add the following code to the file.</span></span>

    ```js
    import { AuthConfig } from './AuthConfig';
    import { AsyncStorage } from 'react-native';
    import { authorize, refresh } from 'react-native-app-auth';
    import moment from 'moment';

    const config = {
      clientId: AuthConfig.appId,
      redirectUrl: Platform.OS === 'ios' ? 'urn:ietf:wg:oauth:2.0:oob' : 'graph-tutorial://react-native-auth',
      scopes: AuthConfig.appScopes,
      additionalParameters: { prompt: 'select_account' },
      serviceConfiguration: {
        authorizationEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/authorize',
        tokenEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/token',
      }
    };

    export class AuthManager {

      static signInAsync = async () => {
        const result = await authorize(config);

        // Store the access token, refresh token, and expiration time in storage
        await AsyncStorage.setItem('userToken', result.accessToken);
        await AsyncStorage.setItem('refreshToken', result.refreshToken);
        await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);
      }

      static signOutAsync = async () => {
        // Clear storage
        await AsyncStorage.removeItem('userToken');
        await AsyncStorage.removeItem('refreshToken');
        await AsyncStorage.removeItem('expireTime');
      }

      static getAccessTokenAsync = async() => {
        const expireTime = await AsyncStorage.getItem('expireTime');

        if (expireTime !== null) {
          // Get expiration time - 5 minutes
          // If it's <= 5 minutes before expiration, then refresh
          const expire = moment(expireTime).subtract(5, 'minutes');
          const now = moment();

          if (now.isSameOrAfter(expire)) {
            // Expired, refresh
            const refreshToken = await AsyncStorage.getItem('refreshToken');

            const result = await refresh(config, {refreshToken: refreshToken});

            // Store the new access token, refresh token, and expiration time in storage
            await AsyncStorage.setItem('userToken', result.accessToken);
            await AsyncStorage.setItem('refreshToken', result.refreshToken);
            await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);

            return result.accessToken;
          }

          // Not expired, just return saved access token
          const accessToken = await AsyncStorage.getItem('userToken');
          return accessToken;
        }

        return null;
      }
    }
    ```

1. <span data-ttu-id="a06d5-113">Abra el archivo **GraphTutorial/views/SignInScreen. js** y agregue la `import` siguiente instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="a06d5-113">Open the **GraphTutorial/views/SignInScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="a06d5-114">Reemplace el método `_signInAsync` existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="a06d5-114">Replace the existing `_signInAsync` method with the following.</span></span>

    ```js
    _signInAsync = async () => {
      try {
        await AuthManager.signInAsync();
        this.props.navigation.navigate('App');
      } catch (error) {
        alert(error);
      }
    };

1. Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="a06d5-115">Agregue el método siguiente a la clase `HomeScreen`.</span><span class="sxs-lookup"><span data-stu-id="a06d5-115">Add the following method to the `HomeScreen` class.</span></span>

    ```js
    async componentDidMount() {
      try {
        const accessToken = await AuthManager.getAccessTokenAsync();

        // TEMPORARY
        this.setState({userName: accessToken, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. <span data-ttu-id="a06d5-116">Abra el archivo **GraphTutorial/menus/DrawerMenu. js** y agregue la `import` siguiente instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="a06d5-116">Open the **GraphTutorial/menus/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="a06d5-117">En `_onItemPressed`, reemplace la `// TEMPORARY` línea con la siguiente.</span><span class="sxs-lookup"><span data-stu-id="a06d5-117">In `_onItemPressed`, replace the `// TEMPORARY` line with the following.</span></span>

    ```js
    await AuthManager.signOutAsync();
    ```

1. <span data-ttu-id="a06d5-118">Guarde los cambios y vuelva a cargar la aplicación en el emulador.</span><span class="sxs-lookup"><span data-stu-id="a06d5-118">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="a06d5-119">Si inicia sesión en la aplicación, debería ver un token de acceso que se muestra en la pantalla de **bienvenida** .</span><span class="sxs-lookup"><span data-stu-id="a06d5-119">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="a06d5-120">Obtener detalles del usuario</span><span class="sxs-lookup"><span data-stu-id="a06d5-120">Get user details</span></span>

<span data-ttu-id="a06d5-121">En esta sección, creará un proveedor de autenticación personalizado para la biblioteca cliente de Graph, creará una clase auxiliar que contendrá todas las llamadas a Microsoft Graph y `HomeScreen` actualizará las clases y `DrawerMenuContent` para que usen esta nueva clase para obtener el usuario que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="a06d5-121">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `HomeScreen` and `DrawerMenuContent` classes to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="a06d5-122">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **Graph**.</span><span class="sxs-lookup"><span data-stu-id="a06d5-122">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="a06d5-123">Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphAuthProvider. js**.</span><span class="sxs-lookup"><span data-stu-id="a06d5-123">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.js**.</span></span> <span data-ttu-id="a06d5-124">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="a06d5-124">Add the following code to the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';

    // Used by Graph client to get access tokens
    // See https://github.com/microsoftgraph/msgraph-sdk-javascript/blob/dev/docs/CustomAuthenticationProvider.md
    export class GraphAuthProvider {
      getAccessToken = async() => {
        return await AuthManager.getAccessTokenAsync();
      }
    }
    ```

1. <span data-ttu-id="a06d5-125">Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphManager. js**.</span><span class="sxs-lookup"><span data-stu-id="a06d5-125">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.js**.</span></span> <span data-ttu-id="a06d5-126">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="a06d5-126">Add the following code to the file.</span></span>

    ```js
    import { Client } from '@microsoft/microsoft-graph-client';
    import { GraphAuthProvider } from './GraphAuthProvider';

    // Set the authProvider to an instance
    // of GraphAuthProvider
    const clientOptions = {
      authProvider: new GraphAuthProvider()
    };

    // Initialize the client
    const graphClient = Client.initWithMiddleware(clientOptions);

    export class GraphManager {
      static getUserAsync = async() => {
        // GET /me
        return graphClient.api('/me').get();
      }
    }
    ```

1. <span data-ttu-id="a06d5-127">Abra el archivo **GraphTutorial/views/HomeScreen. js** y agregue la `import` siguiente instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="a06d5-127">Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="a06d5-128">Reemplace el `componentDidMount` método por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="a06d5-128">Replace the `componentDidMount` method with the following.</span></span>

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();
        // Set the user name to the user's given name
        this.setState({userName: user.givenName, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. <span data-ttu-id="a06d5-129">Abra el archivo **GraphTutorial/views/DrawerMenu. js** y agregue la `import` siguiente instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="a06d5-129">Open the **GraphTutorial/views/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="a06d5-130">Agregue el método `componentDidMount` siguiente a la `DrawerMenuContent` clase.</span><span class="sxs-lookup"><span data-stu-id="a06d5-130">Add the following `componentDidMount` method to the `DrawerMenuContent` class.</span></span>

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();

        // Update UI with display name and email
        this.setState({
          userName: user.displayName,
          // Work/School accounts have email address in mail attribute
          // Personal accounts have it in userPrincipalName
          userEmail: user.mail !== null ? user.mail : user.userPrincipalName,
        });
      } catch(error) {
        alert(error);
      }
    }
    ```

<span data-ttu-id="a06d5-131">Si guarda los cambios y vuelve a cargar la aplicación ahora, después de iniciar sesión, la interfaz de usuario se actualizará con el nombre para mostrar y la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="a06d5-131">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
