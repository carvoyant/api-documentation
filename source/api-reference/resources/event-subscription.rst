EventSubscription
=================

The EventSubscription object represents a unique event subscription within the Carvoyant system. The user may subscribe to an event that will deliver an :doc:`event-notification` to the defined postURL when vehicle data has reached the specified criteria. In order to create an EventSubscription, all required fields for the specific event "_type" must be delivered in the body of the HTTP POST request. Required fields, resource URIs, and examples for the supported event types can be found in this documents children.

The Event model that we have implemented is based off of the `Evented API Spec <http://www.eventedapi.org/>`_. This is a generic specification that helps define the transport of API events between two systems.

See the :doc:`../data-type/event-type` page for details on the different events that can be subscribed to.

.. note::
   You will only be able to interact with subscriptions that have been created with your client Id.  Specifically, we will look at the access token
   specified in the request, determine the client Id that was authorized with that access token, and only return subscriptions for that client Id.
   You do not have access to subscriptions that have been created by other client Ids.

*Common Properties*

+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| Property           | Type                                    | Description                                                                                                 | Required for Creation |
+====================+=========================================+=============================================================================================================+=======================+
| id                 | Integer                                 | The internal system identifier for this subscription.                                                       | Unsupported           |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| _type              | :doc:`../data-type/event-type`          | The type of event being subscribed to. (In this case the _type is "LOWBATTERY")                             | Unsupported           |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| creationTimestamp  | :doc:`../data-type/date-time`           | The time when the subscription was created.                                                                 | Unsupported           |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| deletionTimestamp  | :doc:`../data-type/date-time`           | The time when the subscription was marked for deletion. (This value will only be returned if the event has  | Unsupported           |
|                    |                                         | been marked for deletion)                                                                                   |                       |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| minimumTime        | Integer                                 | The time in minutes that will determine the minimum interval between event notification creation. If the    | Required              |
|                    |                                         | value is less than the reporting interval of the hardware, the hardware limit will be used.                 |                       |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| creatorClientId    | String                                  | The client Id that generated this subscription.                                                             | Unsupported           |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| postUrl            | String                                  | The URL that will receive HTTPS POST notifications from the newly generated subscription. Note that only    | Required              |
|                    |                                         | HTTPS endpoints are supported. The certificate protecting the post URL must be a valid signed certificate.  |                       |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| postHeaders        | Map                                     | A map that contains any headers that should be sent to the postUrl when a notification is generated.        | Optional              |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+
| notificationPeriod | :doc:`../data-type/notification-period` | A string that represents when EventNotifications are sent from the Carvoyant system. All NotificationPeriod | Required              |
|                    |                                         | types are supported for LowBattery subscriptions.                                                           |                       |
+--------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------------------+-----------------------+

*Supported Verbs*

   * GET
   * POST
   * DELETE

GET
---

Returns one or more event subscriptions.  By default, the first 50 results are returned.

*Query Paths*

   * /account/{account-id}/eventSubscription/{subscription-id}
   * /account/{account-id}/eventSubscription/{event-type}/{subscription-id}
   * /vehicle/{vehicle-id}/eventSubscription/{subscription-id}
   * /vehicle/{vehicle-id}/eventSubscription/{event-type}/{subscription-id}

*Query Parameters*

   +-----------------+----------------------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                                              |
   +=================+==========================================================================================================+
   | account-id      | The Carvoyant identifier of the account. This is used for account level subscriptions                    |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | vehicle-id      | The Carvoyant identifier of the vehicle. This could be the device serial number in the car (for example, |
   |                 | C201200001) or it could be the internal id returned from a previous lookup. This is used for vehicle     |
   |                 | level subscriptions                                                                                      |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | subscription-id | The Carvoyant identifier of the subscription. If the subscription-id is not                              |
   |                 | specified, then all subscriptions available will be returned.                                            |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | event-type      | Indicates the :doc:`../data-type/event-type` of subscriptions to be returned.                            |
   +-----------------+----------------------------------------------------------------------------------------------------------+

*Call Options*

   +----------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Sortable | :doc:`Yes </api-overview/sorting-and-paging>` (by timestamp)                                                                             |
   +----------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Pageable | :doc:`Yes </api-overview/sorting-and-paging>` (when no subscription-id is specified. Individual subscription requests are not paginated) |
   +----------+------------------------------------------------------------------------------------------------------------------------------------------+

*Sample JSON Response*::

   {
       "subscriptions": [{
           "id": 1645,
           "_type": "LOWBATTERY",
           "_timestamp": "20140911T203312+0000",
           "minimumTime": 0,
           "creatorClientId": "hasa2czfebhsj6XXXXXXXXXX",
           "vehicleId": 123,
           "postUrl": "https://test.carvoyant.com/notify",
           "postHeaders": {
               "Authorization": "Bearer asdfqwerzxcv",
               "X-Sample-Headers": "Some custom value"
           },
           "notificationPeriod": "STATECHANGE"
       }, {
           "id": 1646,
           "_type": "VEHICLECONNECTED",
           "_timestamp": "20140911T203348+0000",
           "minimumTime": 0,
           "creatorClientId": "hasa2czfebhsj6XXXXXXXXXX",
           "vehicleId": 123,
           "postUrl": "https://test.carvoyant.com/notify",
           "postHeaders": {},
           "notificationPeriod": "INITIALSTATE"
       }, {
           "id": 1647,
           "_type": "VEHICLEDISCONNECTED",
           "_timestamp": "20140911T203408+0000",
           "minimumTime": 0,
           "creatorClientId": "hasa2czfebhsj6XXXXXXXXXX",
           "vehicleId": 123,
           "postUrl": "https://test.carvoyant.com/notify",
           "postHeaders": {},
           "notificationPeriod": "INITIALSTATE"
       }],
       "totalRecords": 3
   }

POST
----

Creates a subscription. The query parameters listed here are common to all :doc:`../data-type/event-type`. In order to successfully create a subscription the body of the request must specify all required properties of the particular :doc:`../data-type/event-type`.

.. note::
   Existing subscriptions cannot be updated.  To "change" a subscription, you must delete the old one
   and create a new one.

*Query Paths*

   * /account/{account-id}/eventSubscription/{event-type}/
   * /vehicle/{vehicle-id}/eventSubscription/{event-type}/

*Query Parameters*

   +------------+----------------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                              |
   +============+==========================================================================================================+
   | account-id | The Carvoyant identifier of the account. This is used for account level subscriptions                    |
   +------------+----------------------------------------------------------------------------------------------------------+
   | vehicle-id | The Carvoyant identifier of the vehicle. This could be the device serial number in the car (for example, |
   |            | C201200001) or it could be the internal id returned from a previous lookup. This is used for vehicle     |
   |            | level subscriptions                                                                                      |
   +------------+----------------------------------------------------------------------------------------------------------+
   | event-type | Indicates the :doc:`../data-type/event-type` of subscriptions to be returned.                            |
   +------------+----------------------------------------------------------------------------------------------------------+

*Sample Request*::

   {
      "minimumTime": 0,
      "postUrl": "https://test.carvoyant.com/notify",
      "postHeaders": {
         "Authorization": "Bearer asdfqwerzxcv",
         "X-Sample-Headers": "Some custom value"
      },
      "notificationPeriod": "CONTINUOUS"
   }

DELETE
------

Marks a subscription for deletion. The system will purge the subscription after a set amount of time. These are not immediately deleted because doing so would also delete the history of :doc:`event-notification` s for this subscription.

*Query Paths*

   * /account/{account-id}/eventSubscription/{subscription-id}
   * /account/{account-id}/eventSubscription/{event-type}/{subscription-id}
   * /vehicle/{vehicle-id}/eventSubscription/{subscription-id}
   * /vehicle/{vehicle-id}/eventSubscription/{event-type}/{subscription-id}

*Query Parameters*

   +-----------------+----------------------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                                              |
   +=================+==========================================================================================================+
   | account-id      | The Carvoyant identifier of the account. This is used for account level subscriptions                    |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | vehicle-id      | The Carvoyant identifier of the vehicle. This could be the device serial number in the car (for example, |
   |                 | C201200001) or it could be the internal id returned from a previous lookup. This is used for vehicle     |
   |                 | level subscriptions                                                                                      |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | subscription-id | The Carvoyant identifier of the subscription. If the subscription-id is not                              |
   |                 | specified, then all subscriptions available will be returned.                                            |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | event-type      | Indicates the :doc:`../data-type/event-type` of subscriptions to be returned.                            |
   +-----------------+----------------------------------------------------------------------------------------------------------+

*Sample JSON Response*::

   {
       "result": "OK",
       "totalRecords": 1,
       "actions": []
   }
