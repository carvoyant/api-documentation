Alerts
======

The Carvoyant system can notify users when different types of events occur.  These are referred to as Alerts within the Driver Dashboard.  This example has one ignition status alert set up for the vehicle:

.. image:: driverdash-alerts.png

After selecting a subscription, you will see a list of any notifications that have been sent for it. Selecting a notification will display details of the alert.

The following alerts can be created:

   * GeoFence - This alert will let you monitor the location where your vehicles are travelling.
   * Ignition Status - This alert monitors whether the vehicle is on or off.
   * Low Battery - This alert indicates that the battery voltage has dropped below 12.0 volts.
   * Numeric Data Key - This alert lets you monitor any numeric data element (for example, when engine temperature has gone over a certain value).
   * Time of Day - This alert lets you monitor the time of day that a vehicle is being used. Note that the alert checks for vehicle activity outside the specified values.
   * Trouble Code - This alert monitors for any trouble codes that the vehicle throws.
   
When configuring an alert, the following properties can be selected for each alert type:

+----------------------+----------+----------+---------+----------+-------------+---------+
|                      | GeoFence | Ignition | Low     | Numeric  | Time of Day | Trouble |
|                      |          | Status   | Battery | Data Key |             | Code    |
+======================+==========+==========+=========+==========+=============+=========+
| Minimum Notification | X        | X        | X       | X        | X           | X       |
| Interval             |          |          |         |          |             |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Notification Period  | X        | X        | X       | X        | X           | X       |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Recipients           | X        | X        | X       | X        | X           | X       |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Location Map         | X        |          |         |          |             |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Radius               | X        |          |         |          |             |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Ignition Status      | X        |          |         |          |             |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Boundary Condition   | X        |          |         |          |             |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Data Key             |          |          |         | X        |             |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Threshold Value      |          |          |         | X        |             |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Relationship         |          |          |         | X        |             |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Start Time           |          |          |         |          | X           |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| End Time             |          |          |         |          | X           |         |
+----------------------+----------+----------+---------+----------+-------------+---------+
| Days of Week         |          |          |         |          | X           |         |
+----------------------+----------+----------+---------+----------+-------------+---------+

**Property Descriptions**

*Minimum Notification Interval*

This is the minimum time between alerts in minutes. If you set this value to 60, you will only receive onealert every 60 minutes even it the event occurs more frequently.

*Notification Period*

This describes when the alert will be checked. Possible values are:

   * Initial State - Only when the conditions are first met
   * One Time - Only when the conditions are first met, and then the alert is delete (subsequent events will not alert you)
   * Continuious - Alerts will be sent every time the Carvoyant system collects data that meet the alerts criteria
   * State Change - Alerts will be sent when the criteria is first met, and then when the criteria is no longer met

*Recipients*

The recipients of the alerts. Currently we support Email and Glympse. Email will send a simple email to the addresses listed. Glympse is an integration with the Glympse service and is currently in beta.

*Location Map*

Select a location on the map.

*Radius*

The distance from a point on the map. This is in miles but can be partial (for example, 0.2).

*Ignition Status*

This can be one of three values:

   * On - When the vehicle is first turned on
   * Off - When the vehicles is turned off
   * Running - Any time the vehicle is running

*Boundary Condition*

This can be one of two values:

   * Inside: The geofence is triggered when the vehicle is within the radius of the specified location
   * Outside: The geofence is triggered when the vehicle is outside the radius of the specified location

*Data Key*

Specified what data key type to monitor.

*Threshold Value*

The value of the recorded data key to check against.

*Relationship*

This can be one of three values:

   * Above - The recorded data is above the threshold value
   * Below - The recorded data is below the threshold value
   * Equals - The recorded data equals the threshold value

*Start Time*

The start time of the allowed window.

*End Time*

The end time of the allowed window.

*Days of Week*

The days of the week for the allowed window.


