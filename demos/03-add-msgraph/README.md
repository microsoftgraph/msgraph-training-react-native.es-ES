# <a name="how-to-run-the-completed-project"></a>Cómo ejecutar el proyecto completado

## <a name="prerequisites"></a>Requisitos previos

Para ejecutar el proyecto completado en esta carpeta, necesita lo siguiente:

- Al menos uno de los siguientes elementos:
  - Kit de desarrollo de [Android Studio](https://developer.android.com/studio/) **y** [Java](https://jdk.java.net) (necesario para ejecutar el ejemplo en Android)
  - [Xcode](https://developer.apple.com/xcode/) (necesario para ejecutar el ejemplo en iOS)
- [Node.js](https://nodejs.org)
- Una cuenta de Microsoft personal con un buzón de correo en Outlook.com o una cuenta profesional o educativa de Microsoft.

> **Nota:** Este tutorial se ha escrito con reaccionar la CLI nativa, que tiene requisitos previos específicos según el sistema operativo y las plataformas de destino. Consulte [reaccionar nativo de introducción](https://facebook.github.io/react-native/docs/getting-started) para obtener instrucciones sobre cómo configurar el equipo de desarrollo. A continuación se enumeran las versiones usadas para este tutorial. Los pasos de esta guía pueden funcionar con otras versiones, pero no se han probado.
>
> - Android Studio versión 3.4.2 con 1.8.0 JRE y el SDK de Android 9,0
> - Kit de desarrollo de Java versión 12.0.2
> - Versión 10,3 de Xcode
> - Node. js versión 10.16.0

Si no tiene una cuenta de Microsoft, hay un par de opciones para obtener una cuenta gratuita:

- Puede [registrarse para obtener una nueva cuenta Microsoft personal](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Puede [registrarse para el programa de desarrolladores de office 365](https://developer.microsoft.com/office/dev-program) para obtener una suscripción gratuita a Office 365.

## <a name="register-an-application-with-the-azure-active-directory-admin-center"></a>Registrar una aplicación con el centro de administración de Azure Active Directory

1. Abra un explorador y vaya al [centro de administración de Azure Active Directory](https://aad.portal.azure.com) e inicie sesión con una **cuenta personal** (también conocida como: cuenta Microsoft) o una **cuenta profesional o educativa**.

1. Seleccione **Azure Active Directory** en el panel de navegación de la izquierda y, después, seleccione **registros de aplicaciones** en **administrar**.

    ![Una captura de pantalla de los registros de la aplicación ](/tutorial/images/aad-portal-app-registrations.png)

1. Seleccione **Nuevo registro**. En la página **Registrar una aplicación**, establezca los valores siguientes.

    - Establezca **Nombre** como `React Native Graph Tutorial`.
    - Establezca **Tipos de cuenta admitidos** en **Cuentas en cualquier directorio de organización y cuentas personales de Microsoft**.
    - En **URI de redireccionamiento**, cambie la lista desplegable a **cliente público (móvil & escritorio)** y establezca `graph-tutorial://react-native-auth`el valor en.

    ![Captura de pantalla de la página registrar una aplicación](/tutorial/images/aad-register-an-app.png)

1. Seleccione **registrar**. En la página de **tutorial de reAct de gráficos nativos** , copie el valor del identificador de la **aplicación (cliente)** y guárdelo, lo necesitará en el paso siguiente.

    ![Captura de pantalla del identificador de la aplicación del nuevo registro de la aplicación](/tutorial/images/aad-application-id.png)

1. En **administrar**, seleccione **autenticación**. En la página **URI de redireccionamiento** , agregue otro URI de redireccionamiento de tipo **cliente público (móvil & escritorio)**, con el URI `urn:ietf:wg:oauth:2.0:oob`. Haga clic en **Guardar**.

    ![Captura de pantalla de la página URI de redireccionamiento](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a>Configuración del ejemplo

1. Cambie el nombre del archivo **GraphTutorial/auth/AuthConfig. js. example** a **AuthConfig. js**.
1. Edite el archivo **AuthConfig. js** y realice los siguientes cambios.
    1. Reemplace `YOUR_APP_ID_HERE` por el **identificador de aplicación** que obtuvo desde el portal de registro de aplicaciones.

1. En la interfaz de línea de comandos (CLI), navegue al directorio **GraphTutorial** y ejecute el siguiente comando para instalar los requisitos.

    ```Shell
    npm install
    ```

## <a name="run-the-sample"></a>Ejecutar el ejemplo

### <a name="run-on-ios-simulator"></a>Ejecutar en simulador de iOS

Ejecute el siguiente comando en su CLI para iniciar la aplicación en un simulador de iOS.

```Shell
react-native run-ios
```

### <a name="run-on-android-emulator"></a>Ejecutar en un emulador de Android

Inicie la instancia del emulador de Android y ejecute el siguiente comando en la CLI para iniciar la aplicación en un emulador de Android.

```Shell
react-native run-android
```
