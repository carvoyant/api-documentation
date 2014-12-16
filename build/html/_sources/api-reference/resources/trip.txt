Trip
====

This resource represents a Trip within the Carvoyant system.  A Trip is defined as the activity of a :doc:`vehicle` between ignition on and ignition off.

*Properties*

+---------------+-------------------------------+-----------------------------------------------------------------+
| Property      | Type                          | Description                                                     |
+===============+===============================+=================================================================+
| id            | Integer                       | The internal system identifier for this trip.                   |
+---------------+-------------------------------+-----------------------------------------------------------------+
| startTime     | :doc:`../data-type/date-time` | The start time of the trip.                                     |
+---------------+-------------------------------+-----------------------------------------------------------------+
| endTime       | :doc:`../data-type/date-time` | The end time of the trip if the trip is not in progress.        |
+---------------+-------------------------------+-----------------------------------------------------------------+
| mileage       | Float                         | The distance traveled during the trip.                          |
+---------------+-------------------------------+-----------------------------------------------------------------+
| startWaypoint | :doc:`../data-type/waypoint`  | The starting location of the trip.                              |
+---------------+-------------------------------+-----------------------------------------------------------------+
| endWaypoint   | :doc:`../data-type/waypoint`  | The ending location of the trip if the trip is in not progress. |
+---------------+-------------------------------+-----------------------------------------------------------------+
| data          | :doc:`data-set` Array         | An array of data sets collected during the trip.                |
+---------------+-------------------------------+-----------------------------------------------------------------+

*Supported Verbs*

   * GET

GET
---

Returns one or more trips for the specified vehicle. By default, the first 50 results are returned.

*Query Paths*

   * /vehicle/{vehicle-id}/trip/?includeData={true|false}&startTime={startTime}&endTime={endTime}
   * /vehicle/{vehicle-id}/trip/{trip-id}

*Query Parameters*

   +-------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter   | Description                                                                                                     |
   +=============+=================================================================================================================+
   | vehicle-id  | The Carvoyant identifier of the vehicle. This could be the device serial number in the car (for example,        |
   |             | C201200001) or it could be the internal id returned from a previous lookup. If the vehicle-id is not specified, |
   |             | then all vehicles available will be returned.                                                                   |
   +-------------+-----------------------------------------------------------------------------------------------------------------+
   | includeData | If true, then the results will include all of the DataSets collected during that trip. If false, the trip       |
   |             | object will not contain the datum property. Only applies if no trip-id is specified.                            |
   +-------------+-----------------------------------------------------------------------------------------------------------------+
   | startTime   | Used for filtering the results.  Only trips that started after this time are returned.  See DateTime for the    |
   |             | format details. Only applies if no trip-id is specified.                                                        |
   +-------------+-----------------------------------------------------------------------------------------------------------------+
   | endTime     | Used for filtering the results.  Only trips that started before this time are returned.  See DateTime for the   |
   |             | format details. Only applies if no trip-id is specified.                                                        |
   +-------------+-----------------------------------------------------------------------------------------------------------------+
   | trip-id     | The Carvoyant identifier for the trip.                                                                          |
   +-------------+-----------------------------------------------------------------------------------------------------------------+

*Call Options*

   +----------+--------------------------------------------------------------------------------------------------------------------------+
   | Sortable | :doc:`Yes </api-overview/sorting-and-paging>` (by startTime)                                                             |
   +----------+--------------------------------------------------------------------------------------------------------------------------+
   | Pageable | :doc:`Yes </api-overview/sorting-and-paging>` (when no trip-id is specified. Individual trip requests are not paginated) |
   +----------+--------------------------------------------------------------------------------------------------------------------------+

*Sample JSON Response (trip list)*::

   {
       "trip": [
           {
               "id": 198260,
               "startTime": "20140116T122340+0000",
               "endTime": "20140116T124904+0000",
               "mileage": 0.5,
               "startWaypoint": {
                   "timestamp": "20140116T122340+0000",
                   "latitude": 28.036539,
                   "longitude": -82.593698
               },
               "endWaypoint": {
                   "timestamp": "20140116T124904+0000",
                   "latitude": 28.036482,
                   "longitude": -82.593697
               }
           },
           {
               "id": 197923,
               "startTime": "20140115T230536+0000",
               "endTime": "20140115T231845+0000",
               "mileage": 5.9,
               "startWaypoint": {
                   "timestamp": "20140115T230536+0000",
                   "latitude": 28.088446,
                   "longitude": -82.578471
               },
               "endWaypoint": {
                   "timestamp": "20140115T231845+0000",
                   "latitude": 28.036513,
                   "longitude": -82.593683
               }
           }
       ],
       "totalRecords": 850,
       "actions": [
           {
               "name": "next",
               "uri": "https://api.carvoyant.com/v1/api/vehicle/C201200001/trip/?includeData=false&sortOrder=desc&startTime=20130627T090000%2B0000&searchOffset=4&searchLimit=2",
               "methods": null,
               "inputs": null
           },
           {
               "name": "previous",
               "uri": "https://api.carvoyant.com/v1/api/vehicle/C201200001/trip/?includeData=false&sortOrder=desc&startTime=20130627T090000%2B0000&searchLimit=2",
               "methods": null,
               "inputs": null
           }
       ]
   }

*Sample JSON Response (single trip)*::

   {
       "trip": {
           "id": 198260,
           "startTime": "20140116T122340+0000",
           "endTime": "20140116T124904+0000",
           "mileage": 0.5,
           "startWaypoint": {
               "timestamp": "20140116T122340+0000",
               "latitude": 28.036539,
               "longitude": -82.593698
           },
           "endWaypoint": {
               "timestamp": "20140116T124904+0000",
               "latitude": 28.036482,
               "longitude": -82.593697
           },
           "data": [
               {
                   "id": 2080099,
                   "timestamp": "20140116T124904+0000",
                   "datum": [
                       {
                           "id": 8713037,
                           "timestamp": "20140116T124904+0000",
                           "key": "GEN_TRIP_MILEAGE",
                           "value": "0.5",
                           "translatedValue": "1 miles"
                       },
                       {
                           "id": 8713036,
                           "timestamp": "20140116T124904+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "81.6",
                           "translatedValue": "204.5 deg F"
                       },
                       {
                           "id": 8713035,
                           "timestamp": "20140116T124904+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8713034,
                           "timestamp": "20140116T124904+0000",
                           "key": "GEN_SPEED",
                           "value": "17.0",
                           "translatedValue": "17.0 mph"
                       },
                       {
                           "id": 8713033,
                           "timestamp": "20140116T124904+0000",
                           "key": "GEN_HEADING",
                           "value": "148",
                           "translatedValue": "148 deg"
                       },
                       {
                           "id": 8713032,
                           "timestamp": "20140116T124904+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.036482,-82.593697",
                           "translatedValue": "28.036482,-82.593697"
                       }
                   ]
               },
               {
                   "id": 2080093,
                   "timestamp": "20140116T124839+0000",
                   "datum": [
                       {
                           "id": 8713013,
                           "timestamp": "20140116T124839+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "82.8",
                           "translatedValue": "206.6 deg F"
                       },
                       {
                           "id": 8713012,
                           "timestamp": "20140116T124839+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8713011,
                           "timestamp": "20140116T124839+0000",
                           "key": "GEN_SPEED",
                           "value": "27.6",
                           "translatedValue": "27.6 mph"
                       },
                       {
                           "id": 8713010,
                           "timestamp": "20140116T124839+0000",
                           "key": "GEN_HEADING",
                           "value": "81",
                           "translatedValue": "81 deg"
                       },
                       {
                           "id": 8713009,
                           "timestamp": "20140116T124839+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037042,-82.594338",
                           "translatedValue": "28.037042,-82.594338"
                       }
                   ]
               },
               {
                   "id": 2080083,
                   "timestamp": "20140116T124739+0000",
                   "datum": [
                       {
                           "id": 8712961,
                           "timestamp": "20140116T124739+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "80.0",
                           "translatedValue": "201.6 deg F"
                       },
                       {
                           "id": 8712960,
                           "timestamp": "20140116T124739+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712959,
                           "timestamp": "20140116T124739+0000",
                           "key": "GEN_HEADING",
                           "value": "333",
                           "translatedValue": "333 deg"
                       },
                       {
                           "id": 8712958,
                           "timestamp": "20140116T124739+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037880,-82.596209",
                           "translatedValue": "28.037880,-82.596209"
                       }
                   ]
               },
               {
                   "id": 2080073,
                   "timestamp": "20140116T124639+0000",
                   "datum": [
                       {
                           "id": 8712912,
                           "timestamp": "20140116T124639+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "78.9",
                           "translatedValue": "199.6 deg F"
                       },
                       {
                           "id": 8712911,
                           "timestamp": "20140116T124639+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712910,
                           "timestamp": "20140116T124639+0000",
                           "key": "GEN_HEADING",
                           "value": "333",
                           "translatedValue": "333 deg"
                       },
                       {
                           "id": 8712909,
                           "timestamp": "20140116T124639+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037871,-82.596204",
                           "translatedValue": "28.037871,-82.596204"
                       }
                   ]
               },
               {
                   "id": 2080060,
                   "timestamp": "20140116T124539+0000",
                   "datum": [
                       {
                           "id": 8712852,
                           "timestamp": "20140116T124539+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "78.9",
                           "translatedValue": "199.6 deg F"
                       },
                       {
                           "id": 8712851,
                           "timestamp": "20140116T124539+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712850,
                           "timestamp": "20140116T124539+0000",
                           "key": "GEN_SPEED",
                           "value": "1.4",
                           "translatedValue": "1.4 mph"
                       },
                       {
                           "id": 8712849,
                           "timestamp": "20140116T124539+0000",
                           "key": "GEN_HEADING",
                           "value": "333",
                           "translatedValue": "333 deg"
                       },
                       {
                           "id": 8712848,
                           "timestamp": "20140116T124539+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037944,-82.596230",
                           "translatedValue": "28.037944,-82.596230"
                       }
                   ]
               },
               {
                   "id": 2080053,
                   "timestamp": "20140116T124439+0000",
                   "datum": [
                       {
                           "id": 8712823,
                           "timestamp": "20140116T124439+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "78.9",
                           "translatedValue": "199.6 deg F"
                       },
                       {
                           "id": 8712822,
                           "timestamp": "20140116T124439+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712821,
                           "timestamp": "20140116T124439+0000",
                           "key": "GEN_SPEED",
                           "value": "2.8",
                           "translatedValue": "2.8 mph"
                       },
                       {
                           "id": 8712820,
                           "timestamp": "20140116T124439+0000",
                           "key": "GEN_HEADING",
                           "value": "333",
                           "translatedValue": "333 deg"
                       },
                       {
                           "id": 8712819,
                           "timestamp": "20140116T124439+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037912,-82.596222",
                           "translatedValue": "28.037912,-82.596222"
                       }
                   ]
               },
               {
                   "id": 2080043,
                   "timestamp": "20140116T124339+0000",
                   "datum": [
                       {
                           "id": 8712782,
                           "timestamp": "20140116T124339+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "78.9",
                           "translatedValue": "199.6 deg F"
                       },
                       {
                           "id": 8712781,
                           "timestamp": "20140116T124339+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712780,
                           "timestamp": "20140116T124339+0000",
                           "key": "GEN_SPEED",
                           "value": "1.1",
                           "translatedValue": "1.1 mph"
                       },
                       {
                           "id": 8712779,
                           "timestamp": "20140116T124339+0000",
                           "key": "GEN_HEADING",
                           "value": "133",
                           "translatedValue": "133 deg"
                       },
                       {
                           "id": 8712778,
                           "timestamp": "20140116T124339+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037902,-82.596198",
                           "translatedValue": "28.037902,-82.596198"
                       }
                   ]
               },
               {
                   "id": 2080036,
                   "timestamp": "20140116T124239+0000",
                   "datum": [
                       {
                           "id": 8712744,
                           "timestamp": "20140116T124239+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "80.0",
                           "translatedValue": "201.6 deg F"
                       },
                       {
                           "id": 8712743,
                           "timestamp": "20140116T124239+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712742,
                           "timestamp": "20140116T124239+0000",
                           "key": "GEN_HEADING",
                           "value": "165",
                           "translatedValue": "165 deg"
                       },
                       {
                           "id": 8712741,
                           "timestamp": "20140116T124239+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037869,-82.596201",
                           "translatedValue": "28.037869,-82.596201"
                       }
                   ]
               },
               {
                   "id": 2080028,
                   "timestamp": "20140116T124139+0000",
                   "datum": [
                       {
                           "id": 8712705,
                           "timestamp": "20140116T124139+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "80.5",
                           "translatedValue": "202.5 deg F"
                       },
                       {
                           "id": 8712704,
                           "timestamp": "20140116T124139+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712703,
                           "timestamp": "20140116T124139+0000",
                           "key": "GEN_SPEED",
                           "value": "4.7",
                           "translatedValue": "4.7 mph"
                       },
                       {
                           "id": 8712702,
                           "timestamp": "20140116T124139+0000",
                           "key": "GEN_HEADING",
                           "value": "165",
                           "translatedValue": "165 deg"
                       },
                       {
                           "id": 8712701,
                           "timestamp": "20140116T124139+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037881,-82.596196",
                           "translatedValue": "28.037881,-82.596196"
                       }
                   ]
               },
               {
                   "id": 2080016,
                   "timestamp": "20140116T124039+0000",
                   "datum": [
                       {
                           "id": 8712653,
                           "timestamp": "20140116T124039+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "77.8",
                           "translatedValue": "197.6 deg F"
                       },
                       {
                           "id": 8712652,
                           "timestamp": "20140116T124039+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712651,
                           "timestamp": "20140116T124039+0000",
                           "key": "GEN_SPEED",
                           "value": "1.5",
                           "translatedValue": "1.5 mph"
                       },
                       {
                           "id": 8712650,
                           "timestamp": "20140116T124039+0000",
                           "key": "GEN_HEADING",
                           "value": "351",
                           "translatedValue": "351 deg"
                       },
                       {
                           "id": 8712649,
                           "timestamp": "20140116T124039+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037978,-82.596189",
                           "translatedValue": "28.037978,-82.596189"
                       }
                   ]
               },
               {
                   "id": 2080009,
                   "timestamp": "20140116T123939+0000",
                   "datum": [
                       {
                           "id": 8712622,
                           "timestamp": "20140116T123939+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "78.9",
                           "translatedValue": "199.6 deg F"
                       },
                       {
                           "id": 8712621,
                           "timestamp": "20140116T123939+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712620,
                           "timestamp": "20140116T123939+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712619,
                           "timestamp": "20140116T123939+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037968,-82.596198",
                           "translatedValue": "28.037968,-82.596198"
                       }
                   ]
               },
               {
                   "id": 2080000,
                   "timestamp": "20140116T123839+0000",
                   "datum": [
                       {
                           "id": 8712583,
                           "timestamp": "20140116T123839+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "83.9",
                           "translatedValue": "208.6 deg F"
                       },
                       {
                           "id": 8712582,
                           "timestamp": "20140116T123839+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712581,
                           "timestamp": "20140116T123839+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712580,
                           "timestamp": "20140116T123839+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037968,-82.596202",
                           "translatedValue": "28.037968,-82.596202"
                       }
                   ]
               },
               {
                   "id": 2079993,
                   "timestamp": "20140116T123739+0000",
                   "datum": [
                       {
                           "id": 8712547,
                           "timestamp": "20140116T123739+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "80.5",
                           "translatedValue": "202.5 deg F"
                       },
                       {
                           "id": 8712546,
                           "timestamp": "20140116T123739+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712545,
                           "timestamp": "20140116T123739+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712544,
                           "timestamp": "20140116T123739+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037976,-82.596200",
                           "translatedValue": "28.037976,-82.596200"
                       }
                   ]
               },
               {
                   "id": 2079986,
                   "timestamp": "20140116T123639+0000",
                   "datum": [
                       {
                           "id": 8712514,
                           "timestamp": "20140116T123639+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "78.9",
                           "translatedValue": "199.6 deg F"
                       },
                       {
                           "id": 8712513,
                           "timestamp": "20140116T123639+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712512,
                           "timestamp": "20140116T123639+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712511,
                           "timestamp": "20140116T123639+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037955,-82.596192",
                           "translatedValue": "28.037955,-82.596192"
                       }
                   ]
               },
               {
                   "id": 2079977,
                   "timestamp": "20140116T123539+0000",
                   "datum": [
                       {
                           "id": 8712476,
                           "timestamp": "20140116T123539+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "76.6",
                           "translatedValue": "195.5 deg F"
                       },
                       {
                           "id": 8712475,
                           "timestamp": "20140116T123539+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712474,
                           "timestamp": "20140116T123539+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712473,
                           "timestamp": "20140116T123539+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037959,-82.596177",
                           "translatedValue": "28.037959,-82.596177"
                       }
                   ]
               },
               {
                   "id": 2079973,
                   "timestamp": "20140116T123439+0000",
                   "datum": [
                       {
                           "id": 8712463,
                           "timestamp": "20140116T123439+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "75.0",
                           "translatedValue": "192.6 deg F"
                       },
                       {
                           "id": 8712462,
                           "timestamp": "20140116T123439+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712461,
                           "timestamp": "20140116T123439+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712460,
                           "timestamp": "20140116T123439+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037962,-82.596198",
                           "translatedValue": "28.037962,-82.596198"
                       }
                   ]
               },
               {
                   "id": 2079967,
                   "timestamp": "20140116T123339+0000",
                   "datum": [
                       {
                           "id": 8712437,
                           "timestamp": "20140116T123339+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "72.8",
                           "translatedValue": "188.6 deg F"
                       },
                       {
                           "id": 8712436,
                           "timestamp": "20140116T123339+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712435,
                           "timestamp": "20140116T123339+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712434,
                           "timestamp": "20140116T123339+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037976,-82.596202",
                           "translatedValue": "28.037976,-82.596202"
                       }
                   ]
               },
               {
                   "id": 2079957,
                   "timestamp": "20140116T123239+0000",
                   "datum": [
                       {
                           "id": 8712402,
                           "timestamp": "20140116T123239+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "70.0",
                           "translatedValue": "183.6 deg F"
                       },
                       {
                           "id": 8712401,
                           "timestamp": "20140116T123239+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712400,
                           "timestamp": "20140116T123239+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712399,
                           "timestamp": "20140116T123239+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037980,-82.596212",
                           "translatedValue": "28.037980,-82.596212"
                       }
                   ]
               },
               {
                   "id": 2079949,
                   "timestamp": "20140116T123139+0000",
                   "datum": [
                       {
                           "id": 8712366,
                           "timestamp": "20140116T123139+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "67.8",
                           "translatedValue": "179.6 deg F"
                       },
                       {
                           "id": 8712365,
                           "timestamp": "20140116T123139+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712364,
                           "timestamp": "20140116T123139+0000",
                           "key": "GEN_SPEED",
                           "value": "1.1",
                           "translatedValue": "1.1 mph"
                       },
                       {
                           "id": 8712363,
                           "timestamp": "20140116T123139+0000",
                           "key": "GEN_HEADING",
                           "value": "329",
                           "translatedValue": "329 deg"
                       },
                       {
                           "id": 8712362,
                           "timestamp": "20140116T123139+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037986,-82.596210",
                           "translatedValue": "28.037986,-82.596210"
                       }
                   ]
               },
               {
                   "id": 2079941,
                   "timestamp": "20140116T123039+0000",
                   "datum": [
                       {
                           "id": 8712329,
                           "timestamp": "20140116T123039+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "65.0",
                           "translatedValue": "174.6 deg F"
                       },
                       {
                           "id": 8712328,
                           "timestamp": "20140116T123039+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "13.9",
                           "translatedValue": "13.9V"
                       },
                       {
                           "id": 8712327,
                           "timestamp": "20140116T123039+0000",
                           "key": "GEN_HEADING",
                           "value": "351",
                           "translatedValue": "351 deg"
                       },
                       {
                           "id": 8712326,
                           "timestamp": "20140116T123039+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037966,-82.596160",
                           "translatedValue": "28.037966,-82.596160"
                       }
                   ]
               },
               {
                   "id": 2079933,
                   "timestamp": "20140116T122939+0000",
                   "datum": [
                       {
                           "id": 8712303,
                           "timestamp": "20140116T122939+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "60.5",
                           "translatedValue": "166.5 deg F"
                       },
                       {
                           "id": 8712302,
                           "timestamp": "20140116T122939+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712301,
                           "timestamp": "20140116T122939+0000",
                           "key": "GEN_HEADING",
                           "value": "351",
                           "translatedValue": "351 deg"
                       },
                       {
                           "id": 8712300,
                           "timestamp": "20140116T122939+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037975,-82.596183",
                           "translatedValue": "28.037975,-82.596183"
                       }
                   ]
               },
               {
                   "id": 2079926,
                   "timestamp": "20140116T122839+0000",
                   "datum": [
                       {
                           "id": 8712267,
                           "timestamp": "20140116T122839+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "55.5",
                           "translatedValue": "157.5 deg F"
                       },
                       {
                           "id": 8712266,
                           "timestamp": "20140116T122839+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712265,
                           "timestamp": "20140116T122839+0000",
                           "key": "GEN_SPEED",
                           "value": "3.2",
                           "translatedValue": "3.2 mph"
                       },
                       {
                           "id": 8712264,
                           "timestamp": "20140116T122839+0000",
                           "key": "GEN_HEADING",
                           "value": "351",
                           "translatedValue": "351 deg"
                       },
                       {
                           "id": 8712263,
                           "timestamp": "20140116T122839+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037986,-82.596209",
                           "translatedValue": "28.037986,-82.596209"
                       }
                   ]
               },
               {
                   "id": 2079920,
                   "timestamp": "20140116T122739+0000",
                   "datum": [
                       {
                           "id": 8712243,
                           "timestamp": "20140116T122739+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "50.0",
                           "translatedValue": "147.6 deg F"
                       },
                       {
                           "id": 8712242,
                           "timestamp": "20140116T122739+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712241,
                           "timestamp": "20140116T122739+0000",
                           "key": "GEN_HEADING",
                           "value": "166",
                           "translatedValue": "166 deg"
                       },
                       {
                           "id": 8712240,
                           "timestamp": "20140116T122739+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037970,-82.596211",
                           "translatedValue": "28.037970,-82.596211"
                       }
                   ]
               },
               {
                   "id": 2079914,
                   "timestamp": "20140116T122639+0000",
                   "datum": [
                       {
                           "id": 8712212,
                           "timestamp": "20140116T122639+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "43.9",
                           "translatedValue": "136.6 deg F"
                       },
                       {
                           "id": 8712211,
                           "timestamp": "20140116T122639+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712210,
                           "timestamp": "20140116T122639+0000",
                           "key": "GEN_HEADING",
                           "value": "166",
                           "translatedValue": "166 deg"
                       },
                       {
                           "id": 8712209,
                           "timestamp": "20140116T122639+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037971,-82.596211",
                           "translatedValue": "28.037971,-82.596211"
                       }
                   ]
               },
               {
                   "id": 2079913,
                   "timestamp": "20140116T122539+0000",
                   "datum": [
                       {
                           "id": 8712208,
                           "timestamp": "20140116T122539+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "35.5",
                           "translatedValue": "121.5 deg F"
                       },
                       {
                           "id": 8712207,
                           "timestamp": "20140116T122539+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712206,
                           "timestamp": "20140116T122539+0000",
                           "key": "GEN_SPEED",
                           "value": "22.5",
                           "translatedValue": "22.5 mph"
                       },
                       {
                           "id": 8712205,
                           "timestamp": "20140116T122539+0000",
                           "key": "GEN_HEADING",
                           "value": "166",
                           "translatedValue": "166 deg"
                       },
                       {
                           "id": 8712204,
                           "timestamp": "20140116T122539+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037975,-82.596213",
                           "translatedValue": "28.037975,-82.596213"
                       }
                   ]
               },
               {
                   "id": 2079910,
                   "timestamp": "20140116T122439+0000",
                   "datum": [
                       {
                           "id": 8712191,
                           "timestamp": "20140116T122439+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "22.8",
                           "translatedValue": "98.6 deg F"
                       },
                       {
                           "id": 8712190,
                           "timestamp": "20140116T122439+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.1",
                           "translatedValue": "14.1V"
                       },
                       {
                           "id": 8712189,
                           "timestamp": "20140116T122439+0000",
                           "key": "GEN_SPEED",
                           "value": "23.5",
                           "translatedValue": "23.5 mph"
                       },
                       {
                           "id": 8712188,
                           "timestamp": "20140116T122439+0000",
                           "key": "GEN_HEADING",
                           "value": "330",
                           "translatedValue": "330 deg"
                       },
                       {
                           "id": 8712187,
                           "timestamp": "20140116T122439+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.037493,-82.595962",
                           "translatedValue": "28.037493,-82.595962"
                       }
                   ]
               },
               {
                   "id": 2079908,
                   "timestamp": "20140116T122340+0000",
                   "datum": [
                       {
                           "id": 8712185,
                           "timestamp": "20140116T122340+0000",
                           "key": "GEN_ENGINE_COOLANT_TEMP",
                           "value": "83.9",
                           "translatedValue": "208.6 deg F"
                       },
                       {
                           "id": 8712184,
                           "timestamp": "20140116T122340+0000",
                           "key": "GEN_VOLTAGE",
                           "value": "14.0",
                           "translatedValue": "14.0V"
                       },
                       {
                           "id": 8712183,
                           "timestamp": "20140116T122340+0000",
                           "key": "GEN_HEADING",
                           "value": "326",
                           "translatedValue": "326 deg"
                       },
                       {
                           "id": 8712182,
                           "timestamp": "20140116T122340+0000",
                           "key": "GEN_WAYPOINT",
                           "value": "28.036539,-82.593698",
                           "translatedValue": "28.036539,-82.593698"
                       }
                   ]
               }
           ]
       },
       "totalRecords": 27,
       "actions": []
   }
