Using the Refresh Token
=======================

When using the Authorization Code grant type, you will receive a refresh token in addition to the access token. Any time up until the expiration of the refresh token (currently 30 days past the access token expiration), you can generate a new access token without requiring the user to go through the authorization process.

*Request*::

   curl -i -H "Authorization: Bearer dmnda67wbdnyayXXXXXXXXXX" "https://api.carvoyant.com/v1/api/vehicle/"

*Response*::

   HTTP/1.1 200 OK
   Content-Type: application/json;charset=UTF-8
   Date: Mon, 28 Apr 2014 15:06:47 GMT
   Server: Apache-Coyote/1.1
   X-Mashery-Responder: prod-j-worker-us-east-1b-36.mashery.com
   Content-Length: 1205
   Connection: keep-alive
   {"vehicle":[{"name":"1999 Jeep Wrangler SE","label":"Custom dune buggy","vehicleId":3,"deviceId":"C201200001","vin":"1J4FY29P7XP442798","mileage":160854.0,"lastWaypoint":{"timestamp":"20140428T144739+0000","latitude":28.036441,"longitude":-82.593687},"running":false,"lastRunningTimestamp":"20140428T113035+0000"},{"name":"Unidentified Vehicle","label":null,"vehicleId":4,"deviceId":null,"vin":null,"mileage":162151.0,"lastWaypoint":{"timestamp":"20131112T231526+0000","latitude":28.036473,"longitude":-82.593671},"running":false,"lastRunningTimestamp":"20131110T190222+0000"},{"name":"2000 Chevrolet Corvette Hardtop","label":null,"vehicleId":123,"deviceId":"4562001045","vin":"1G1YY22G2Y5108919","mileage":111940.0,"lastWaypoint":{"timestamp":"20140428T143141+0000","latitude":28.088404,"longitude":-82.578463},"running":false,"lastRunningTimestamp":"20140428T123141+0000"},{"name":"2013 Subaru XV Crosstrek Limited","label":null,"vehicleId":284,"deviceId":"C201200002","vin":"JF2GPAKC5D2889395","mileage":9156.0,"lastWaypoint":{"timestamp":"20140428T142731+0000","latitude":27.991497,"longitude":-82.406288},"running":false,"lastRunningTimestamp":"20140428T111028+0000"}],"totalRecords":4,"actions":[]}
