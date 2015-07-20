Using the Refresh Token
=======================

When using the Authorization Code grant type, you will receive a refresh token in addition to the access token. Any time up until the expiration of the refresh token (currently 30 days past the access token expiration), you can generate a new access token without requiring the user to go through the authorization process.
