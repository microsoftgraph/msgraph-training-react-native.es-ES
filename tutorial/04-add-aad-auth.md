<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ae355-101">En este ejercicio, ampliará la aplicación del ejercicio anterior para admitir la autenticación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae355-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="ae355-102">Esto es necesario para obtener el token de acceso de OAuth necesario para llamar a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ae355-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="ae355-103">Para ello, integrará la biblioteca de [reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae355-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="ae355-104">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **auth**.</span><span class="sxs-lookup"><span data-stu-id="ae355-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="ae355-105">Cree un nuevo archivo en el directorio **GraphTutorial/auth** denominado **AuthConfig. ts**.</span><span class="sxs-lookup"><span data-stu-id="ae355-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.ts**.</span></span> <span data-ttu-id="ae355-106">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-106">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.ts.example":::

    <span data-ttu-id="ae355-107">Reemplace `YOUR_APP_ID_HERE` por el identificador de la aplicación del registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae355-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae355-108">Si usa un control de código fuente como GIT, ahora sería un buen momento para excluir el archivo **AuthConfig. ts** del control de código fuente para evitar la pérdida inadvertida del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae355-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.ts** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="ae355-109">Implementar el inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ae355-109">Implement sign-in</span></span>

<span data-ttu-id="ae355-110">En esta sección, creará una clase auxiliar de autenticación y actualizará la aplicación para iniciar sesión y cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="ae355-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="ae355-111">Cree un nuevo archivo en el directorio **GraphTutorial/auth** denominado **AuthManager. ts**.</span><span class="sxs-lookup"><span data-stu-id="ae355-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.ts**.</span></span> <span data-ttu-id="ae355-112">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-112">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. <span data-ttu-id="ae355-113">Abra el archivo **GraphTutorial/views/SignInScreen. TSX** y agregue la `import` siguiente instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-113">Open the **GraphTutorial/views/SignInScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="ae355-114">Reemplace el método `_signInAsync` existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="ae355-114">Replace the existing `_signInAsync` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/SignInScreen.tsx" id="SignInAsyncSnippet":::

1. <span data-ttu-id="ae355-115">Abra el archivo **GraphTutorial/views/HomeScreen. TSX** y agregue la `import` siguiente instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-115">Open the **GraphTutorial/views/HomeScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="ae355-116">Agregue el método siguiente a la clase `HomeScreen`.</span><span class="sxs-lookup"><span data-stu-id="ae355-116">Add the following method to the `HomeScreen` class.</span></span>

    ```typescript
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

1. <span data-ttu-id="ae355-117">Abra el archivo **GraphTutorial/menus/DrawerMenu. TSX** y agregue la `import` siguiente instrucción en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-117">Open the **GraphTutorial/menus/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="ae355-118">Reemplace el método `_signOut` existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="ae355-118">Replace the existing `_signOut` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="SignOutSnippet" highlight="5":::

1. <span data-ttu-id="ae355-119">Guarde los cambios y vuelva a cargar la aplicación en el emulador.</span><span class="sxs-lookup"><span data-stu-id="ae355-119">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="ae355-120">Si inicia sesión en la aplicación, debería ver un token de acceso que se muestra en la pantalla de **bienvenida** .</span><span class="sxs-lookup"><span data-stu-id="ae355-120">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="ae355-121">Obtener detalles del usuario</span><span class="sxs-lookup"><span data-stu-id="ae355-121">Get user details</span></span>

<span data-ttu-id="ae355-122">En esta sección, creará un proveedor de autenticación personalizado para la biblioteca cliente de Graph, creará una clase auxiliar que contendrá todas las llamadas a Microsoft Graph y `HomeScreen` actualizará las clases y `DrawerMenuContent` para que usen esta nueva clase para obtener el usuario que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="ae355-122">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `HomeScreen` and `DrawerMenuContent` classes to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="ae355-123">Cree un nuevo directorio en el directorio **GraphTutorial** denominado **Graph**.</span><span class="sxs-lookup"><span data-stu-id="ae355-123">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="ae355-124">Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphAuthProvider. ts**.</span><span class="sxs-lookup"><span data-stu-id="ae355-124">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.ts**.</span></span> <span data-ttu-id="ae355-125">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-125">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. <span data-ttu-id="ae355-126">Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphManager. ts**.</span><span class="sxs-lookup"><span data-stu-id="ae355-126">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.ts**.</span></span> <span data-ttu-id="ae355-127">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-127">Add the following code to the file.</span></span>

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
        return graphClient.api('/me').get();
      }
    }
    ```

1. <span data-ttu-id="ae355-128">Abra el archivo **GraphTutorial/views/HomeScreen. TSX** y agregue la `import` siguiente instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-128">Open the **GraphTutorial/views/HomeScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="ae355-129">Reemplace el `componentDidMount` método por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="ae355-129">Replace the `componentDidMount` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="ComponentDidMountSnippet" highlight="3-6,9":::

1. <span data-ttu-id="ae355-130">Abra el archivo **GraphTutorial/views/DrawerMenu. TSX** y agregue la `import` siguiente instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="ae355-130">Open the **GraphTutorial/views/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="ae355-131">Agregue el método `componentDidMount` siguiente a la `DrawerMenuContent` clase.</span><span class="sxs-lookup"><span data-stu-id="ae355-131">Add the following `componentDidMount` method to the `DrawerMenuContent` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

<span data-ttu-id="ae355-132">Si guarda los cambios y vuelve a cargar la aplicación ahora, después de iniciar sesión, la interfaz de usuario se actualizará con el nombre para mostrar y la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="ae355-132">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
