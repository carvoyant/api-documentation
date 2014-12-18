Test EventSubscription
======================

Generates an :doc:`event-notification` for the specified :doc:`event-subscription`.  This allows you to test that your subscription is configured properly. A dummy :doc:`event-notification` object will be delivered to the postUrl provided in the requested :doc:`event-subscription` and as a response to this request. The dummy notification will have null values where there would normally be recorded data that triggered the event.

*Supported Verbs*

   * GET

GET
---

*Query Paths*

   * test/vehicle/{vehicle-id}/eventSubscription/{subscription-id}

*Query Parameters*

+-----------------+-------------------------------------------------------------------------------------------------------------------------+
| Parameter       | Description                                                                                                             |
+=================+=========================================================================================================================+
| vehicle-id      | The Carvoyant identifier of the vehicle. This could be the device serial number in the car (for example, C201200001) or |
|                 | it could be the internal id returned from a previous lookup.                                                            |
+-----------------+-------------------------------------------------------------------------------------------------------------------------+
| subscription-id | The Carvoyant identifier of the subscription.                                                                           |
+-----------------+-------------------------------------------------------------------------------------------------------------------------+

*Call Options*

   +----------+----+
   | Sortable | No |
   +----------+----+
   | Pageable | No |
   +----------+----+

*Sample JSON Response*::

   {
      "notification": {
         "id": 1098702,
         "subscriptionId": 1645,
         "_domain": "carvoyant.com",
         "_type": "LOWBATTERY",
         "_name": "LOWBATTERY",
         "_timestamp": "20141218T211057+0000",
         "minimumTime": 0,
         "httpStatusCode": 500,
         "notificationPeriod": "STATECHANGE",
         "dataSetId": null,
         "creatorClientId": "hasa2czfebhsj6XXXXXXXXXX",
         "thresholdVoltage": 12,
         "recordedVoltage": null
      },
      "totalRecords": 1
   }
