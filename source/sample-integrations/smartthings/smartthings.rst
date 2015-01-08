SmartThings
===========

Overview
--------

At the end of this walk through, you will have added your Carvoyant enabled connected car to your SmartThings connected home. This will be a step-by-step instruction but it does assume some familiarity with the SmartThings ide and the standard nomenclature that SmartThings uses.  Specifically, you will be creating a custom device type and two custom SmartApps.

All of the code referenced here can be found in our Github repository.

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

If you do not already have one, you will need to register a Carvoyant developer account.  Refer to our :doc:`Getting Started </getting-started>`_ guide.  You will need to decide whether to connect to the Carvoyant sandbox or production environment. It's easiest to test things using the sandbox environment so that's what we will assume in this guide.

Once you have a developer account, you will need to create a Carvoyant client id for your SmartThings application.  Follow the instructions for creating a sandbox application :doc:`here </sandbox-api>`_ .

SmartThings Account
~~~~~~~~~~~~~~~~~~~

Create a SmartThings account for their online IDE `here <https://graph.api.smartthings.com/>`_ .