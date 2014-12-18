EventType
=========

An EventType represents and event that can be triggered within the Carvoyant system. API users can subscribe to these events using an :doc:`event-subscription`. This page describes the details of each event type. In the details below you will find the following:

* Event Type Key: This is the string that will be used in EventSubscription and EventNotification objects wherever you see {event-type}.
* Subscription Properties: This will be the list of propertis that are specified when the subscription is created.

Geo Fence
---------

GeoFence events will trigger when a vehicles location is reported at a certain location.  This is evaluated any time a :doc:`waypoint` is received by the system.

*Event Type Key*

GEOFENCE

*Subscription Properties*

+-------------------+---------------------+--------------------------------------------------------------------------------+-----------------------+
| Name              | Type                | Description                                                                    | Required for Creation |
+===================+=====================+================================================================================+=======================+
| origin            | Waypoint            | The reference location on which to base event notification                     | Required              |
+-------------------+---------------------+--------------------------------------------------------------------------------+-----------------------+
| radius            | Float               | The length of the radius extending outward from the origin that creates the    | Required              |
|                   |                     | GeoFence boundary. This is specified in miles.                                 |                       |
+-------------------+---------------------+--------------------------------------------------------------------------------+-----------------------+
| ignitionStatus    | String Enumeration: | Defines the required ignition state of the vehicle that must be met in order   | Required              |
|                   | * ON                | for the event notification to occur.                                           |                       |
|                   | * OFF               |                                                                                |                       |
|                   | * RUNNING           |                                                                                |                       |
|                   | * ANY               |                                                                                |                       |
+-------------------+---------------------+--------------------------------------------------------------------------------+-----------------------+
| boundaryCondition | String Enumeration: | Specifies whether to trigger the event notification if the vehicle is "INSIDE" | Required              |
|                   | * INSIDE            | or "OUTSIDE" of the defined boundary.                                          |                       |
|                   | * OUTSIDE           |                                                                                |                       |
+-------------------+---------------------+--------------------------------------------------------------------------------+-----------------------+

Ignition Status
---------------

Low Battery
-----------

Numeric Data Keys
-----------------

Time Of Day
-----------

Trouble Code
------------

Driver Behaviors
----------------

Vehicle Events
--------------
