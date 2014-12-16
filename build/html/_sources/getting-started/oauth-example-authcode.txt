Authorization Code
==================

The first step is to request the authorization from the user. This call will return a redirect to the login page.

*Authorize Request*::

   curl -i -X GET -d "client_id=pekfaf6jxk6suyXXXXXXXXXX" --data-urlencode "redirect_uri=http://test.carvoyant.com/" -d "response_type=code" "https://auth.carvoyant.com/OAuth/authorize"
   
   HTTP/1.1 302 Found
   Content-Type: text/plain; charset=UTF-8
   Date: Mon, 28 Apr 2014 14:03:51 GMT
   Location: https://auth.carvoyant.com/login/auth
   Server: Apache-Coyote/1.1
   Set-Cookie: JSESSIONID=2D3C7E5AA412DF98124B8AC7121FEF7D; Path=/; Secure; HttpOnly
   Content-Length: 0
   Connection: keep-alive

If you did this through a browser, the login screen would appear to the user:

.. image:: auth-dialog.png

After logging in, the user will be redirected to the redirect_url specified in the authorization request with the authorization code appended to it.  For the request above, the redirect uri would look like:::

   http://test.carvoyant.com/?code=v369uars628mgkXXXXXXXXXX

From this response, the server running at test.carvoyant.com would parse the authorization code and make a request to the token endpoint to read an actual access token.  Note that this request requires the client id and secret key for the development partner to be passed as the Basic Authentication credentials.

*Access Token Request*::

   curl -i --user pekfaf6jxk6suyXXXXXXXXXX:XXXXXXXXXX -d "grant_type=authorization_code" -d "code=v369uars628mgkXXXXXXXXXX" --data-urlencode "redirect_uri=http://test.carvoyant.com/" "https://api.carvoyant.com/oauth/token"

The response will include a json body with the access token information.

*Access Token Response*::

   HTTP/1.1 200 OK
   Cache-Control: no-store
   Content-Type: application/json;charset=UTF-8
   Date: Mon, 28 Apr 2014 14:24:34 GMT
   Server: Mashery Proxy
   X-Mashery-Responder: prod-j-worker-us-east-1c-31.mashery.com
   Content-Length: 161
   Connection: keep-alive
   {
       "token_type":"bearer",
       "mapi":"pekfaf6jxk6suyXXXXXXXXXX",
       "access_token":"dmnda67wbdnyayXXXXXXXXXX",
       "expires_in":86400,
       "refresh_token":"f2hqes6fpg37d2XXXXXXXXXX"
   }

At this point, the development partners system would store the access token and refresh token and use them for future requests.
