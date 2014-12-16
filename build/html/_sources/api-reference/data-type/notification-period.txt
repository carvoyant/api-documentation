NotificationPeriod
==================

NotificationPeriod is a string that represents when EventNotifications are sent from the Carvoyant system.

+--------------+----------------------------------------------------------------------------------------------------------------+
| Key String   | Description                                                                                                    |
+==============+================================================================================================================+
| CONTINUOUS   | Every time a data point is collected and the EventSubscription criteria is met, an EventNotification           |
|              | will be sent.  When the criteria is no longer met, an EventNotification will NOT be sent.                      |
+--------------+----------------------------------------------------------------------------------------------------------------+
| STATECHANGE  | An EventNotification will be sent when the EventSubscription criteria is first met. Another EventNotification  |
|              | will be sent when the criteria is no longer met.                                                               |
+--------------+----------------------------------------------------------------------------------------------------------------+
| INITIALSTATE | An EventNotification will be sent when the EventSubscription criteria is first met.  Another EventNotification |
|              | will not be sent until the criteria is no longer met, and then is met again.                                   |
+--------------+----------------------------------------------------------------------------------------------------------------+
| ONETIME      | An EventNotification will be sent when the EventSubscription criteria is first met and the EventSubscription   |
|              | will be deleted.  No further event EventNotifications will be sent.                                            |
+--------------+----------------------------------------------------------------------------------------------------------------+

Here's a chart to help visualize when event notifications are sent for each state:

.. image:: notificationperiod.png

.. note::

   Not all NotificationPeriod values will be supported for every EventNotification