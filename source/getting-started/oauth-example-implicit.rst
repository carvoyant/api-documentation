Implicit
========

The first step is to request the authorization from the user. This call will return a redirect to the login page.

*Authorize Request*::

   curl -i -X GET -d "client_id=pekfaf6jxk6suyXXXXXXXXXX" --data-urlencode "redirect_uri=http://test.carvoyant.com/" -d "response_type=token" "https://auth.carvoyant.com/OAuth/authorize"
   
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

After logging in, the user will be redirected to the redirect_url specified in the authorization request with the access token appended to it.  For the request above, the redirect uri would look like:::

   http://test.carvoyant.com/?access_token=2pr9tvk3vgnr9aXXXXXXXXXX&token_type=bearer&expires_in=86400

From this response, the endpoint at test.carvoyant.com would parse the access token and begin making API calls.