<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ef239-101">En este ejercicio crearás una nueva aplicación nativa de Azure AD con el Centro de administración de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef239-101">In this exercise you will create a new Azure AD native application using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="ef239-102">Abra un explorador y vaya al [centro de administración de Azure Active Directory](https://aad.portal.azure.com) e inicie sesión con una **cuenta personal** (también conocida como: cuenta Microsoft) o una **cuenta profesional o educativa**.</span><span class="sxs-lookup"><span data-stu-id="ef239-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="ef239-103">Seleccione **Azure Active Directory** en el panel de navegación izquierdo y, a continuación, seleccione **Registros de aplicaciones** en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="ef239-103">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="ef239-104">Captura de pantalla de los registros de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef239-104">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="ef239-105">Seleccione **Nuevo registro**.</span><span class="sxs-lookup"><span data-stu-id="ef239-105">Select **New registration**.</span></span> <span data-ttu-id="ef239-106">En la página **Registrar una aplicación**, establezca los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="ef239-106">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="ef239-107">Establezca **Nombre** como `React Native Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="ef239-107">Set **Name** to `React Native Graph Tutorial`.</span></span>
    - <span data-ttu-id="ef239-108">Establezca **Tipos de cuenta admitidos** en **Cuentas en cualquier directorio de organización y cuentas personales de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ef239-108">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="ef239-109">En **URI de** redireccionamiento, cambie el desplegable a Cliente público **(móvil & escritorio)** y establezca el valor en `graph-tutorial://react-native-auth/` .</span><span class="sxs-lookup"><span data-stu-id="ef239-109">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `graph-tutorial://react-native-auth/`.</span></span>

    ![Captura de pantalla de la página Registrar una aplicación](./images/aad-register-an-app.png)

1. <span data-ttu-id="ef239-111">Seleccione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="ef239-111">Select **Register**.</span></span> <span data-ttu-id="ef239-112">En la **página Tutorial de React Native Graph,** copie el valor del identificador de aplicación **(cliente)** y guárdelo, lo necesitará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="ef239-112">On the **React Native Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Captura de pantalla del identificador de aplicación del nuevo registro de la aplicación](./images/aad-application-id.png)
