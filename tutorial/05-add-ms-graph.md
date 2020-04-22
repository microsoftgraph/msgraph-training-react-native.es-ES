<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="846d8-101">En este ejercicio, incorporará Microsoft Graph a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="846d8-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="846d8-102">Para esta aplicación, usará la [biblioteca cliente de JavaScript de Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="846d8-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="846d8-103">Obtener eventos de calendario de Outlook</span><span class="sxs-lookup"><span data-stu-id="846d8-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="846d8-104">En esta sección, ampliará la `GraphManager` clase para agregar una función para obtener los eventos del usuario y actualizar `CalendarScreen` para usar estas funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="846d8-104">In this section you will extend the `GraphManager` class to add a function to get the user's events and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="846d8-105">Abra el archivo **GraphTutorial/Graph/GraphManager. TSX** y agregue el método siguiente a la `GraphManager` clase.</span><span class="sxs-lookup"><span data-stu-id="846d8-105">Open the **GraphTutorial/graph/GraphManager.tsx** file and add the following method to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetEventsSnippet":::

    > [!NOTE]
    > <span data-ttu-id="846d8-106">Tenga en cuenta lo que `getEvents` hace el código.</span><span class="sxs-lookup"><span data-stu-id="846d8-106">Consider what the code in `getEvents` is doing.</span></span>
    >
    > - <span data-ttu-id="846d8-107">La dirección URL a la que se `/v1.0/me/events`llamará es.</span><span class="sxs-lookup"><span data-stu-id="846d8-107">The URL that will be called is `/v1.0/me/events`.</span></span>
    > - <span data-ttu-id="846d8-108">La `select` función limita los campos devueltos para cada evento a solo aquellos que la aplicación usará realmente.</span><span class="sxs-lookup"><span data-stu-id="846d8-108">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="846d8-109">La `orderby` función ordena los resultados por la fecha y hora en que se crearon, con el elemento más reciente en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="846d8-109">The `orderby` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="846d8-110">Abra el **GraphTutorial/views/CalendarScreen. TSX** y reemplace todo su contenido por el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="846d8-110">Open the **GraphTutorial/views/CalendarScreen.tsx** and replace its entire contents with the following code.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      FlatList,
      Modal,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';
    import { GraphManager } from '../graph/GraphManager';

    const Stack = createStackNavigator();
    const initialState: CalendarScreenState = { loadingEvents: true, events: []};
    const CalendarState = React.createContext(initialState);

    type CalendarScreenState = {
      loadingEvents: boolean;
      events: any[];
    }

    // Temporary JSON view
    const CalendarComponent = () => {
      const calendarState = React.useContext(CalendarState);

      return (
        <View style={styles.container}>
          <Modal visible={calendarState.loadingEvents}>
            <View style={styles.loading}>
              <ActivityIndicator animating={calendarState.loadingEvents} size='large' />
            </View>
          </Modal>
          <ScrollView>
            <Text>{JSON.stringify(calendarState.events, null, 2)}</Text>
          </ScrollView>
        </View>
      );
    }

    export default class CalendarScreen extends React.Component {

      state: CalendarScreenState = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const events = await GraphManager.getEvents();

          this.setState({
            loadingEvents: false,
            events: events.value
          });
        } catch(error) {
          Alert.alert(
            'Error getting events',
            JSON.stringify(error),
            [
              {
                text: 'OK'
              }
            ],
            { cancelable: false }
          );
        }
      }

      render() {
        return (
          <CalendarState.Provider value={this.state}>
            <Stack.Navigator screenOptions={ headerOptions }>
              <Stack.Screen name='Calendar'
                component={ CalendarComponent }
                options={{
                  title: 'Calendar',
                  headerLeft: () => <DrawerToggle/>
                }} />
            </Stack.Navigator>
          </CalendarState.Provider>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      loading: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center'
      },
      eventItem: {
        padding: 10
      },
      eventSubject: {
        fontWeight: '700',
        fontSize: 18
      },
      eventOrganizer: {
        fontWeight: '200'
      },
      eventDuration: {
        fontWeight: '200'
      }
    });
    ```

<span data-ttu-id="846d8-111">Ahora puede ejecutar la aplicación, iniciar sesión y puntear en el elemento de navegación **calendario** del menú.</span><span class="sxs-lookup"><span data-stu-id="846d8-111">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="846d8-112">Debería ver un volcado JSON de los eventos en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="846d8-112">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="846d8-113">Mostrar los resultados</span><span class="sxs-lookup"><span data-stu-id="846d8-113">Display the results</span></span>

<span data-ttu-id="846d8-114">Ahora puede reemplazar el volcado de JSON con algo para mostrar los resultados de forma fácil de uso.</span><span class="sxs-lookup"><span data-stu-id="846d8-114">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="846d8-115">En esta sección, se agregará una `FlatList` a la pantalla de calendario para representar los eventos.</span><span class="sxs-lookup"><span data-stu-id="846d8-115">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="846d8-116">Abra el archivo **GraphTutorial/Graph/Screens/CalendarScreen. TSX** y agregue la siguiente `import` instrucción en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="846d8-116">Open the **GraphTutorial/graph/screens/CalendarScreen.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import moment from 'moment';
    ```

1. <span data-ttu-id="846d8-117">Agregue el siguiente método **encima** de `CalendarScreen` la declaración de clase.</span><span class="sxs-lookup"><span data-stu-id="846d8-117">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. <span data-ttu-id="846d8-118">Reemplace el `ScrollView` en el `CalendarComponent` método por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="846d8-118">Replace the `ScrollView` in the `CalendarComponent` method with the following.</span></span>

    ```typescript
    <FlatList data={calendarState.events}
      renderItem={({item}) =>
        <View style={styles.eventItem}>
          <Text style={styles.eventSubject}>{item.subject}</Text>
          <Text style={styles.eventOrganizer}>{item.organizer.emailAddress.name}</Text>
          <Text style={styles.eventDuration}>
            {convertDateTime(item.start.dateTime)} - {convertDateTime(item.end.dateTime)}
          </Text>
        </View>
      } />
    ```

1. <span data-ttu-id="846d8-119">Ejecute la aplicación, inicie sesión y pulse el elemento de navegación **calendario** .</span><span class="sxs-lookup"><span data-stu-id="846d8-119">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="846d8-120">Debe ver la lista de eventos.</span><span class="sxs-lookup"><span data-stu-id="846d8-120">You should see the list of events.</span></span>

    ![Captura de pantalla de la tabla de eventos](./images/calendar-list.png)
