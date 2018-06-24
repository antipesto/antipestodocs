.. _MyController:

MyController.org
================

`MyController.org <mhttps://www.mycontroller.org/#/home>`_ is a controller for the sensors world! Primarily it was developed to support `MySensors.org <https://www.mysensors.org/>`_ projects.

MyController gives you a way to monitor the wifi-gateway and wireless sensor node. It can also be configured to send you notifications when the pest trap has been sprung.

Pre-requisites
--------------

Before its useful to have MyController running, you will want to get your :ref:`MQTT Broker` running and build the :ref:`Wifi Gateway` so that you have something to control.


Install MyController
--------------------

These instructions are based on the Raspberry Pi build covered in the :ref:`MQTT Broker` section. 

MyController works best with an up to date version of Java installed. The version of Java distributed with Rasberrian is a little too old so the fist steps are to install an updated Java.
Its a rather convoluted process but these steps should get you there.

Install Java 8
^^^^^^^^^^^^^^

These commands add the Java repository to the Pi::

   sudo su
   echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list
   apt-get install dirmgr
   gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
   gpg --export --armor EEA14886 | apt-key add -

   apt-get update
   apt-get install oracle-java8-installer

You will get some prompts to Accept the license to install Java.
Expect to wait a few minutes for java to be installed, you can then exit from the elevated root privilege shell back to normal::

  exit

Download and install MyController
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There's a couple of steps needed here. First download MyController and move it to the location where it will run from. Then as long as you have Java installed you can launch it and log in::

   wget https://github.com/mycontroller-org/mycontroller/releases/download/1.2.0.Final-mycontroller-dist-standalone-1.2.0.Final-bundle.tar.gz

   gunzip -c mycontroller-dist-standalone-1.2.0.Final-bundle.tar.gz | tar -xvf -

   sudo mv ./mycontroller /opt

   cd /opt/mycontroller/bin

   ./start.sh


The ``./start.sh`` command will launch MyController on the default port :8443 . You will be able to browse to the IP address of you Raspberry Pi from another computer to see the MyController application. 

.. sidebar:: Autostart MyController

   .. tip::

      If you restart the Pi, the MyController application will not start automatically. This `post <https://forum.mysensors.org/topic/2262/server-restart/7>`_ explains that you can add

      ``/opt/mycontroller/bin/start/sh``

      to the file ``/etc/rc.local`` 

Use MyController
----------------

Log into MyController at the IP address of your Raspberry Pi:

https://<ipaddress>:8443

The default credentials are `admin/admin` we won't cover changing that here  

Add the wifi gateway to MyController
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^



Add the gateway

Resources -> Gateways -> add

Enter a name for the gateway
Change network type to MySensors
change Type to MQTT
enter tcp://localhost:1883
Enter a client ID E.g. antipesto-mycontroller-mqtt-client

Topic Publish - enter the publish topic from the gateway firmware
Topic Subscribe - enter the subscribe topic from the gateway firmware
