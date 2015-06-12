DeliveryType
============

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

*HTTP_POST Properties*

+-------------+--------+------------------------------------------------------------------------------------------------------------+-----------------------+
| Name        | Type   | Description                                                                                                | Required for Creation |
+=============+========+============================================================================================================+=======================+
| postUrl     | String | The URL that will receive HTTPS POST notifications from the newly generated subscription. Note that only   | Required              |
|             |        | HTTPS endpoints are supported. The certificate protecting the post URL must be a valid signed certificate. |                       |
+-------------+--------+------------------------------------------------------------------------------------------------------------+-----------------------+
| postHeaders | Map    | A map that contains any headers that should be sent to the postUrl when a notification is generated.       | Optional              |
+-------------+--------+------------------------------------------------------------------------------------------------------------+-----------------------+
| oauth2      | Map    | A map that contains the values for OAuth2 based authentication of notifications endpoints.                 | Optional              |
+-------------+--------+------------------------------------------------------------------------------------------------------------+-----------------------+

OAUTH2
~~~~~~

A DeliveryType can use OAuth2 as an authentication mechanism when sending the HTTP_POST. The following fields are required as a part of the oauth2 map.

*OAUTH2 Properties*

+---------------+--------+------------------------------------------------------------------------------------------------------------------+-----------------------+
| Name          | Type   | Description                                                                                                      | Required for Creation |
+===============+========+==================================================================================================================+=======================+
| access_token  | String | The access token to be included in the request.                                                                  | Required              |
+---------------+--------+------------------------------------------------------------------------------------------------------------------+-----------------------+
| client_id     | String | The OAuth2 client id in the receiving system.                                                                    | Required              |
+---------------+--------+------------------------------------------------------------------------------------------------------------------+-----------------------+
| client_secret | String | The OAuth2 client secret in the receiving system.                                                                | Required              |
+---------------+--------+------------------------------------------------------------------------------------------------------------------+-----------------------+
| refresh_token | String | The OAuth2 refresh token for this access token. If a 401 is returned from a notification request                 | Required              |
|               |        | the Carvoyant system will attempt to refresh the token. This will follow the format in the OAuth2 specification. |                       |
+---------------+--------+------------------------------------------------------------------------------------------------------------------+-----------------------+
| redirect_uri  | String | The URI to use when refreshing a token.                                                                          | Required              |
+---------------+--------+------------------------------------------------------------------------------------------------------------------+-----------------------+

When a notification is delivered using OAuth2, the initial HTTP_POST to the postUrl will contain an *authorization* header with the value "Bearer <access_token>".
If the delivery returns an HTTP status of 401 (Unauthorized), the Carvoyant system will attempt to refresh the token. A request will be sent to the redirect_uri
following the `OAuth2 <http://tools.ietf.org/html/draft-ietf-oauth-v2-20#page-40>`_ refresh token specification. The request will use an http POST and will look like the following:

<redirect_uri>?grant_type=refresh_token&client_id=<client_id>&client_secret=<client_secret>&refresh_token=<refresh_token>

The expected response will be a JSON object that contains the properties "access_token" and "refresh_token". Those values will update the delivery object and the notification
will be retried.


EMAIL
-----

This DeliveryType will send an email with the details of the :doc:`../resources/event-notification` .

*EMAIL Properties*

+-------------------+--------+-------------------------------------------------+-----------------------+
| Name              | Type   | Description                                     | Required for Creation |
+===================+========+=================================================+=======================+
| recipient         | String | The email address to send the notificaation to. | Required              |
+-------------------+--------+-------------------------------------------------+-----------------------+
| subscriberSubject | String | The subject of the notification email.          | Optional              |
+-------------------+--------+-------------------------------------------------+-----------------------+
| subscriberContent | String | The body of the notification email.             | Optional              |
+-------------------+--------+-------------------------------------------------+-----------------------+
   