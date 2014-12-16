OAuth2 / Delegated Access
=========================

The Carvoyant system uses an `OAuth2 <http://tools.ietf.org/html/rfc6749>`_ implementation in order to allow users to delegate access to the applications that they want to use.  All four of the `Authorization Grant types <http://tools.ietf.org/html/rfc6749#section-1.3>`_ have been implemented, however, only Authorization Code, Implicit and Client Credentials are available to our standard development partners.  If you need to support the Resource Owner type, please contact us to discuss.

Here is a brief summary of how you will use each of the grant types when accessing the Carvoyant system.  Please refer to the specification for details on each grant type.

+-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
| Grant Type                                                                              | Usage                                                                                                                               |
+=========================================================================================+=====================================================================================================================================+
| `Authorization Code <http://tools.ietf.org/html/draft-ietf-oauth-v2-20#section-1.4.1>`_ | This type will be used in the scenario where the system making the actual API call is in a secured environment. For example,        |
|                                                                                         | web applications where the Carvoyant API call originates from our partners server will use this method. The development partner     |
|                                                                                         | will direct the user to a Carvoyant hosted web page where the user will log in and grant access to the development partner. The     |
|                                                                                         | Carvoyant system will redirect the user back to an endpoint that the development partner hosts which will contain an authorization  |
|                                                                                         | code. The development partner will then make a request from their controlled environment to retrieve an access token to the users   |
|                                                                                         | Carvoyant data. That call will be a server to server call over SSL and will require the development partners credentials. The       |
|                                                                                         | response will include an access token and a refresh token per the OAuth2 specification. This is the preferred grant type as it      |
|                                                                                         | provides the highest level of security in the token negotiation process.                                                            |
+-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
| `Implicit <http://tools.ietf.org/html/draft-ietf-oauth-v2-20#section-1.4.2>`_           | This type will be used when the calls into the Carvoyant system are made from an insecure environment. The primary example for this |
|                                                                                         | use case is a mobile application. In this process, the development partners application (typically running on a resource controlled |
|                                                                                         | by the user) directs the user to a Carvoyant hosted web page where the user will log in and grant access to the development         |
|                                                                                         | partner. The Carvoyant system will redirect the user back to an endpoint that the development partner specifies. That redirect will |
|                                                                                         | contain the access token per the OAuth2 specification. In this grant type, refresh tokens are not provided.                         |
+-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
| `Client Credentials <http://tools.ietf.org/html/draft-ietf-oauth-v2-20#section-1.4.3>`_ | There are a few calls into the Carvoyant API that the development partner will make that does not require a user access token. A    |
|                                                                                         | primary example of this is the call to register a new account. Since the account does not exist yet, there is no user to grant      |
|                                                                                         | access. API calls using this grant type will still expect an access token, but that token will be requested using only the          |
|                                                                                         | development partners credentials.                                                                                                   |
+-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+

.. warning::
   **Configuration Requirements**

   In order to ensure the security of the OAuth2 process, there are two requirements that must be met. When you registered your application, one of the fields that you were asked for was the "Register Callback URL".  This is the URL that the OAuth2 process will redirect users back to after they authorize your application.  Specifically, it is the value of the redirect_uri in all of the below examples.  There are two important aspects to this

   #. The value MUST be an SSL protected URL of the form https://... and the certificate must be signed by a trusted certificate authority (ie, self signed certificates are not supported).
   #. All requests that are made into the OAuth2 process must use that value for the redirect_uri. Mismatched values will generate errors and will result in an access token not being generated.
   
   If you need to change this value, or are unsure of what it is set to, you can access it by logging into the `Developer Console <https://developer.carvoyant.com/>`_ and selecting "My Account" in the top right.  This will let you access any applications that you have created keys for.
   
Examples
--------

Below are example calls using cURL to show how to generate tokens under each grant type.

Authorization Code
~~~~~~~~~~~~~~~~~~

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

Implicit
~~~~~~~~

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

Client Credentials
~~~~~~~~~~~~~~~~~~

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
