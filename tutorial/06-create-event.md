<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="092df-101">En esta sección, agregará la capacidad de crear eventos en el calendario del usuario.</span><span class="sxs-lookup"><span data-stu-id="092df-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-the-new-event-screen"></a><span data-ttu-id="092df-102">Crear la nueva pantalla de eventos</span><span class="sxs-lookup"><span data-stu-id="092df-102">Create the new event screen</span></span>

1. <span data-ttu-id="092df-103">Abra **./Graph/GraphManager.ts** y agregue la siguiente función a la `GraphManager` clase.</span><span class="sxs-lookup"><span data-stu-id="092df-103">Open **./graph/GraphManager.ts** and add the following function to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="CreateEventSnippet":::

    <span data-ttu-id="092df-104">Esta función usa Graph SDK para crear un nuevo evento.</span><span class="sxs-lookup"><span data-stu-id="092df-104">This function uses the Graph SDK to create a new event.</span></span>

1. <span data-ttu-id="092df-105">Cree un nuevo archivo en el archivo **./Screens** denominado **NewEventScreen. TSX** y agregue el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="092df-105">Create a new file in the **./screens** named **NewEventScreen.tsx** and add the following code.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/NewEventScreen.tsx" id="NewEventScreenSnippet":::

    <span data-ttu-id="092df-106">Tenga en cuenta lo que `createEvent` hace la función.</span><span class="sxs-lookup"><span data-stu-id="092df-106">Consider what the `createEvent` function does.</span></span> <span data-ttu-id="092df-107">Crea un `MicrosoftGraph.Event` objeto con los valores del formulario y, a continuación, pasa ese objeto a la `GraphManager.createEvent` función.</span><span class="sxs-lookup"><span data-stu-id="092df-107">It creates a `MicrosoftGraph.Event` object using the values from the form, then passes that object to the `GraphManager.createEvent` function.</span></span>

1. <span data-ttu-id="092df-108">Abra **./menus/DrawerMenu.TSX** y agregue la siguiente `import` instrucción en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="092df-108">Open **./menus/DrawerMenu.tsx** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import NewEventScreen from '../screens/NewEventScreen';
    ```

1. <span data-ttu-id="092df-109">Agregue el siguiente código dentro del `<Drawer.Navigator>` elemento, justo encima de la `</Drawer.Navigator>` línea.</span><span class="sxs-lookup"><span data-stu-id="092df-109">Add the following code inside the `<Drawer.Navigator>` element, just above the `</Drawer.Navigator>` line.</span></span>

    ```typescript
    { userLoaded &&
      <Drawer.Screen name='NewEvent'
        component={NewEventScreen}
        options={{drawerLabel: 'New event'}} />
    }
    ```

1. <span data-ttu-id="092df-110">Guarde los cambios y reinicie o actualice la aplicación.</span><span class="sxs-lookup"><span data-stu-id="092df-110">Save your changes and restart or refresh the app.</span></span> <span data-ttu-id="092df-111">Seleccione la opción **nuevo evento** en el menú para ir al nuevo formulario de eventos.</span><span class="sxs-lookup"><span data-stu-id="092df-111">Select the **New event** option on the menu to get to the new event form.</span></span>

1. <span data-ttu-id="092df-112">Rellene el formulario y seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="092df-112">Fill in the form and select **Create**.</span></span>

    ![Captura de pantalla del nuevo formulario de eventos](images/new-event-form.png)
