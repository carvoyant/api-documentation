Account
=======

The Account object represents a unique account within the Carvoyant system.

*Properties*

+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| Property         | Type     | Description                                                                            | Required for Creation |
+==================+==========+========================================================================================+=======================+
| id               | Integer  | The internal system identifier for this vehicle.                                       | Unsupported           |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| firstName        | String   | The first name on the account.                                                         | Required              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| lastName         | String   | The last name on the account.                                                          | Required              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| dateCreated      | DateTime | The timestamp of when the account was created.                                         | Unsupported           |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| zipcode          | String   | The zipcode where the user primarily drives.                                           | Required              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| email            | String   | Email address for the account.                                                         | Optional              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| phone            | String   | Phone number for the account.                                                          | Optional              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| timeZone         | String   | The timezone to use for time display.                                                  | Required              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| preferredContact | String   | How the account owner prefers to be contacted.                                         | Required              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| accessToken      | String   | A Bearer access token to use to access this account. Note that an access token is only | Unsupported           |
|                  |          | returned by the creation of a new account.                                             |                       |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| username         | String   | The username for the account.                                                          | Required              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+
| password         | String   | The password for the account.                                                          | Required              |
+------------------+----------+----------------------------------------------------------------------------------------+-----------------------+

*Supported Verbs*

   * GET
   * POST
   * DELETE

GET
---

Returns one or more accounts.

*Query Paths*

   * /account/
   * /account/{account-id}

*Query Parameters*

   +------------+------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                    |
   +============+================================================================================================+
   | account-id | The Carvoyant identifier of the account. If the account-id is not specified, then all accounts |
   |            | available will be returned. In most cases, only one account is available so both calls         |
   |            | will return the same account.                                                                  |
   +------------+------------------------------------------------------------------------------------------------+

*Call Options*

   +----------+----+
   | Sortable | No |
   +----------+----+
   | Pageable | No |
   +----------+----+

*Sample JSON Response*::

   {
       "account": {
           "id: 3
           "firstName": "Speed"
           "lastName": "Racer"
           "username": "speedracer"
           "dateCreated": "20121130T144013+0000"
           "email": "speedracer@noemail.com"
           "zipcode": "33635"
           "phone": "8135551212"
           "timeZone": "America/New_York"
           "preferredContact": "PHONE"
       }
       totalRecords: null
       actions: [ ]
   }

POST
----

Creates or updates an account. Note that the client credentials authentication mechanism must be used for account creation. User account access tokens are not authorized to create new accounts. In the response to the creation of a new response, an OAuth2 authorization code will be provided. The calling system can use that authorization code to retrieve an access token for the new account without required the user to explicitly grant access (creating the account assumes access has been granted).

*Query Paths*

   * /account/
   * /account/{account-id}

*Query Parameters*

   +------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                                   |
   +============+===============================================================================================================+
   | account-id | The Carvoyant identifier of the account. If the account-id is not specified, a new account will be created.   |
   |            | If it is specified, then any account fields specified in the request will be updated. Unspecified fields will |
   |            | remain unchanged.                                                                                             |
   +------------+---------------------------------------------------------------------------------------------------------------+

*Sample JSON Response*::

   {
       account: {
           id: 87
           firstName: "Speed"
           lastName: "Racer"
           username: null
           dateCreated: "20140505T173906+0000"
           email: "matt@carvoyant.com"
           zipcode: "33635"
           phone: null
           timeZone: null
           preferredContact: "EMAIL"
           accessToken: {
               code: "2f2w4ae6mmbvrdk94feen2gy"
           }
       }
       totalRecords: null
       actions: [ ]
   }

DELETE
------

Deletes the specified account.

.. warning::

   This operation is permanent! All data and configuration for the account, including all of it's vehicles will be deleted and
   cannot be restored. Please ensure that the Carvoyant account owner confirms this operation before making the API call.
   
*Query Paths*

   * /account/{account-id}

*Query Parameters*

   +------------+------------------------------------------+
   | Parameter  | Description                              |
   +============+==========================================+
   | account-id | The Carvoyant identifier of the account. |
   +------------+------------------------------------------+

*Sample JSON Response*::

   {
       "result": "OK",
       "totalRecords": 1,
       "actions": []
   }
