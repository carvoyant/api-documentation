Client Credentials
==================

In this grant type, there is no user interaction. The development partner requests a token for their client credentials directly.

*Access Token Request*::

   curl -i --user pekfaf6jxk6suyXXXXXXXXXX:XXXXXXXXXX -d "grant_type=client_credentials" "https://api.carvoyant.com/oauth/token"

The response will include a json body with the access token information.

*Access Token Response*::

   HTTP/1.1 200 OK
   Cache-Control: no-store
   Content-Type: application/json;charset=UTF-8
   Date: Mon, 28 Apr 2014 14:57:20 GMT
   Server: Mashery Proxy
   X-Mashery-Responder: prod-j-worker-us-east-1d-32.mashery.com
   Content-Length: 161
   Connection: keep-alive
   {
       "token_type":"bearer",
       "mapi":"pekfaf6jxk6suyXXXXXXXXXX",
       "access_token":"n45u7eufgdmfysXXXXXXXXXX",
       "expires_in":86400,
       "refresh_token":"r9acw76k327g3cXXXXXXXXXX"
   }

At this point, the development partners system would store the access token and refresh token and use them for future requests.