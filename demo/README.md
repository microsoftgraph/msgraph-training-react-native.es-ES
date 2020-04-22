# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="f8fcb-101">Cómo ejecutar el proyecto completado</span><span class="sxs-lookup"><span data-stu-id="f8fcb-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8fcb-102">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f8fcb-102">Prerequisites</span></span>

<span data-ttu-id="f8fcb-103">Para ejecutar el proyecto completado en esta carpeta, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8fcb-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="f8fcb-104">Al menos uno de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f8fcb-104">At least one of the following:</span></span>
  - <span data-ttu-id="f8fcb-105">Kit de desarrollo de [Android Studio](https://developer.android.com/studio/) **y** [Java](https://jdk.java.net) (necesario para ejecutar el ejemplo en Android)</span><span class="sxs-lookup"><span data-stu-id="f8fcb-105">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="f8fcb-106">[Xcode](https://developer.apple.com/xcode/) (necesario para ejecutar el ejemplo en iOS)</span><span class="sxs-lookup"><span data-stu-id="f8fcb-106">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="f8fcb-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f8fcb-107">Node.js</span></span>](https://nodejs.org)
- <span data-ttu-id="f8fcb-108">Una cuenta de Microsoft personal con un buzón de correo en Outlook.com o una cuenta profesional o educativa de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

> <span data-ttu-id="f8fcb-109">**Nota:** Este tutorial se ha escrito con reaccionar la CLI nativa, que tiene requisitos previos específicos según el sistema operativo y las plataformas de destino.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-109">**Note:** This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="f8fcb-110">Consulte [reaccionar nativo de introducción](https://facebook.github.io/react-native/docs/getting-started) para obtener instrucciones sobre cómo configurar el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="f8fcb-111">A continuación se enumeran las versiones usadas para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="f8fcb-112">Los pasos de esta guía pueden funcionar con otras versiones, pero no se han probado.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="f8fcb-113">Android Studio versión 3.6.2 con el SDK de Android 9,0</span><span class="sxs-lookup"><span data-stu-id="f8fcb-113">Android Studio version 3.6.2 with the Android 9.0 SDK</span></span>
> - <span data-ttu-id="f8fcb-114">Kit de desarrollo de Java versión 12.0.2</span><span class="sxs-lookup"><span data-stu-id="f8fcb-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="f8fcb-115">Versión 11,4 de Xcode</span><span class="sxs-lookup"><span data-stu-id="f8fcb-115">Xcode version 11.4</span></span>
> - <span data-ttu-id="f8fcb-116">Node. js versión 12.16.2</span><span class="sxs-lookup"><span data-stu-id="f8fcb-116">Node.js version 12.16.2</span></span>

<span data-ttu-id="f8fcb-117">Si no tiene una cuenta de Microsoft, hay un par de opciones para obtener una cuenta gratuita:</span><span class="sxs-lookup"><span data-stu-id="f8fcb-117">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="f8fcb-118">Puede [registrarse para obtener una nueva cuenta Microsoft personal](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="f8fcb-118">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="f8fcb-119">Puede [registrarse para el programa de desarrolladores de office 365](https://developer.microsoft.com/office/dev-program) para obtener una suscripción gratuita a Office 365.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-119">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-an-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="f8fcb-120">Registrar una aplicación con el centro de administración de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8fcb-120">Register an application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="f8fcb-121">Abra un explorador y vaya al [centro de administración de Azure Active Directory](https://aad.portal.azure.com) e inicie sesión con una **cuenta personal** (también conocida como: cuenta Microsoft) o una **cuenta profesional o educativa**.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-121">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="f8fcb-122">Seleccione **Azure Active Directory** en el panel de navegación de la izquierda y, después, seleccione **registros de aplicaciones** en **administrar**.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-122">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="f8fcb-123">Una captura de pantalla de los registros de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f8fcb-123">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="f8fcb-124">Seleccione **Nuevo registro**.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-124">Select **New registration**.</span></span> <span data-ttu-id="f8fcb-125">En la página **Registrar una aplicación**, establezca los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-125">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="f8fcb-126">Establezca **Nombre** como `React Native Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-126">Set **Name** to `React Native Graph Tutorial`.</span></span>
    - <span data-ttu-id="f8fcb-127">Establezca **Tipos de cuenta admitidos** en **Cuentas en cualquier directorio de organización y cuentas personales de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-127">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="f8fcb-128">En **URI de redireccionamiento**, cambie la lista desplegable a **cliente público (móvil & escritorio)** y establezca `graph-tutorial://react-native-auth`el valor en.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-128">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `graph-tutorial://react-native-auth`.</span></span>

    ![Captura de pantalla de la página registrar una aplicación](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="f8fcb-130">Seleccione **registrar**.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-130">Select **Register**.</span></span> <span data-ttu-id="f8fcb-131">En la página de **tutorial de reAct de gráficos nativos** , copie el valor del identificador de la **aplicación (cliente)** y guárdelo, lo necesitará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-131">On the **React Native Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Captura de pantalla del identificador de la aplicación del nuevo registro de la aplicación](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="f8fcb-133">En **administrar**, seleccione **autenticación**.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-133">Under **Manage**, select **Authentication**.</span></span> <span data-ttu-id="f8fcb-134">En la página **URI de redireccionamiento** , agregue otro URI de redireccionamiento de tipo **cliente público (móvil & escritorio)**, con el URI `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-134">On the **Redirect URIs** page, add another redirect URI of type **Public client (mobile & desktop)**, with the URI `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="f8fcb-135">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-135">Select **Save**.</span></span>

    ![Captura de pantalla de la página URI de redireccionamiento](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a><span data-ttu-id="f8fcb-137">Configuración del ejemplo</span><span class="sxs-lookup"><span data-stu-id="f8fcb-137">Configure the sample</span></span>

1. <span data-ttu-id="f8fcb-138">Cambie el nombre del archivo **GraphTutorial/auth/AuthConfig. TS. example** a **AuthConfig. ts**.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-138">Rename the **GraphTutorial/auth/AuthConfig.ts.example** file to **AuthConfig.ts**.</span></span>
1. <span data-ttu-id="f8fcb-139">Edite el archivo **AuthConfig. ts** y realice los siguientes cambios.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-139">Edit the **AuthConfig.ts** file and make the following changes.</span></span>
    1. <span data-ttu-id="f8fcb-140">Reemplace `YOUR_APP_ID_HERE` por el **identificador de aplicación** que obtuvo desde el portal de registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-140">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>

1. <span data-ttu-id="f8fcb-141">En la interfaz de línea de comandos (CLI), navegue al directorio **GraphTutorial** y ejecute el siguiente comando para instalar los requisitos.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-141">In your command-line interface (CLI), navigate to the **GraphTutorial** directory and run the following command to install requirements.</span></span>

    ```Shell
    npm install
    ```

1. <span data-ttu-id="f8fcb-142">En la interfaz de línea de comandos (CLI), navegue al directorio **GraphTutorial/iOS** y ejecute el siguiente comando para instalar los requisitos.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-142">In your command-line interface (CLI), navigate to the **GraphTutorial/ios** directory and run the following command to install requirements.</span></span>

    ```Shell
    pod install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="f8fcb-143">Ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="f8fcb-143">Run the sample</span></span>

### <a name="run-on-ios-simulator"></a><span data-ttu-id="f8fcb-144">Ejecutar en simulador de iOS</span><span class="sxs-lookup"><span data-stu-id="f8fcb-144">Run on iOS Simulator</span></span>

<span data-ttu-id="f8fcb-145">Ejecute el siguiente comando en su CLI para iniciar la aplicación en un simulador de iOS.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-145">Run the following command in your CLI to start the application in an iOS Simulator.</span></span>

```Shell
react-native run-ios
```

### <a name="run-on-android-emulator"></a><span data-ttu-id="f8fcb-146">Ejecutar en un emulador de Android</span><span class="sxs-lookup"><span data-stu-id="f8fcb-146">Run on Android emulator</span></span>

<span data-ttu-id="f8fcb-147">Inicie la instancia del emulador de Android y ejecute el siguiente comando en la CLI para iniciar la aplicación en un emulador de Android.</span><span class="sxs-lookup"><span data-stu-id="f8fcb-147">Launch and Android emulator instance and run the following command in your CLI to start the application in an Android emulator.</span></span>

```Shell
react-native run-android
```
