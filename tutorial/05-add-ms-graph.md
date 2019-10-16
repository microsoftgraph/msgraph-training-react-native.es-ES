<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="54adf-101">En este ejercicio, incorporará Microsoft Graph a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54adf-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="54adf-102">Para esta aplicación, usará la [biblioteca cliente de JavaScript de Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="54adf-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="54adf-103">Obtener eventos de calendario de Outlook</span><span class="sxs-lookup"><span data-stu-id="54adf-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="54adf-104">En esta sección, ampliará la `GraphManager` clase para agregar una función para obtener los eventos del usuario y actualizar `CalendarScreen` para usar estas funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="54adf-104">In this section you will extend the `GraphManager` class to add a function to get the user's events and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="54adf-105">Abra el archivo **GraphTutorial/Graph/GraphManager. js** y agregue el siguiente método a la `GraphManager` clase.</span><span class="sxs-lookup"><span data-stu-id="54adf-105">Open the **GraphTutorial/graph/GraphManager.js** file and add the following method to the `GraphManager` class.</span></span>

    ```js
    static getEvents = async() => {
      // GET /me/events
      return graphClient.api('/me/events')
        // $select='subject,organizer,start,end'
        // Only return these fields in results
        .select('subject,organizer,start,end')
        // $orderby=createdDateTime DESC
        // Sort results by when they were created, newest first
        .orderby('createdDateTime DESC')
        .get();
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="54adf-106">Tenga en cuenta lo que `getEvents` hace el código.</span><span class="sxs-lookup"><span data-stu-id="54adf-106">Consider what the code in `getEvents` is doing.</span></span>
    >
    > - <span data-ttu-id="54adf-107">La dirección URL a la que se `/v1.0/me/events`llamará es.</span><span class="sxs-lookup"><span data-stu-id="54adf-107">The URL that will be called is `/v1.0/me/events`.</span></span>
    > - <span data-ttu-id="54adf-108">La `select` función limita los campos devueltos para cada evento a solo aquellos que la aplicación usará realmente.</span><span class="sxs-lookup"><span data-stu-id="54adf-108">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="54adf-109">La `orderby` función ordena los resultados por la fecha y hora en que se crearon, con el elemento más reciente en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="54adf-109">The `orderby` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="54adf-110">Abra el **GraphTutorial/views/CalendarScreen. js** y reemplace todo su contenido por el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="54adf-110">Open the **GraphTutorial/views/CalendarScreen.js** and replace its entire contents with the following code.</span></span>

    ```JSX
    import React from 'react';
    import {
      ActivityIndicator,
      FlatList,
      Modal,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';
    import { GraphManager } from '../graph/GraphManager';

    export default class CalendarScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Calendar',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      state = {
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
          alert(error);
        }
      }

      // Temporary JSON view
      render() {
        return (
          <View style={styles.container}>
            <Modal visible={this.state.loadingEvents}>
              <View style={styles.loading}>
                <ActivityIndicator animating={this.state.loadingEvents} size='large' />
              </View>
            </Modal>
            <ScrollView>
              <Text>{JSON.stringify(this.state.events, null, 2)}</Text>
            </ScrollView>
          </View>
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

<span data-ttu-id="54adf-111">Ahora puede ejecutar la aplicación, iniciar sesión y puntear en el elemento de navegación **calendario** del menú.</span><span class="sxs-lookup"><span data-stu-id="54adf-111">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="54adf-112">Debería ver un volcado JSON de los eventos en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54adf-112">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="54adf-113">Mostrar los resultados</span><span class="sxs-lookup"><span data-stu-id="54adf-113">Display the results</span></span>

<span data-ttu-id="54adf-114">Ahora puede reemplazar el volcado de JSON con algo para mostrar los resultados de forma fácil de uso.</span><span class="sxs-lookup"><span data-stu-id="54adf-114">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="54adf-115">En esta sección, se agregará una `FlatList` a la pantalla de calendario para representar los eventos.</span><span class="sxs-lookup"><span data-stu-id="54adf-115">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="54adf-116">Abra el archivo **GraphTutorial/Graph/GraphManager. js** y agregue la siguiente `import` instrucción a la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="54adf-116">Open the **GraphTutorial/graph/GraphManager.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import moment from 'moment';
    ```

1. <span data-ttu-id="54adf-117">Agregue el siguiente método **encima** de `CalendarScreen` la declaración de clase.</span><span class="sxs-lookup"><span data-stu-id="54adf-117">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    ```js
    convertDateTime = (dateTime) => {
      const utcTime = moment.utc(dateTime);
      return utcTime.local().format('MMM Do H:mm a');
    };
    ```

1. <span data-ttu-id="54adf-118">Reemplace el `ScrollView` en el `render` método por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="54adf-118">Replace the `ScrollView` in the `render` method with the following.</span></span>

    ```JSX
    <FlatList data={this.state.events}
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

1. <span data-ttu-id="54adf-119">Ejecute la aplicación, inicie sesión y pulse el elemento de navegación **calendario** .</span><span class="sxs-lookup"><span data-stu-id="54adf-119">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="54adf-120">Debe ver la lista de eventos.</span><span class="sxs-lookup"><span data-stu-id="54adf-120">You should see the list of events.</span></span>

    ![Captura de pantalla de la tabla de eventos](./images/calendar-list.png)
