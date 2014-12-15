Access & Registration Workflows
===============================

.. toctree::
   :hidden:
   :maxdepth: 3

When a partner creates an application for the Carvoyant platform, it is necessary to handle two different user scenarios.  In the first scenario, the end user does not already have a Carvoyant account and needs to be registered with the Carvoyant platform.  In the second scenario, the user already has a Carvoyant account and simply wants to connect the partners application to their account. This poses some questions regarding how the Carvoyant account is created (when necessary), how Carvoyant validates that the user has granted access to the partner application and how the partner uses that access.  If you are not already familiar with the OAuth mechanism used in the Carvoyant Platform, please read that first.

Scenario 1 - New Carvoyant Account
----------------------------------

In many cases, our partners will be bringing on new Carvoyant users to our platform as a part of their application.  Perhaps you are creating a brand new connected car application.  Or maybe you're simply adding connected car features to your existing application.  In either case, it is necessary to create the Carvoyant user account.  This can be done two ways. First, you can just treat the "new" and "existing" customers the exact same way.  You simply prompt them to authorize Carvoyant to access their account and then take them to our authentication server as outlined in our OAuth documentation.  If you want to use this method, please see Scenario 2.

If you don't want to require the user to go through the Carvoyant UI for account creation, you can simply call the account creation API endpoint in our system. You will need to pass over all of the required fields for a new account.  The response to the account creation call will include an authorization code.  That code can then be used to programmatically generate the access token.  An example request flow looks like this:

*Account Creation Request*::

   curl -X POST -H 'Authorization: Bearer m7dwthfgv9dvdpxXXXXXXXXX' -H 'Content-Type: application/json' https://sandbox-api.carvoyant.com/sandbox/api/account/ -d '{"firstName": "Doc","lastName": "Test","email": "matt@carvoyant.com","username": "doctest","password": "doctestpassword"}'

*Account Creation Response*::

   {
       "account":{
           "id":166,
           "firstName":"Doc",
           "lastName":"Test",
           "username":null,
           "dateCreated":"20141112T195503+0000",
           "email":"matt@carvoyant.com",
           "zipcode":null,
           "phone":null,
           "timeZone":null,
           "preferredContact":null,
           "accessToken":{
               "code":"dj6fpxdbkh3xqyXXXXXXXXXX"
           }
       },
       "totalRecords":1
   }

Note the ``accessToken.code`` in the response.

Now lets get the access token:

*Access Token Request*::

   curl --user r6dwmz2zxkqms7sac2r8mdqa:XXXXXXXXXX -d "grant_type=authorization_i=https://test.carvoyant.com" "https://sandbox-api.carvoyant.com/sandbox/oauth/token"

*Access Token Response*::

   {
       "access_token":"6dpmu7c4gv3s3yXXXXXXXXXX",
       "token_type":"bearer",
       "expires_in":86400,
       "refresh_token":"z9h69fqx4cdkfjXXXXXXXXXX"
   }

Now you've successfully registered a new Carvoyant account and generated an access token into the API for that user without requiring the user manually log in.

.. note::

   Accounts created in this way make it very easy for the end user to misunderstand who is collecting their data and who is storing it.  If you are generating accounts and access tokens for Carvoyant users in this manner, you must notify them of the following:

   #. Their Carvoyant user credentials (ie, the username and password that was passed in to the account creation).
   #. A link to https://driver.carvoyant.com where the user can access their Carvoyant account.
   #. A clear statement that their connected car data is being collected on their behalf by Carvoyant and made available to you, our partner.

If there are any questions about this, please contact us: `contact us <support@carvoyant.com>`_.

Scenario 2 - Existing Carvoyant User (or using the Carvoyant new account UI)
----------------------------------------------------------------------------

As the Carvoyant user base grows, connected users are going to want to connect more and more applications to their connected car.  In order to do this, application providers need to allow those users to authorize the partner's application to the user's Carvoyant account.  This is done by using our authorization server.  Note that this process is also outlined on our OAuth2 / Delegated Access documentation.

When the you are ready to have your user authorize you to their Carvoyant account, you simply open a browser and redirect them to our authorization page.  The URL looks like this:::

   https://sandbox-auth.carvoyant.com/OAuth/authorize?client_id=r6dwmz2zxkqms7XXXXXXXXXX&redirect_uri=https%3A%2F%2Ftest.carvoyant.com&response_type=token

Replace the ``client_id`` with your applications client_id and the ``redirect_uri`` with the URL that you will listen on for the response.  The user will be presented with a screen like this:

.. image:: auth-dialog.png

Note that the user can log in with their existing credentials or they can register a new one right there.  From a partner's perspective, you can simply provide a "Connect Carvoyant" action and this will solve the integration for both new Carvoyant users and already existing Carvoyant users.  After the user logs in and authorizes access, they will be redirected back to the URL you specified in the redirect_uri parameter and it will include the authorization code.  The URL will look like this:::

   https://test.carvoyant.com?code=dj6fpxdbkh3xqyXXXXXXXXXX

The code query parameter in that URL is the authorization code that is used to request the access token.  That process is identical to what is outlined above.  Note that this example is using the authorization code grant type.  The same process can be followed for the ``implicit`` grant type.