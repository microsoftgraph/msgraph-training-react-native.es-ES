<!-- markdownlint-disable MD002 MD041 -->

Este tutorial le enseña a crear una aplicación nativa reAct que use la API de Microsoft Graph para recuperar la información de calendario de un usuario.

> [!TIP]
> Si prefiere descargar solo el tutorial completo, puede descargar o clonar el repositorio de [GitHub](https://github.com/microsoftgraph/msgraph-training-react-native).

## <a name="prerequisites"></a>Requisitos previos

Antes de iniciar este tutorial, debe tener instalado lo siguiente en el equipo de desarrollo.

- Al menos uno de los siguientes elementos:
  - Kit de desarrollo de [Android Studio](https://developer.android.com/studio/) **y** [Java](https://jdk.java.net) (necesario para ejecutar el ejemplo en Android)
  - [Xcode](https://developer.apple.com/xcode/) (necesario para ejecutar el ejemplo en iOS)
- [Node.js](https://nodejs.org)

También debe tener una cuenta de Microsoft personal con un buzón de correo en Outlook.com o una cuenta profesional o educativa de Microsoft. Si no tiene una cuenta de Microsoft, hay un par de opciones para obtener una cuenta gratuita:

- Puede [registrarse para obtener una nueva cuenta Microsoft personal](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Puede [registrarse para el programa de desarrolladores de office 365](https://developer.microsoft.com/office/dev-program) para obtener una suscripción gratuita a Office 365.

> [!NOTE]
> Este tutorial se ha escrito con reaccionar la CLI nativa, que tiene requisitos previos específicos según el sistema operativo y las plataformas de destino. Consulte [reaccionar nativo de introducción](https://reactnative.dev/docs/environment-setup) para obtener instrucciones sobre cómo configurar el equipo de desarrollo. A continuación se enumeran las versiones usadas para este tutorial. Los pasos de esta guía pueden funcionar con otras versiones, pero no se han probado.
>
> - Android Studio versión 3.6.2 con el SDK de Android 9,0
> - Kit de desarrollo de Java versión 12.0.2
> - Versión 11,4 de Xcode
> - Node. js versión 12.16.2

## <a name="feedback"></a>Comentarios

Envíe sus comentarios sobre este tutorial en el [repositorio de github](https://github.com/microsoftgraph/msgraph-training-react-native).
