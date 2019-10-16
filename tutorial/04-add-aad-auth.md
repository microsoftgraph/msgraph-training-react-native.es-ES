<!-- markdownlint-disable MD002 MD041 -->

En este ejercicio, ampliará la aplicación del ejercicio anterior para admitir la autenticación con Azure AD. Esto es necesario para obtener el token de acceso de OAuth necesario para llamar a Microsoft Graph. Para ello, integrará la biblioteca de [reAct-Native-App-auth](https://github.com/FormidableLabs/react-native-app-auth) en la aplicación.

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **auth**.
1. Cree un archivo nuevo en el directorio **GraphTutorial/auth** denominado **AuthConfig. js**. Agregue el siguiente código al archivo.

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

    Reemplace `YOUR_APP_ID_HERE` por el identificador de la aplicación del registro de la aplicación.

> [!IMPORTANT]
> Si usa un control de código fuente como GIT, ahora sería un buen momento para excluir el archivo **AuthConfig. js** del control de código fuente para evitar la pérdida inadvertida del identificador de la aplicación.

## <a name="implement-sign-in"></a>Implementar el inicio de sesión

En esta sección, creará una clase auxiliar de autenticación y actualizará la aplicación para iniciar sesión y cerrar sesión.

1. Cree un archivo nuevo en el directorio **GraphTutorial/auth** denominado **AuthManager. js**. Agregue el siguiente código al archivo.

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

1. Abra el archivo **GraphTutorial/views/SignInScreen. js** y agregue la `import` siguiente instrucción a la parte superior del archivo.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. Reemplace el método `_signInAsync` existente por lo siguiente.

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

1. Agregue el método siguiente a la clase `HomeScreen`.

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

1. Abra el archivo **GraphTutorial/menus/DrawerMenu. js** y agregue la `import` siguiente instrucción a la parte superior del archivo.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. En `_onItemPressed`, reemplace la `// TEMPORARY` línea con la siguiente.

    ```js
    await AuthManager.signOutAsync();
    ```

1. Guarde los cambios y vuelva a cargar la aplicación en el emulador.

Si inicia sesión en la aplicación, debería ver un token de acceso que se muestra en la pantalla de **bienvenida** .

## <a name="get-user-details"></a>Obtener detalles del usuario

En esta sección, creará un proveedor de autenticación personalizado para la biblioteca cliente de Graph, creará una clase auxiliar que contendrá todas las llamadas a Microsoft Graph y `HomeScreen` actualizará las clases y `DrawerMenuContent` para que usen esta nueva clase para obtener el usuario que ha iniciado sesión.

1. Cree un nuevo directorio en el directorio **GraphTutorial** denominado **Graph**.
1. Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphAuthProvider. js**. Agregue el siguiente código al archivo.

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

1. Cree un archivo nuevo en el directorio **GraphTutorial/Graph** denominado **GraphManager. js**. Agregue el siguiente código al archivo.

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

1. Abra el archivo **GraphTutorial/views/HomeScreen. js** y agregue la `import` siguiente instrucción a la parte superior del archivo.

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Reemplace el `componentDidMount` método por lo siguiente.

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

1. Abra el archivo **GraphTutorial/views/DrawerMenu. js** y agregue la `import` siguiente instrucción a la parte superior del archivo.

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. Agregue el método `componentDidMount` siguiente a la `DrawerMenuContent` clase.

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

Si guarda los cambios y vuelve a cargar la aplicación ahora, después de iniciar sesión, la interfaz de usuario se actualizará con el nombre para mostrar y la dirección de correo electrónico del usuario.
