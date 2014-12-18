DataSet
=======

A DataSet is a collection of :doc:`data-point` s taken at the same time.  For example, a DataSet may contain a speed value, a battery voltage value and a GPS location.  It should be assumed that the DataPoints are related and were collected at the same time. This allows you to correlate different DataPoints with each other.

*Properties*

+----------------+-------------------------------+-----------------------------------------------------------+
| Property       | Type                          | Description                                               |
+================+===============================+===========================================================+
| id             | Integer                       | The internal system identifier for this data set.         |
+----------------+-------------------------------+-----------------------------------------------------------+
| timestamp      | :doc:`../data-type/date-time` | The time that the DataSet was created.                    |
+----------------+-------------------------------+-----------------------------------------------------------+
| datum          | :doc:`data-point`             | The :doc:`data-point` s contained within this DataSet.    |
+----------------+-------------------------------+-----------------------------------------------------------+
| ignitionStatus | String Enumeration            | The state of the vehicle when this DataSet was collected. |
|                | ON                            |                                                           |
|                | OFF                           |                                                           |
|                | RUNNING                       |                                                           |
+----------------+-------------------------------+-----------------------------------------------------------+

*Supported Verbs*

   * GET
   * POST

GET
---

Returns data sets for the specified vehicle.  By default, the first 50 results are returned.

*Query Paths*

   * /vehicle/{vehicle-id}/dataSet/

*Call Options*

   +----------+--------------------------------------------------------------+
   | Sortable | :doc:`Yes </api-overview/sorting-and-paging>` (by timestamp) |
   +----------+--------------------------------------------------------------+
   | Pageable | :doc:`Yes </api-overview/sorting-and-paging>`                |
   +----------+--------------------------------------------------------------+

*Sample JSON Response*::

   {
       "dataSet": [
           {
               "id": 1187922,
               "timestamp": "19991130T000000+0000",
               "datum": [
                   {
                       "id": 4562158,
                       "timestamp": "19991130T000000+0000",
                       "key": "GEN_WAYPOINT",
                       "value": "0.000000,0.000000",
                       "translatedValue": "0.000000,0.000000"
                   },
                   {
                       "id": 4562160,
                       "timestamp": "19991130T000000+0000",
                       "key": "GEN_VOLTAGE",
                       "value": "13.9",
                       "translatedValue": "13.9V"
                   },
                   {
                       "id": 4562163,
                       "timestamp": "19991130T000000+0000",
                       "key": "GEN_FUELRATE",
                       "value": "0.0",
                       "translatedValue": "0.0 gph"
                   }
               ]
           },
           {
               "id": 1562501,
               "timestamp": "19991130T000000+0000",
               "datum": [
                   {
                       "id": 6223164,
                       "timestamp": "19991130T000000+0000",
                       "key": "GEN_WAYPOINT",
                       "value": "0.000000,0.000000",
                       "translatedValue": "0.000000,0.000000"
                   },
                   {
                       "id": 6223165,
                       "timestamp": "19991130T000000+0000",
                       "key": "GEN_VOLTAGE",
                       "value": "13.9",
                       "translatedValue": "13.9V"
                   },
                   {
                       "id": 6223167,
                       "timestamp": "19991130T000000+0000",
                       "key": "GEN_FUELLEVEL",
                       "value": "0",
                       "translatedValue": "0 %"
                   }
               ]
           }
       ],
       "totalRecords": 23893,
       "actions": [
           {
               "name": "next",
               "uri": "https://api.carvoyant.com/v1/api/vehicle/C201200001/dataSet/?searchOffset=2&searchLimit=2",
               "methods": null,
               "inputs": null
           }
       ]
   }

POST
----

Saves the data set to the specified vehicle. Note that in the production environment, this is a restricted call that only certain partners are authorized to use. If you feel you need to make calls to this endpoint, please `contact us <mailto://support@carvoyant.com>`_ . In the sandbox environment, this is available for everyone.

*Query Paths*

   * /vehicle/{vehicle-id}/dataSet/

*Sample JSON Request*::

   {  
      "timestamp":"20140811T140444+0000",
      "ignitionStatus":"ON",
      "datum":[  
         {  
            "timestamp":"20140811T140444+0000",
            "key":"GEN_WAYPOINT",
            "value":"28.027065,-82.588619"
         },
         {  
            "timestamp":"20140811T140444+0000",
            "key":"GEN_HEADING",
            "value":323
         },
         {  
            "timestamp":"20140811T140444+0000",
            "key":"GEN_VOLTAGE",
            "value":"13.6"
         }
      ]
   }
