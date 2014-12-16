JSON Error Response Format
==========================

API calls that result in an error will have a different format than successful message.  The first difference is that the HTTP response code will not be 200.  It will be an HTTP code more reflective of the error encountered.  For example, a 404 will be returned if a resource that does not exist is requested.  The body of the response will contain the following JSON response format:::

   {
       "error":
           {
               "httpStatus": <http status code>,
               "detail": "<string message>"
           }
   }