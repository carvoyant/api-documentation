Vehicle
=======

The Vehicle object represents a unique vehicle within the Carvoyant system. All data with a drivers car/truck is associated with this object.

*Properties*

+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| Property             | Type                          | Description                                                                                     | Required for Creation |
+======================+===============================+=================================================================================================+=======================+
| name                 | String                        | The text representation of the vehicle type. For instance, "2010 Jeep Wrangler". If the vehicle | Unsupported           |
|                      |                               | type is not known, the value of this property will be "Unidentified Vehicle"                    |                       |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| vehicleId            | Integer                       | The internal system identifier for this vehicle.                                                | Unsupported           |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| deviceId             | String                        | The serial number for the Carvoyant device installed in this vehicle.                           | Optional              |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| vin                  | String                        | The Vehicle Identifier Number. Will be null if the vehicle is currently unidentified.           | Optional              |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| label                | String                        | A custom label that the driver can assign to the vehicle.                                       | Optional              |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| mileage              | Integer                       | The current odometer reading of the vehicle.                                                    | Optional              |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| lastWaypoint         | :doc:`../data-type/waypoint`  | The last known geographic location of the vehicle.                                              | Unsupported           |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| running              | Boolean                       | Whether the vehicle is currently running.                                                       | Unsupported           |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| lastRunningTimestamp | :doc:`../data-type/date-time` | The time that the vehicle was last running.                                                     | Unsupported           |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| year                 | String                        | The Year the vehicle was made.                                                                  | Unsupported           |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| make                 | String                        | The make of the vehicle.                                                                        | Unsupported           |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
| model                | String                        | The model of the vehicle.                                                                       | Unsupported           |
+----------------------+-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+

*Supported Verbs*

   * GET
   * POST
   * DELETE

GET
---

Returns one or more vehicles.  By default, the first 50 results are returned.

*Query Paths*

   * /vehicle/
   * /vehicle/{vehicle-id}

*Query Parameters*

   +------------+----------------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                              |
   +============+==========================================================================================================+
   | vehicle-id | The Carvoyant identifier of the vehicle. This could be the device serial number in the car (for example, |
   |            | C201200001) or it could be the internal id returned from a previous lookup. If the vehicle-id is not     |
   |            | specified, then all vehicles available will be returned.                                                 |
   +------------+----------------------------------------------------------------------------------------------------------+

*Call Options*

   +----------+----+
   | Sortable | No |
   +----------+----+
   | Pageable | No |
   +----------+----+

*Sample JSON Response*::

   {
       "vehicle": {
           "name": "1999 Jeep Wrangler",
           "vehicleId": 3,
           "deviceId": "C201200001",
           "vin": "12345678912345678",
           "label": "Custom dune buggy",
           "mileage": 159774,
           "lastWaypoint": {
               "timestamp": "20140116T152440+0000",
               "latitude": 28.088505,
               "longitude": -82.578467
           },
           "running": false,
           "lastRunningTimestamp": "20140116T151952+0000",
           "year": "1999",
           "make": "Jeep",
           "model": "Wrangler
       },
       "totalRecords": null,
       "actions": []
   }

POST
----

Creates or updates a vehicle.

*Query Paths*

   * /vehicle/
   * /vehicle/{vehicle-id}

*Query Parameters*

   +------------+----------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                        |
   +============+====================================================================================================+
   | vehicle-id | The Carvoyant identifier of the vehicle. This could be the device serial number in the car         |
   |            | (for example, C201200001) or it could be the internal id returned from a previous lookup. If       |
   |            | the vehicle-id is not specified, a new vehicle will be created. If it is specified, then any       |
   |            | vehicle fields specified in the request will be updated. Unspecified fields will remain unchanged. |
   +------------+----------------------------------------------------------------------------------------------------+

DELETE
------

Deletes the specified vehicle.

.. warning::

   This operation is permanent! All data and configuration for the vehicle will be deleted and cannot be restored. Please ensure
   that the Carvoyant account owner confirms this operation before making the API call.
   
*Query Paths*

   * /vehicle/{vehicle-id}

*Query Parameters*

   +------------+----------------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                              |
   +============+==========================================================================================================+
   | vehicle-id | The Carvoyant identifier of the vehicle. This could be the device serial number in the car (for example, |
   |            | C201200001) or it could be the internal id returned from a previous lookup.                              |
   +------------+----------------------------------------------------------------------------------------------------------+

*Sample JSON Response*::

   {
       "result": "OK",
       "totalRecords": 1,
       "actions": []
   }
