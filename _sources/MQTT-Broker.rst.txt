.. _MQTT Broker:

MQTT Broker
===========

Use of a Raspberry Pi is not mandatory for this project, if you have one then this is a use for it. If you already have another server that can run Linux then you could use that instead. Alternatively there are public brokers you could use; take a look at `<https://test.mosquitto.org/>`_

Dependencies
------------

You will need to have the MQTT Broker up and running before you can run :ref:`MyController` or :ref:`Node Red`

Set up MQTT on Raspberry Pi
---------------------------

Starting from a clean install on an SD card installed in a Raspberry Pi, get your Pi up and running and attached to the network so you can ssh into it. Look for guides on doing a "Headless install" of Raspberry Pi where you can enable the wifi and configure the Pi to accept ssh connections witout needing to connect a screen.

Initial Configuration
^^^^^^^^^^^^^^^^^^^^^

Log in with the default credentials and change the password to secure things a little bit, also change the default hostname from rasberrypi to something else and configure it with a fixed IP address::

   ssh pi@raspberrypi

Change the password::

   passwd

Install some updates::

   sudo apt-get update
   sudo apt-get upgrade

Change the hostname to something else::

   sudo nano /etc/hostname

Edit rasberrypi to somthing more interesting and then close the editor with ctrl+x y

Next edit the hosts file to specify the new hostname in there too::

   sudo nano /etc/hosts

change raspberrypi to hostname

Its not a bad idea to give the Pi a fixed IP address as it is going to be a server, its good to make sure it will always be where you expect it to be::

   sudo nano /etc/dhcpcd.conf

Below are some example IP addresses, you will need to alter this according to your own network::

   # Uncomment the interface that you are going to give the fixed IP address. 
   
   # eth0 is the wired connection uncomment the line below if you are going to use a wired connection
   #interface eth0
   
   #wlan0 is the wireless connection uncomment the line below if you want to use the wireless connection
   #interface wlan0

   static ip_address=10.1.1.7/24
   static routers=10.1.1.1
   static domain_name_servers=10.1.1.1

Exit nano with ctrl+x y and we are done with the initial configuration so then reboot the Pi::

   sudo reboot

Install Mosquitto
-----------------

Once the initial configuration steps above have been done, after a few moments you should be able to log back into the Pi again, and then install Mosquitto::

   sudo apt-get install mosquitto mosquitto-clients

More Information
----------------

`<https://diyprojects.io/mqtt-mosquitto-communicating-connected-objects-iot/#.Wy4V7xyxVuQ>`_
