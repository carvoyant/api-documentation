EventNotification
=================

The EventNotification object corresponds to a unique :doc:`event-subscription` within the Carvoyant system. The EventNotification will be delivered to the postURL provided by the :doc:`event-subscription` via an HTTP POST message whose JSON body contains the details specific to the notification type. Examples for the supported event types can be found in this documents children.

The Event model that we have implemented is based off of the `Evented API Spec <http://www.eventedapi.org/>`_. This is a generic specification that helps define the transport of API events between two systems.

See the :doc:`../data-type/event-type` page for details on the different events that can be notified.

.. note::
   You will only be able to get notifications that have been created for your client Id.  Specifically, we will look at the access token
   specified in the request, determine the client Id that was authorized with that access token, and only return notifications for :doc:`event-subscription` s
   for that client Id.  You do not have access to notifications for subscriptions that have been created by other client Ids.

*Common Properties*

+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Property           | Type                                    | Description                                                                                                                                                                                                                                                                                                                              |
+====================+=========================================+==========================================================================================================================================================================================================================================================================================================================================+
| id                 | Integer                                 | The internal system identifier for this notification.                                                                                                                                                                                                                                                                                    |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| accountId          | Integer                                 | The internal system identifier for this account.                                                                                                                                                                                                                                                                                         |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| vehicleId          | Integer                                 | The internal system identifier for this vehicle.                                                                                                                                                                                                                                                                                         |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| dataSetId          | Integer                                 | The Id of the :doc:`data-set` that generated the notification.                                                                                                                                                                                                                                                                           |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| tripId             | Integer                                 | The Id of the :doc:`trip` that generated the notification.                                                                                                                                                                                                                                                                               |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| subscriptionId     | Integer                                 | The internal system identifier for this notification's corresponding EventSubscription.                                                                                                                                                                                                                                                  |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| _domain            | String                                  | Serves as a namespace for the event.                                                                                                                                                                                                                                                                                                     |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| _type              | :doc:`../data-type/event-type`          | The type of event notification being sent.                                                                                                                                                                                                                                                                                               |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| _name              | :doc:`../data-type/event-type`          | The type of event notification being sent. Note that this field should be considered deprecated. It is only supported because the Evented API spec has not fully implemented the change.                                                                                                                                                 |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| _timestamp         | :doc:`../data-type/date-time`           | The time when the event occurred.                                                                                                                                                                                                                                                                                                        |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| eventTimestamp     | :doc:`../data-type/date-time`           | The time when the event notification was created.                                                                                                                                                                                                                                                                                        |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| minimumTime        | Integer                                 | The time in minutes that will determine the minimum interval between event notification creation. If the value is less than the reporting interval of the hardware, the hardware limit will be used.                                                                                                                                     |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| httpStatusCode     | Integer                                 | The status code that was returned when attempting to POST the EventNotification to the postUrl. When the EventNotification is delivered to the postUrl the value of httpStatusCode will be 0. However, a subsequent GET request on the EventNotification will provide a useful httpStatusCode value derived from the postUrl's response. |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| notificationPeriod | :doc:`../data-type/notification-period` | A string that represents when EventNotifications are sent from the Carvoyant system. Each EventType will define what periods are supported.                                                                                                                                                                                              |
+--------------------+-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

*Supported Verbs*

   * GET

GET
---

Returns one or more event notifications.  By default, the first 50 results are returned.

*Query Paths*

   * /account/{account-id}/eventNotification/{notification-id}
   * /account/{account-id}/eventNotification/{event-type}/{notification-id}
   * /account/{account-id}/eventSubscription/{subscription-id}/eventNotification/{notification-id}
   * /account/{account-id}/eventSubscription/{subscription-id}/eventNotification/{event-type}/{notification-id}
   * /vehicle/{vehicle-id}/eventNotification/{notification-id}
   * /vehicle/{vehicle-id}/eventNotification/{event-type}/{notification-id}
   * /vehicle/{vehicle-id}/eventSubscription/{subscription-id}/eventNotification/{notification-id}
   * /vehicle/{vehicle-id}/eventSubscription/{subscription-id}/eventNotification/{event-type}/{notification-id}

*Query Parameters*

   +-----------------+----------------------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                                              |
   +=================+==========================================================================================================+
   | account-id      | The Carvoyant identifier of the account. This is used for account level notification                     |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | vehicle-id      | The Carvoyant identifier of the vehicle. This could be the device serial number in the car (for example, |
   |                 | C201200001) or it could be the internal id returned from a previous lookup. This is used for vehicle     |
   |                 | level notification                                                                                       |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | notification-id | The Carvoyant identifier of the notification. If the notification-id is not                              |
   |                 | specified, then all notifications available will be returned.                                            |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | subscription-id | The Carvoyant identifier of the subscription.                                                            |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | event-type      | Indicates the :doc:`../data-type/event-type` of notifications to be returned.                            |
   +-----------------+----------------------------------------------------------------------------------------------------------+

*Call Options*

   +----------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Sortable | :doc:`Yes </api-overview/sorting-and-paging>` (by timestamp)                                                                             |
   +----------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Pageable | :doc:`Yes </api-overview/sorting-and-paging>` (when no notification-id is specified. Individual notification requests are not paginated) |
   +----------+------------------------------------------------------------------------------------------------------------------------------------------+

*Sample JSON Response*

.. note::
   This response only includes the properties that are common to all :doc:`../data-type/event-type` . It is not a complete response.  Refer to the :doc:`../data-type/event-type`
   page for the detailed list of what properties are returned for the notification.

::

   {
      "notifications":[
         {
            "id":315931,
            "subscriptionId":1647,
            "_domain":"carvoyant.com",
            "_type":"VEHICLEDISCONNECTED",
            "_name":"VEHICLEDISCONNECTED",
            "_timestamp":"20140912T010246+0000",
            "minimumTime":0,
            "httpStatusCode":200,
            "notificationPeriod":"INITIALSTATE",
            "dataSetId":4795420,
            "creatorClientId":"hasa2czfebhsj6XXXXXXXXXX",
            "vehicleId":123
         },
         {
            "id":315932,
            "subscriptionId":1646,
            "_domain":"carvoyant.com",
            "_type":"VEHICLECONNECTED",
            "_name":"VEHICLECONNECTED",
            "_timestamp":"20140912T010303+0000",
            "minimumTime":0,
            "httpStatusCode":200,
            "notificationPeriod":"INITIALSTATE",
            "dataSetId":4795435,
            "creatorClientId":"hasa2czfebhsj6XXXXXXXXXX",
            "vehicleId":123
         }
      ],
      "totalRecords":2
   }
