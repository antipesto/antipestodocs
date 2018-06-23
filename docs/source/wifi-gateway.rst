Wifi Gateway
============

The wifi gateway has a radio for wifi and is directly wired to another radio the same as the wireless sensors and provides the following:

* Acts as a bridge between the wireless sensors and your wifi network.

I built mine exactly the same as the example on the MySensors website. On my prototype I also opted for one of the advanced build options with LED indicators so I could see when the gateway is communicating with a sensor node. Plus LED's make beige enclosure boxes look a bit more interesting.


I used a NodeMCU with an NRF24L01+PA+LNA Antenna version radio module.

Building instructions
---------------------

Instructions for how to connect the radio module to a NodeMCU can be found here `connect_radio <https://www.mysensors.org/build/connect_radio>`_

Further build instructions for the gateway can be found here `esp8266_gateway <https://www.mysensors.org/build/esp8266_gateway>`_

Coding the gateway firmware
---------------------------

For my build I am using an MQTT broker so the code I used is based on the `ESP8266MQTTClient example: <https://github.com/mysensors/MySensors/blob/master/examples/GatewayESP8266MQTTClient/GatewayESP8266MQTTClient.ino>`_

Customise the firmware
----------------------

There is some configuration to change in the firmware for the wifi gateway to get it to join your wifi network, connect to your MQTT broker and set some other MQTT parameters up.

SSID and Password
^^^^^^^^^^^^^^^^^

MQTT Broker IP address
^^^^^^^^^^^^^^^^^^^^^^

MQTT Client Name
^^^^^^^^^^^^^^^^

MQTT Publish Topic
^^^^^^^^^^^^^^^^^^

MQTT Subscribe Topic
^^^^^^^^^^^^^^^^^^^^

