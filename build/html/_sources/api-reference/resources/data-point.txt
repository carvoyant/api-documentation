DataPoint
=========

Represents a data point collected from a vehicle.

*Properties*

+-----------------+-------------------------------+---------------------------------------------------------------------------------------------------------------+
| Property        | Type                          | Description                                                                                                   |
+=================+===============================+===============================================================================================================+
| id              | Integer                       | The internal system identifier for this data point.                                                           |
+-----------------+-------------------------------+---------------------------------------------------------------------------------------------------------------+
| timestamp       | :doc:`../data-type/date-time` | The time that the data point was collected.                                                                   |
+-----------------+-------------------------------+---------------------------------------------------------------------------------------------------------------+
| key             | :doc:`../data-type/data-key`  | The type of data collected.                                                                                   |
+-----------------+-------------------------------+---------------------------------------------------------------------------------------------------------------+
| value           | String                        | The raw value collected from the vehicle.                                                                     |
+-----------------+-------------------------------+---------------------------------------------------------------------------------------------------------------+
| translatedValue | String                        | The value collected translated into human understandable form. This should only be used for display purposes. |
+-----------------+-------------------------------+---------------------------------------------------------------------------------------------------------------+

*Supported Verbs*

   * GET

GET
---

Returns raw vehicle data for the specified vehicle.  By default, the first 50 results are returned.

*Query Paths*

   * /vehicle/{vehicle-id}/data/
   * /vehicle/{vehicle-id}/data/?key={key-id}
   * /vehicle/{vehicle-id}/data/?mostRecentOnly=true

*Query Parameters*

   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter      | Description                                                                                                     |
   +================+=================================================================================================================+
   | key            | Allows only specific data types to be returned. See :doc:`../data-type/data-key` for the allowable ``key-id``s. |
   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | mostRecentOnly | If this is present, only the most recently collected data point for each type will be returned.                 |
   +----------------+-----------------------------------------------------------------------------------------------------------------+

*Call Options*

   +----------+--------------------------------------------------------------+
   | Sortable | :doc:`Yes </api-overview/sorting-and-paging>` (by timestamp) |
   +----------+--------------------------------------------------------------+
   | Pageable | :doc:`Yes </api-overview/sorting-and-paging>`                |
   +----------+--------------------------------------------------------------+

*Sample JSON Response*::

   {
       "data": [
           {
               "id": 8727772,
               "timestamp": "20140116T183654+0000",
               "key": "GEN_WAYPOINT",
               "value": "28.088472,-82.578439",
               "translatedValue": "28.088472,-82.578439"
           },
           {
               "id": 8727773,
               "timestamp": "20140116T183654+0000",
               "key": "GEN_VOLTAGE",
               "value": "12.6",
               "translatedValue": "12.6V"
           }
       ],
       "totalRecords": 65070,
       "actions": [
           {
               "name": "next",
               "uri": "https://api.carvoyant.com/v1/api/vehicle/C201200001/data/?sortOrder=desc&searchOffset=2&searchLimit=2",
               "methods": null,
               "inputs": null
           }
       ]
   }
