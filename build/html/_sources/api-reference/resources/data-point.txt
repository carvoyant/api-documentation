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

GET
---

Returns raw vehicle data for the specified vehicle.  By default, the first 50 results are returned.

**Query Paths**

   * /vehicle/{vehicle-id}/data/
   * /vehicle/{vehicle-id}/data/?key={key-id}
   * /vehicle/{vehicle-id}/data/?mostRecentOnly=true

**Query Parameters**

   +----------------+-------------------------------------------------------------------------------------------------+
   | Parameter      | Description                                                                                     |
   +================+=================================================================================================+
   | key            | Allows only specific data types to be returned. See DataKey for the allowable types.            |
   +----------------+-------------------------------------------------------------------------------------------------+
   | mostRecentOnly | If this is present, only the most recently collected data point for each type will be returned. |
   +----------------+-------------------------------------------------------------------------------------------------+

**Call Options**

   +----------+-----+
   | Sortable | Yes |
   +----------+-----+
   | Pagable  | Yes |
   +----------+-----+
