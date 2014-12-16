Waypoint
========

A waypoint is a GPS location at a specific point in time.

*Properties*

+---------------+----------+-----------------------------------------+----------+
| Property Name | Type     | Description                             | Optional |
+===============+==========+=========================================+==========+
| timestamp     | DateTime | The time that the location was recorded | N        |
| latitude      | Float    | The latitude of the location            | N        |
| longitude     | Float    | The longitude of the location           | N        |
+---------------+----------+-----------------------------------------+----------+

*JSON Sample*::

   {
       "timestamp":"20140116T152440+0000",
       "latitude":28.088445,
       "longitude":-82.578451
   }
