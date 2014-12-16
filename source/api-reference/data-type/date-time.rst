DateTime
========

All timestamps will be returned in the `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_ standard format (``yyyyMMddTHHmmssZ``).

   * yyyy : 4 digit year
   * MM : 2 digit month
   * dd : 2 digit day
   * HH : hour (on a 24 hour scale)
   * mm : minutes
   * ss : seconds
   * Z : timezone offset

Implementations should honor the timezone but in most cases all timestamps will be returned in UTC with a timezone offset of +0000 (we expect and use the +0000 offset for UTC rather than the Z shorthand that the spec provides for).

For example, the string ``20130526T204840+0000`` denotes ``May 26, 2013 at 8:48 and 40 seconds, PM, in UTC``.