DeliveryType
============

.. error:: 

   DeliveryType objects within an :doc:`../resources/event-subscription` are not yet supported
   in the production environment.

A DeliveryType represents how a notification should be sent when the subscription criteria is met. The following types are supported:

* HTTP_POST
* EMAIL

*DeliveryType Properties*

+--------------------+--------------------+--------------------------------------------------------------------------------+-----------------------+
| Name               | Type               | Description                                                                    | Required for Creation |
+====================+====================+================================================================================+=======================+
| type               | POST_HTTP or EMAIL | The type of delivery.                                                          | Required              |
+--------------------+--------------------+--------------------------------------------------------------------------------+-----------------------+
| active             | boolean            | Indicates if the DeliveryType is currently active. This can only be set by the | Unsupported           |
|                    |                    | Carvoyant system (it cannot be set through the API)                            |                       |
+--------------------+--------------------+--------------------------------------------------------------------------------+-----------------------+
| deactivationReason | String             | If the system deactivates this DeliveryType, this field will indicate why.     | Unsupported           |
+--------------------+--------------------+--------------------------------------------------------------------------------+-----------------------+

HTTP_POST
---------

This DeliveryType will uses HTTP POST to submit the :doc:`../resources/event-notification` the specified URL.

*DeliveryType Properties*

+-------------+--------+------------------------------------------------------------------------------------------------------------+-----------------------+
| Name        | Type   | Description                                                                                                | Required for Creation |
+=============+========+============================================================================================================+=======================+
| postUrl     | String | The URL that will receive HTTPS POST notifications from the newly generated subscription. Note that only   | Required              |
|             |        | HTTPS endpoints are supported. The certificate protecting the post URL must be a valid signed certificate. |                       |
+-------------+--------+------------------------------------------------------------------------------------------------------------+-----------------------+
| postHeaders | Map    | A map that contains any headers that should be sent to the postUrl when a notification is generated.       | Optional              |
+-------------+--------+------------------------------------------------------------------------------------------------------------+-----------------------+

EMAIL
-----

This DeliveryType will send an email with the details of the :doc:`../resources/event-notification` .

*DeliveryType Properties*

+-------------------+--------+-------------------------------------------------+-----------------------+
| Name              | Type   | Description                                     | Required for Creation |
+===================+========+=================================================+=======================+
| recipient         | String | The email address to send the notificaation to. | Required              |
+-------------------+--------+-------------------------------------------------+-----------------------+
| subscriberSubject | String | The subject of the notification email.          | Optional              |
+-------------------+--------+-------------------------------------------------+-----------------------+
| subscriberContent | String | The body of the notification email.             | Optional              |
+-------------------+--------+-------------------------------------------------+-----------------------+
   