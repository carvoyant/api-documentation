Access & Registration Workflows
===============================

When a partner creates an application for the Carvoyant platform, it is necessary to handle two different user scenarios.  In the first scenario, the end user does not already have a Carvoyant account and needs to be registered with the Carvoyant platform.  In the second scenario, the user already has a Carvoyant account and simply wants to connect the partners application to their account. This poses some questions regarding how the Carvoyant account is created (when necessary), how Carvoyant validates that the user has granted access to the partner application and how the partner uses that access.  If you are not already familiar with the OAuth mechanism used in the Carvoyant Platform, please read that first.

Scenario 1 - New Carvoyant Account
----------------------------------

In many cases, our partners will be bringing on new Carvoyant users to our platform as a part of their application.  Perhaps you are creating a brand new connected car application.  Or maybe you're simply adding connected car features to your existing application.  In either case, it is necessary to create the Carvoyant user account.  This can be done two ways. First, you can just treat the "new" and "existing" customers the exact same way.  You simply prompt them to authorize Carvoyant to access their account and then take them to our authentication server as outlined in our OAuth documentation.  If you want to use this method, please see Scenario 2.

If you don't want to require the user to go through the Carvoyant UI for account creation, you can simply call the account creation API endpoint in our system. You will need to pass over all of the required fields for a new account.  The response to the account creation call will include an authorization code.  That code can then be used to programmatically generate the access token.  An example request flow looks like this:

Account Creation Request::

   curl -X POST -H 'Authorization: Bearer m7dwthfgv9dvdpxXXXXXXXXX' -H 'Content-Type: application/json' https://sandbox-api.carvoyant.com/sandbox/api/account/ -d '{"firstName": "Doc","lastName": "Test","email": "matt@carvoyant.com","username": "doctest","password": "doctestpassword"}'