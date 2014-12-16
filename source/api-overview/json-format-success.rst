JSON Success Response Format
============================

Responses from the Carvoyant system will follow a common structure for all API calls.  The general format will be:::

   {
       "<object name>":
           [
               {<object 1>},
               {<object 2>},
               {<object 3>}
           ],
       "totalRecords": <total records>,
       "actions":
           [
               {
                   "name": "<action1 name>",
                   "uri": "<action1 uri>"
               },
               {
                   "name": "<action2 name>",
                   "uri": "<action2 uri>"
               },
           ]
   }
   
``<object name>`` will be defined by the specific API call that is made.  In cases where a list is returned, the object value will be an array.  If a single object is returned then the object value will just be the object (it will not be a single element array).  The "actions" array will include any subsequent API calls that can be made related to the returned object (this is our first pass at implementing `HATEOAS <https://en.wikipedia.org/wiki/HATEOAS>`_ ).  We decided to standardize the payload format rather then rely on something like the HTTP Link header for passing back available actions.

Note that the ``totalRecords`` property will only be present when the object returned is a list.  The value of ``totalRecords`` will be the total count of records contained within the Carvoyant system.  It will not be the number of records returned in the response.  This will be useful with returned data that is paged.  For instance, the system might have 115 records stored but the pagination parameters may only return 20 records in this particular response.  In that scenario, the totalRecords value will be 115.