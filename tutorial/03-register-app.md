<!-- markdownlint-disable MD002 MD041 -->

En este ejercicio crearás una nueva aplicación nativa de Azure AD con el Centro de administración de Azure Active Directory.

1. Abra un explorador y vaya al [centro de administración de Azure Active Directory](https://aad.portal.azure.com) e inicie sesión con una **cuenta personal** (también conocida como: cuenta Microsoft) o una **cuenta profesional o educativa**.

1. Seleccione **Azure Active Directory** en el panel de navegación izquierdo y, a continuación, seleccione **Registros de aplicaciones** en **Administrar**.

    ![Captura de pantalla de los registros de aplicaciones ](./images/aad-portal-app-registrations.png)

1. Seleccione **Nuevo registro**. En la página **Registrar una aplicación**, establezca los valores siguientes.

    - Establezca **Nombre** como `React Native Graph Tutorial`.
    - Establezca **Tipos de cuenta admitidos** en **Cuentas en cualquier directorio de organización y cuentas personales de Microsoft**.
    - En **URI de** redireccionamiento, cambie el desplegable a Cliente público **(móvil & escritorio)** y establezca el valor en `graph-tutorial://react-native-auth/` .

    ![Captura de pantalla de la página Registrar una aplicación](./images/aad-register-an-app.png)

1. Seleccione **Registrar**. En la **página Tutorial de React Native Graph,** copie el valor del identificador de aplicación **(cliente)** y guárdelo, lo necesitará en el paso siguiente.

    ![Captura de pantalla del identificador de aplicación del nuevo registro de la aplicación](./images/aad-application-id.png)
