<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="77dd3-101">En este ejercicio, ampliará la aplicación del ejercicio anterior para admitir la autenticación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77dd3-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="77dd3-102">Esto es necesario para obtener el token de acceso de OAuth necesario para llamar a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="77dd3-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="77dd3-103">Para ello, integrará la biblioteca de [reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77dd3-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="77dd3-104">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **auth**.</span><span class="sxs-lookup"><span data-stu-id="77dd3-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="77dd3-105">Cree un nuevo archivo en el directorio **GraphTutorial/auth** denominado **AuthConfig. ts**.</span><span class="sxs-lookup"><span data-stu-id="77dd3-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.ts**.</span></span> <span data-ttu-id="77dd3-106">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="77dd3-106">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.example.ts":::

    <span data-ttu-id="77dd3-107">Reemplace `YOUR_APP_ID_HERE` por el identificador de la aplicación del registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77dd3-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77dd3-108">Si usa un control de código fuente como GIT, ahora sería un buen momento para excluir el archivo **AuthConfig. ts** del control de código fuente para evitar la pérdida inadvertida del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77dd3-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.ts** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="77dd3-109">Implementar el inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="77dd3-109">Implement sign-in</span></span>

<span data-ttu-id="77dd3-110">En esta sección, creará una clase auxiliar de autenticación y actualizará la aplicación para iniciar sesión y cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="77dd3-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="77dd3-111">Cree un nuevo archivo en el directorio **GraphTutorial/auth** denominado **AuthManager. ts**.</span><span class="sxs-lookup"><span data-stu-id="77dd3-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.ts**.</span></span> <span data-ttu-id="77dd3-112">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="77dd3-112">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. <span data-ttu-id="77dd3-113">Abra el archivo **GraphTutorial/app. TSX** y agregue la siguiente `import` instrucción en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="77dd3-113">Open the **GraphTutorial/App.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from './auth/AuthManager';
    ```

1. <span data-ttu-id="77dd3-114">Reemplace la `authContext` declaración existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="77dd3-114">Replace the existing `authContext` declaration with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AuthContextSnippet" highlight="4-6,9":::

1. <span data-ttu-id="77dd3-115">Abra el archivo **GraphTutorial/menus/DrawerMenu. TSX** y agregue la siguiente `import` instrucción en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="77dd3-115">Open the **GraphTutorial/menus/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="77dd3-116">Agregue el siguiente código a la `componentDidMount` función.</span><span class="sxs-lookup"><span data-stu-id="77dd3-116">Add the following code to the `componentDidMount` function.</span></span>

    ```typescript
    try {
      const accessToken = await AuthManager.getAccessTokenAsync();

      // TEMPORARY
      this.setState({userFirstName: accessToken, userLoading: false});
    } catch (error) {
      Alert.alert(
        'Error getting token',
        JSON.stringify(error),
        [
          {
            text: 'OK'
          }
        ],
        { cancelable: false }
      );
    }
    ```

1. <span data-ttu-id="77dd3-117">Guarde los cambios y vuelva a cargar la aplicación en el emulador.</span><span class="sxs-lookup"><span data-stu-id="77dd3-117">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="77dd3-118">Si inicia sesión en la aplicación, debería ver un token de acceso que se muestra en la pantalla de **bienvenida** .</span><span class="sxs-lookup"><span data-stu-id="77dd3-118">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="77dd3-119">Obtener detalles del usuario</span><span class="sxs-lookup"><span data-stu-id="77dd3-119">Get user details</span></span>

<span data-ttu-id="77dd3-120">En esta sección, creará un proveedor de autenticación personalizado para la biblioteca cliente de Graph, creará una clase auxiliar que contendrá todas las llamadas a Microsoft Graph y actualizará la `DrawerMenuContent` clase para que use esta nueva clase para obtener el usuario que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="77dd3-120">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `DrawerMenuContent` class to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="77dd3-121">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **Graph**.</span><span class="sxs-lookup"><span data-stu-id="77dd3-121">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="77dd3-122">Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphAuthProvider. ts**.</span><span class="sxs-lookup"><span data-stu-id="77dd3-122">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.ts**.</span></span> <span data-ttu-id="77dd3-123">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="77dd3-123">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. <span data-ttu-id="77dd3-124">Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphManager. ts**.</span><span class="sxs-lookup"><span data-stu-id="77dd3-124">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.ts**.</span></span> <span data-ttu-id="77dd3-125">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="77dd3-125">Add the following code to the file.</span></span>

    ```typescript
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
        return await graphClient
          .api('/me')
          .select('displayName,givenName,mail,mailboxSettings,userPrincipalName')
          .get();
      }
    }
    ```

1. <span data-ttu-id="77dd3-126">Abra el archivo **GraphTutorial/views/DrawerMenu. TSX** y agregue la siguiente `import` instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="77dd3-126">Open the **GraphTutorial/views/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="77dd3-127">Reemplace el `componentDidMount` método por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="77dd3-127">Replace the `componentDidMount` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

<span data-ttu-id="77dd3-128">Si guarda los cambios y vuelve a cargar la aplicación ahora, después de iniciar sesión, la interfaz de usuario se actualizará con el nombre para mostrar y la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="77dd3-128">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
