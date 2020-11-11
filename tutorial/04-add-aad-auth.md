<!-- markdownlint-disable MD002 MD041 -->

En este ejercicio, ampliará la aplicación del ejercicio anterior para admitir la autenticación con Azure AD. Esto es necesario para obtener el token de acceso de OAuth necesario para llamar a Microsoft Graph. Para ello, integrará la biblioteca de [reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) en la aplicación.

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **auth**.
1. Cree un nuevo archivo en el directorio **GraphTutorial/auth** denominado **AuthConfig. ts**. Agregue el siguiente código al archivo.

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.example.ts":::

    Reemplace `YOUR_APP_ID_HERE` por el identificador de la aplicación del registro de la aplicación.

> [!IMPORTANT]
> Si usa un control de código fuente como GIT, ahora sería un buen momento para excluir el archivo **AuthConfig. ts** del control de código fuente para evitar la pérdida inadvertida del identificador de la aplicación.

## <a name="implement-sign-in"></a>Implementar el inicio de sesión

En esta sección, creará una clase auxiliar de autenticación y actualizará la aplicación para iniciar sesión y cerrar sesión.

1. Cree un nuevo archivo en el directorio **GraphTutorial/auth** denominado **AuthManager. ts**. Agregue el siguiente código al archivo.

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. Abra el archivo **GraphTutorial/app. TSX** y agregue la siguiente `import` instrucción en la parte superior del archivo.

    ```typescript
    import { AuthManager } from './auth/AuthManager';
    ```

1. Reemplace la `authContext` declaración existente por lo siguiente.

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AuthContextSnippet" highlight="4-6,9":::

1. Abra el archivo **GraphTutorial/menus/DrawerMenu. TSX** y agregue la siguiente `import` instrucción en la parte superior del archivo.

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Agregue el siguiente código a la `componentDidMount` función.

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

1. Guarde los cambios y vuelva a cargar la aplicación en el emulador.

Si inicia sesión en la aplicación, debería ver un token de acceso que se muestra en la pantalla de **bienvenida** .

## <a name="get-user-details"></a>Obtener detalles del usuario

En esta sección, creará un proveedor de autenticación personalizado para la biblioteca cliente de Graph, creará una clase auxiliar que contendrá todas las llamadas a Microsoft Graph y actualizará la `DrawerMenuContent` clase para que use esta nueva clase para obtener el usuario que ha iniciado sesión.

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **Graph**.
1. Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphAuthProvider. ts**. Agregue el siguiente código al archivo.

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphManager. ts**. Agregue el siguiente código al archivo.

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

1. Abra el archivo **GraphTutorial/views/DrawerMenu. TSX** y agregue la siguiente `import` instrucción a la parte superior del archivo.

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Reemplace el `componentDidMount` método por lo siguiente.

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

Si guarda los cambios y vuelve a cargar la aplicación ahora, después de iniciar sesión, la interfaz de usuario se actualizará con el nombre para mostrar y la dirección de correo electrónico del usuario.
