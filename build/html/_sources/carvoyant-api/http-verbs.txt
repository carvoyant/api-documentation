HTTP Verbs
==========

One of the recurring areas of confusion around APIs that strive to be RESTful has to do with the mapping of HTTP verbs to actual server side actions.  Here are some guidelines for how the Carvoyant API handles the various verbs for different resource types.

+--------+--------------------------------------------------------------------------+-------------------------------------------------------------------------+
| Verb   | Container (e.g. /vehicle)                                                | Entity (e.g. /vehicle/{id})                                             |
+========+==========================================================================+=========================================================================+
| GET    | Returns a list of all entities in the container.                         | Returns the specified entity.                                           |
+--------+--------------------------------------------------------------------------+-------------------------------------------------------------------------+
| PUT    | Currently not supported for any container type. In practice, this would  | Replaces the specified entity.                                          |
|        | replace the entire container with the entities specified in the request. |                                                                         |
+--------+--------------------------------------------------------------------------+-------------------------------------------------------------------------+
| POST   | Creates a new entity within the container.                               | Updates the specified entity. Only data elements included in            |
|        |                                                                          | the request will be updated. Non-specifiied fields will not be changed. |
+--------+--------------------------------------------------------------------------+-------------------------------------------------------------------------+
| DELETE | Currently not supported for any container type. In practice, this would  | Deletes the specified entity.                                           |
|        | delete all entities in the container.                                    |                                                                         |
+--------+--------------------------------------------------------------------------+-------------------------------------------------------------------------+
