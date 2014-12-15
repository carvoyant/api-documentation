Getting Started
===============

.. toctree::
   :maxdepth: 2
   :hidden:
   
   oauth2-delegated-access
   access-registration
   
Overview
--------

Before accessing the Carvoyant system as a developer, you must first register on our developer portal.  After your account is registered, you will be able to make calls into our system.  One of our main philosophies is that our users have full control over who can access the data for their vehicles.  In order to facilitate this, nearly all calls that a developer makes into the system requires an `OAuth2 <http://tools.ietf.org/html/draft-ietf-oauth-v2-20>`_ access token that the end user has granted.  Once a token has been granted, the various Carvoyant resources will be accessible through the API.

Developer Registration
----------------------

The first step in building an application for the Carvoyant system is to register with us as a developer.  We have several different developer levels depending on your interest.  You can view the different developer levels and associated pricing `here <https://developer.carvoyant.com/pricing>`_ or you can just go register `here <https://developer.carvoyant.com/member/register>`_.

During registration you will enter in some basic information about your application and you will be given an API key to use in your application.  Please only create a Standard Developer key if you are also purchasing a developer device or already have a Carvoyant enable vehicle.  A free Trial key is available if you are just taking a look.

Sandbox Access
--------------

In order to allow developers to try out our system, or even just develop against a non-production environment, we've created a Sandbox version of our API.  This environment matches our production environment with two important distinctions.  First, it is not possibly to connect a live vehicle to an account in this system.  All of the data in this system is "fake".  Second, all developers have the ability to call an endpoint that allows them to create their own vehicle data.  In this way, you can programmatically generate the vehicle data that you need to test your application.  Review the information about the Sandbox API to get started.

Paid Standard Developer Accounts
--------------------------------

Every paid Standard Developer account also includes one telematics device to connect your car to the Carvoyant platform.  Before that the data for your car can be accessed, you must register as a Carvoyant user `here <https://driver.carvoyant.com>`_ (this can also be done through an API call).  It's important to recognize the difference between a developer account and a user account.  Developer accounts are authorized to make API calls against the Carvoyant platform.

Developer vs. User Accounts
---------------------------

When working with the Carvoyant platform, it's very important to understand the difference between Developer accounts and User accounts.  A Developer account is registered through https://developer.carvoyant.com and is what you will use to interact with the Carvoyant API. A User account is registered with the Carvoyant platform (either programmatically through the /account endpoint, or on the driver dashboard at https://driver.carvoyant.com ).  User accounts contain the vehicles which contain the data collected by the telematics device.

All Carvoyant Users can create a Developer account to access their own connected car data.

Making an API Call
------------------

The best way to get familiar with our API is to jump in and start using it.  Using our `interactive documentation <https://developer.carvoyant.com/io-docs>`_, you can start calling the API directly.

We've also added a couple of sample applications to our GitHub repository.

`Car-Locator <https://github.com/carvoyant/Car-Locator>`_ is an Android application that uses the Implicit grant type to authenticate a user.  Once logged in, it displays a map of the users Carvoyant enabled vehicles.

`Example-Carvoyant-Web-App <https://github.com/carvoyant/Example-Carvoyant-Web-App>`_ is a Grails web application that uses it's own security model to authenticate it's application users and then lets that user connect to their Carvoyant account.  This application uses the Authorization Code grant type.
