Carvoyant API
=============

The Carvoyant API is a RESTful web API that allows our customers and partners to access Carvoyant data programmatically.  All API calls must be made over SSL and access into the system is controlled by an OAuth2 implementation.  The URI to access the API is https://api.carvoyant.com/v1/api.  Every request is expected to include the Authorization header containing the bearer token generated through one of the OAuth2 grant types.  See :doc:`OAuth2 / Delegated Access <../getting-started/oauth2-delegated-access>` for details on how to request an access token.

In following along with the standard approach for a RESTful service, our API is structured in terms of it's Resources.  So you won't see "actions" listed in here.  Instead, you will find the information organized in terms of the resources that the Carvoyant API exposes.  For each resource, you will find a description of the object as well as the various requests that can be made against it (ie, GET, PUT, POST, DELETE).

.. toctree::
   :maxdepth: 3
   
   json-format-success
   json-format-error
   http-verbs
   sorting-and-paging