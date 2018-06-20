Overview
========

Project Objective
-----------------

I wanted to build a wireless sensor node that could be completely self contained in a small weatherproof box including a battery and all the electronics. A box with holes in it to accept wires risks allowing water to get in. Wires and cables outside the box might also get chewed on by animals or interfere with the trap mechanism.
I want to get information from the sensor to confirm that it is alive and well and also to immediately signal when something gets caught in the trap.

The complete solution is based on the framework provided by `MySensors <http://mysensors.org>`_ which is an Arduino library with support for NRF24L01+ wireless transceivers. Because the library takes care of all the complicated set up needed to get the radios up and running, you can focus on assembling your sensors and making use of the data.

My project has several components that produce the complete solution. There is core infrastructure that needs to be in place such as a Gateway and `MQTT <https://en.wikipedia.org/wiki/MQTT>`_ service, some of these you may already have if you have been building other sensor projects. From there you can add as many trap sensor nodes as you need [#f1]_.

Optional components are `NodeRed <https://nodered.org/>`_ which will let you integrate your trap sensors with external services such as `'Trap NZ' <http://api.trap.nz>`_ . I used `MyController <http://mycontroller.org>`_ as a local GUI interface to see what my sensors were up to. You could conceivably use something else like `Domoticz <http://www.domoticz.com/>`_ as long as it can subscribe to messages that the sensor publishes to MQTT.

Core Infrastructure
-------------------

* MySensors wifi gateway to bridge from the NRF24L01+ wireless sensor node network to Ethernet
  
  * Low power “always on” power supply.
  * ESP8266 / NodeMCU
  * NRF24L01+ / RFM69 transceiver 

* MQTT service to act as a communications bus.

  * I used Mosquitto running on a Raspberry Pi, but you could always use one you might already have running for other projects or even try a publicly accessible online MQTT service. The Raspberry Pi is just what I used to run the MQTT service and MyController (see below) but any computer that can run these packages is OK.

Wireless Sensor Nodes
---------------------

* Battery powered wireless Sensor Node

  * 3.7v Li-Ion battery to supply power to;
  * Arduino Nano type MCU
  * Magnetic reed switch or some kind of switch contraption that can be somehow actuated by a mechanical pest trap.
  * NRF24L01+ / RFM69 wireless transceiver.

Optional bits
-------------

* MyController or Domoticz for local monitoring.

   * This does nothing but give you a view of the sensor nodes by subscribing to messages on the MQTT bus. You might want to send yourself alerts when a trap is sprung and you could use these to trigger alerts via push notification or email. (Keep in mind some target pests are more active at night!)

* Node-Red to bridge from the MQTT bus to other external services such as http://trap.nz

.. rubric:: Footnotes

.. [#f1] There are some caveats such as how many you can get in the limited radio range, but in theory: a lot of sensors.
