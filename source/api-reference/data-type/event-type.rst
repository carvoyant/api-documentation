EventType
=========

An EventType represents and event that can be triggered within the Carvoyant system. API users can subscribe to these events using an :doc:`../resources/event-subscription`. This page describes the details of each event type. In the details below you will find the following:

* Event Scope: Events can be set at the system, account or vehicle scope.
+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| Scope   | Description                                                                                                                                                                                                                 | Query Path Prefixes |
+=========+=============================================================================================================================================================================================================================+=====================+
| System  | These subscriptions are created using the Client Credentials mechanism and are not account specific. They allow you to subscribe to system level events.                                                                    | /system             |
+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| Account | These subscriptions are applicable to the account that the access token applies to.                                                                                                                                         | /account            |
+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| Vehicle | These subscriptions are applicable to a specific vehicle. They can be specified at the account level in which case the Carvoyant system will ensure that all vehicles on your account have the subscription created for it. | /account            |
|         |                                                                                                                                                                                                                             | /vehicle            |
+---------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+

* Event Type Key: This is the string that will be used in :doc:`../resources/event-subscription` and :doc:`../resources/event-notification` objects wherever you see {event-type}.
* Subscription Properties: This will be the list of propertis that are specified when the subscription is created.
* Supported Notification Periods: This will list which :doc:`notification-period` values are supported for the event type.

Geo Fence
---------

GeoFence events will trigger when a vehicles location is reported at a certain location.  This is evaluated any time a :doc:`waypoint` is received by the system.

*Scope*: Vehicle

*Event Type Key*: GEOFENCE

*Subscription Properties*

+-------------------+------------------------------+--------------------------------------------------------------------------------+-----------------------+
| Name              | Type                         | Description                                                                    | Required for Creation |
+===================+==============================+================================================================================+=======================+
| origin            | :doc:`../data-type/waypoint` | The reference location on which to base event notification                     | Required              |
+-------------------+------------------------------+--------------------------------------------------------------------------------+-----------------------+
| radius            | Float                        | The length of the radius extending outward from the origin that creates the    | Required              |
|                   |                              | GeoFence boundary. This is specified in miles.                                 |                       |
+-------------------+------------------------------+--------------------------------------------------------------------------------+-----------------------+
| ignitionStatus    | String Enumeration:          | Defines the required ignition state of the vehicle that must be met in order   | Required              |
|                   | ON                           | for the event notification to occur.                                           |                       |
|                   | OFF                          |                                                                                |                       |
|                   | RUNNING                      |                                                                                |                       |
|                   | ANY                          |                                                                                |                       |
+-------------------+------------------------------+--------------------------------------------------------------------------------+-----------------------+
| boundaryCondition | String Enumeration:          | Specifies whether to trigger the event notification if the vehicle is "INSIDE" | Required              |
|                   | INSIDE                       | or "OUTSIDE" of the defined boundary.                                          |                       |
|                   | OUTSIDE                      |                                                                                |                       |
+-------------------+------------------------------+--------------------------------------------------------------------------------+-----------------------+

*Supported Notification Periods*

   * CONTINUOUS
   * STATECHANGE
   * INITIAL
   * ONETIME

Ignition Status
---------------

Ignition status events will trigger when a vehicles engine state (ie, ignition state) is turned on or off.

*Scope*: Vehicle

*Event Type Key*: IGNITIONSTATUS

*Subscription Properties*: No additional properties

*Supported Notification Periods*

   * STATECHANGE
   * INITIAL
   * ONETIME

Low Battery
-----------

The low battery event will trigger when the voltage read from the vehicle falls below 12.0V.  For other values, see the Numeric Data Keys event type.

*Scope*: Vehicle

*Event Type Key*: LOWBATTERY

*Subscription Properties*: No additional properties

*Supported Notification Periods*

   * CONTINUOUS
   * STATECHANGE
   * INITIAL
   * ONETIME

Numeric Data Keys
-----------------

Numeric data key events will trigger when the value of the specified :doc:`data-key` meets the criteria. This can be used to customize events off of any numerical data point collected by Carvoyant.

*Scope*: Vehicle

*Event Type Key*: NUMERICDATAKEY

*Subscription Properties*

+----------------+-----------------+-----------------------------------------------------------------------------------+-----------------------+
| Name           | Type            | Description                                                                       | Required for Creation |
+================+=================+===================================================================================+=======================+
| dataKey        | :doc:`data-key` | The :doc:`data-key` to check against. Note that the following keys are supported: | Required              |
|                |                 | GEN_VOLTAGE, GEN_TRIP_MILEAGE, GEN_ODOMETER, GEN_HEADING, GEN_RPM, GEN_FUELLEVEL, |                       |
|                |                 | GEN_FUELRATE, GEN_ENGINE_COOLANT_TEMP, GEN_SPEED                                  |                       |
+----------------+-----------------+-----------------------------------------------------------------------------------+-----------------------+
| thresholdValue | Float           | The value that determines when to send the event notification in reference        | Required              |
|                |                 | to the corresponding vehicle data.                                                |                       |
+----------------+-----------------+-----------------------------------------------------------------------------------+-----------------------+
| relationship   | String:         | Defines the condition that is used to compare the value of the subscription       | Required              |
|                | ABOVE           | against current vehicle data.                                                     |                       |
|                | BELOW           |                                                                                   |                       |
|                | EQUALTO         |                                                                                   |                       |
+----------------+-----------------+-----------------------------------------------------------------------------------+-----------------------+

*Supported Notification Periods*

   * CONTINUOUS
   * STATECHANGE
   * INITIAL
   * ONETIME

Time Of Day
-----------

The TimeOfDay Subscription allows event notification when a vehicle is operated outside of a defined time period. 

*Scope*: Vehicle

*Event Type Key*: TIMEOFDAY

*Subscription Properties*

+----------------+------------------------------+------------------------------------------------------------------------------+-----------------------+
| Name           | Type                         | Description                                                                  | Required for Creation |
+================+==============================+==============================================================================+=======================+
| startTime      | String in                    | The time of day that the vehicle is permitted to run.                        | Required              |
|                | HH:MM format                 |                                                                              |                       |
+----------------+------------------------------+------------------------------------------------------------------------------+-----------------------+
| endTime        | String in                    | The time of day when the vehicle is no longer permitted to run.              | Required              |
|                | HH:MM format                 |                                                                              |                       |
+----------------+------------------------------+------------------------------------------------------------------------------+-----------------------+
| daysOfWeek     | Array of String Enumeration: | Represents the days of the week that the vehicle is permitted to run.        | Required              |
|                | SUN, MON, TUE, WED, THU,     |                                                                              |                       |
|                | FRI, SAT, SUN                |                                                                              |                       |
+----------------+------------------------------+------------------------------------------------------------------------------+-----------------------+
| ignitionStatus | String Enumeration:          | Defines the required ignition state of the vehicle that must be met in order | Required              |
|                | ON                           | for the event notification to occur.                                         |                       |
|                | OFF                          |                                                                              |                       |
|                | RUNNING                      |                                                                              |                       |
|                | ANY                          |                                                                              |                       |
+----------------+------------------------------+------------------------------------------------------------------------------+-----------------------+

*Supported Notification Periods*

   * CONTINUOUS
   * STATECHANGE
   * INITIAL
   * ONETIME

Trouble Code
------------

The trouble code event will trigger when the vehicle reports a Diagnostic Trouble Code (DTC).

*Scope*: Vehicle

*Event Type Key*: TROUBLECODE

*Subscription Properties*: No additional properties

*Supported Notification Periods*

   * INITIAL
   * ONETIME

Driver Behaviors
----------------

Driver behavior events trigger based on how the driver is driving.  Each are determined using an internal accelerometer within the device in the vehicle.

*Scope*: Vehicle

*Event Type Keys*:
   * VEHICLEHARSHACCEL: Indicates that a high rate of acceleration has been detected.
   * VEHICLEHARSHDECEL: Indicates that a high rate of deceleration has been detected.
   * VEHICLEHARSHRIGHT: Indicates that a hard right turn has been detected.
   * VEHICLEHARSHLEFT: Indicates that a hard left turn has been detected.
   * VEHICLEIMPACT: Indicates that an impact has been detected. Please note that currently, the act of plugging in or unplugging a device to the OBDII port while the vehicle is on may trigger this event.
   
.. note::
   Driver behavior events will only be triggered while the vehicle is running.  Specifically, this means that an impact that takes place while
   the vehicle is not running will not trigger an alert.

*Subscription Properties*: No additional properties

*Supported Notification Periods*

   * INITIAL
   * ONETIME

Vehicle Events
--------------

Vehicle events are generally related to events that occur with the vehicle that do not have to do with driving activities.

*Scope*: Vehicle

*Event Type Keys*:
   * VEHICLECONNECTED: Indicates that connectivity to the car has been established. For OBDII based cars, this means the device has been plugged in.
   * VEHICLEDISCONNECTED: Indicates that connectivity to the car has been removed. For OBDII based cars, this means the device has been unplugged.
   * VEHICLETOWED: Indicates that the vehicle is being towed. Specifically, this means the vehicle has moved a certain distance (currently 1500 meters) without the vehicle being turned on.
   
.. note::
   VEHICLETOWED will be triggered if the device is unplugged and then plugged back in after moving the configured distance.  If a device is unplugged
   and then plugged back in that distance away, the vehicle should be started.  That will clear the towing indicator on the device.

*Subscription Properties*: No additional properties

*Supported Notification Periods*

   * INITIAL
   * ONETIME

Vehicle Creation
----------------

These events allow you to react to the creation or deletion of a vehicle on an account.

*Scope*: Account

*Event Type Keys*:
   * VEHICLECREATED: Indicates that the vehicle has been created in the system.
   * VEHICLEDELETED: Indicates that the vehicle has been deleted from the system. Note that after receiving a notification that the vehicle has been deleted, you can no longer query against it.
   
*Subscription Properties*: No additional properties

*Supported Notification Periods*

   * ONETIME
   * CONTINUOUS
   
Account Authorization
---------------------

This event will notify you of the change in access grants to an account for your client id. At this time, only revoke notifications will be sent.

*Scope*: System

*Event Type Key*:
   * AUTHORIZATIONSTATUS: Indicates that the authorization status for the account has changed.
   
*Subscription Properties*: No additional properties

*Supported Notification Periods*

   * ONETIME
   * CONTINUOUS
   
*Notification Properties*

+---------------------+--------------------+-------------------------------------------------------+
| Name                | Type               | Description                                           |
+=====================+====================+=======================================================+
| authorizationStatus | String Enumeration | The time of day that the vehicle is permitted to run. |
|                     | GRANTED, REVOKED   |                                                       |
+---------------------+--------------------+-------------------------------------------------------+
   