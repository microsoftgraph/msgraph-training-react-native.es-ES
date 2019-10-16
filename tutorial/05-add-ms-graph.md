<!-- markdownlint-disable MD002 MD041 -->

En este ejercicio, incorporará Microsoft Graph a la aplicación. Para esta aplicación, usará la [biblioteca cliente de JavaScript de Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) para realizar llamadas a Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Obtener eventos de calendario de Outlook

En esta sección, ampliará la `GraphManager` clase para agregar una función para obtener los eventos del usuario y actualizar `CalendarScreen` para usar estas funciones nuevas.

1. Abra el archivo **GraphTutorial/Graph/GraphManager. js** y agregue el siguiente método a la `GraphManager` clase.

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
    > Tenga en cuenta lo que `getEvents` hace el código.
    >
    > - La dirección URL a la que se `/v1.0/me/events`llamará es.
    > - La `select` función limita los campos devueltos para cada evento a solo aquellos que la aplicación usará realmente.
    > - La `orderby` función ordena los resultados por la fecha y hora en que se crearon, con el elemento más reciente en primer lugar.

1. Abra el **GraphTutorial/views/CalendarScreen. js** y reemplace todo su contenido por el siguiente código.

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

Ahora puede ejecutar la aplicación, iniciar sesión y puntear en el elemento de navegación **calendario** del menú. Debería ver un volcado JSON de los eventos en la aplicación.

## <a name="display-the-results"></a>Mostrar los resultados

Ahora puede reemplazar el volcado de JSON con algo para mostrar los resultados de forma fácil de uso. En esta sección, se agregará una `FlatList` a la pantalla de calendario para representar los eventos.

1. Abra el archivo **GraphTutorial/Graph/GraphManager. js** y agregue la siguiente `import` instrucción a la parte superior del archivo.

    ```js
    import moment from 'moment';
    ```

1. Agregue el siguiente método **encima** de `CalendarScreen` la declaración de clase.

    ```js
    convertDateTime = (dateTime) => {
      const utcTime = moment.utc(dateTime);
      return utcTime.local().format('MMM Do H:mm a');
    };
    ```

1. Reemplace el `ScrollView` en el `render` método por lo siguiente.

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

1. Ejecute la aplicación, inicie sesión y pulse el elemento de navegación **calendario** . Debe ver la lista de eventos.

    ![Captura de pantalla de la tabla de eventos](./images/calendar-list.png)
