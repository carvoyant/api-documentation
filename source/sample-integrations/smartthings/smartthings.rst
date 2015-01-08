SmartThings
===========

Overview
--------

At the end of this walk through, you will have added your Carvoyant enabled connected car to your SmartThings connected home. This will be a step-by-step instruction but it does assume some familiarity with the SmartThings ide and the standard nomenclature that SmartThings uses.  Specifically, you will be creating a custom device type and two custom SmartApps.

All of the code referenced here can be found in our `SmartThings Github repository <https://github.com/carvoyant/SmartThings>`_ .

The following SmartThings objects will be created:

carvoyant: Connected Car Device Type
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This device type will support the "sensor" and "presenceSensor" capabilities and will have a custom attribute representing the ignition status of the vehicle. This device type will be used to create a ``thing`` representing your vehicle.

carvoyant: Connected Car Setup SmartApp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This SmartApp is a service manager SmartApp that allows the Carvoyant system and the SmartThings cloud to communicate with each other.

carvoyant: Carvoyant Actions SmartApp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This SmartApp is used to configure events from your Connect Car device.

Pre-requisites
--------------

Carvoyant Developer Account
~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you do not already have one, you will need to register a Carvoyant developer account.  Refer to our :doc:`/getting-started/index` guide.  You will need to decide whether to connect to the Carvoyant sandbox or production environment. It's easiest to test things using the sandbox environment so that's what we will assume in this guide.

Once you have a developer account, you will need to create a Carvoyant client id for your SmartThings application.  Follow the instructions for creating a sandbox application :doc:`here </sandbox-api/index>` .

After your sandbox application is created, register a driver account at https://sandbox-driver.carvoyant.com and add a vehicle to it. Get familiar with simulating data against your sandbox account as described in the :doc:`/sandbox-api/index` . Confirm that you can make API calls using the `Interactive API <https://developer.carvoyant.com/io-docs>`_ .

SmartThings Account
~~~~~~~~~~~~~~~~~~~

Create a SmartThings account for their online IDE `here <https://graph.api.smartthings.com/>`_ .

A Carvoyant connected vehicle is what SmartThings refers to as a *Cloud-Connected Device Type*. These are devices that the SmartHub does not directly interact with. If you are not familiar with this functionality within SmartThings, we suggest you read over their `documentation <http://docs.smartthings.com/en/latest/cloud-and-lan-connected-device-types-developers-guide/building-cloud-connected-device-types/index.html>`_ .

SmartThings Setup
-----------------

Custom Device Type
~~~~~~~~~~~~~~~~~~

Within the SmartThings IDE, navigate to *My Device Types* and add a new device type. Select *From Code* and paste in the contents of `ConnectedCar.groovy <https://github.com/carvoyant/SmartThings/blob/master/ConnectedCar.groovy>`_ .  This will create the device type that represents a Carvoyant enabled car. Save and then *Publish* the new device type.

Service Manager SmartApp
~~~~~~~~~~~~~~~~~~~~~~~~

After creating the device type, change to the *My SmartApps* section within the SmartThings IDE and add a new SmartApp. Select *From Code* and paste in the contents of TOBEDETERMINED.  This creates the initial SmartApp to interact with Carvoyant.

Once the service manager is created, go back into it and select the *App Settings* button.  On the *Edit* screen, select the *Settings* section.  You will need to populate following four settings:

+-------------------+----------------------------------------------------------------------------------------+
| Name              | Value                                                                                  |
+===================+========================================================================================+
| carvoyantApiUrl   | The Carvoyant API URL. For now, enter ``https://sandbox-api.carvoyant.com``            |
+-------------------+----------------------------------------------------------------------------------------+
| carvoyantAuthUrl  | The Carvoyant Authorization URL. For now, enter ``https://sandbox-auth.carvoyant.com`` |
+-------------------+----------------------------------------------------------------------------------------+
| carvoyantClientId | This is the Client Id for the Carvoyant Sandbox Application that you created.          |
+-------------------+----------------------------------------------------------------------------------------+
| carvoyantSecret   | This is the Secret for the specified Client Id.                                        |
+-------------------+----------------------------------------------------------------------------------------+

Save your changes and then *Publish* the SmartApp.

Carvoyant Actions SmartApp
~~~~~~~~~~~~~~~~~~~~~~~~~~

The SmartApp that we will be creating will tell the Carvoyant system to notify SmartThings of several different events for your vehicle:

   * Arrival - An event will be triggered indicating that the vehicle has arrived at the current SmartThings selected location.
   * Departure - An event will be triggered indicating that the vehicle has left the current SmartThings selected location.
   * Ignition On - An event will be triggered indicating that the vehicle has been turned on.
   * Ignition Off - An event will be triggered indicating that the vehicle has been turned off.

.. note::

   These events are just a few of the events that can be triggered.  Any event notification generated by the Carvoyant system can be tied into the SmartThings system.  See below on how to extend these SmartApps.

Go into the *My SmartApps* section within the SmartThings IDE and add a new SmartApp. Select *From Code* and past in the contents of TOBEDETERMINED. There is no configuration needed so just Save and *Publish* the SmartApp.

Get Everything Running
----------------------

At this point, all of the necessary items have been created in your SmartThings environment. Now it's time to hook it all up.  For this example we have a set of Philips Hue lights that are controlled by our SmartHub. We are going to configure our office so that one light is on or off depending on the ignition status of the vehicle and another light on or off depending on the presence of the vehicle.

Install the Connected Car Setup SmartApp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Open the SmartThings mobile application and select the + icon at the bottom. Swipe right until you get to *My Apps*. You should see the two Carvoyant SmartApps available. Select *Connected Car Setup*.

<INSERT IMAGE>

First you must authorize Carvoyant to share data with SmartThings.  Select *Carvoyant Authorization*. This will open up a log in screen in the Carvoyant sandbox environment.  Log in with the driver account credentials that you created earlier. These are the same credentials you used to log in to https://sandbox-driver.carvoyant.com.

<INSERT IMAGE>
