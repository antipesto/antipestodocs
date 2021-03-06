Wireless Tranceivers
====================

Just a bit of discussion about wireless radios and sensors, strengths and weaknesses.


Wifi
----

.. image:: ./_images/nodemcu.jpg
    :height: 100px
    :align: left
    :alt: NodeMCU image.

Wifi is fairly ubiquitous and it is reasonable to assume a household will have some wifi coverage in their outdoor area where a trap box might be located.

The disadvantage of WiFi is that it needs quite a bit of power when it is running; this means I need either a bigger battery or a way to keep the battery topped up (maybe a solar panel). The ESP8266 chip (or NodeMCU module) are inexpensive (you can get them for less than NZD $5) and they have a lot of potential. I do make use of one in the sensor gateway but there are some fiddly things besides power consumption I need to overcome. For example:

* **Monitoring Battery Voltage** - You need to build some circuitry (a voltage divider) to allow the battery voltage to be measured via the single analogue pin on the ESP8266
* **Wake up on Interupt** - To make sure that the battery lasts as long as possible, the node needs to be put to sleep. You can program it to wake up at intervals to "check in" with the gateway and perhaps send a battery voltage measurement but its also really useful if you can get the device to wake up immediately in the event that the pest trap is sprung. Its not insurmountable but interupt handling on the ESP8266 while its asleep seems to need external circuitry to send a signal to the wake up pin when the state of the sensor changes. 

It's still something I would like to explore more but for the moment I am not using wifi on my remote sensor nodes.

NRF24L01+
---------

.. image:: ./_images/nrf24l01.jpg
    :height: 100px
    :align: left
    :alt: NRF24L01 image.

These are the wireless transceivers that are used extensively on the `MySensors <http://mysensors.org>`_ framework. They are really really cheap, if you are prepared to wait a little while for them to be delivered you can get a bunch of them. Less than NZD $10 can get you 10 of them.  

They are only transceivers and you hook them up to microcontrollers like Arduino Nano or similar so that microcontrollers can talk to each other wirelessly.

The immediate disadvantage I have found with these is the range that the wireless signal can go. With the circuitry out on my bench I can easily get coverage through several rooms indoors. Once I have them inside enclosures and then inside the trap tunnel the range is extremely short. I pretty much have my wifi gateway indoors by a window and the trap tunnel containing the sensor node is on the ground just below the window. It's working for the moment but I might play about with the way the antenna is oriented and see if I can get a bit more distance between the gateway and the sensor node. I might also see if I can get my wifi gateway a bit more weather tight and stick it outoors as well in case the external walls of my house are antenuating the radio signal a lot.

.. image:: ./_images/NRF24L01+PA+LNA.jpg
   :width: 100px
   :align: left
   :alt: NRF24L01+PA+LNA

The NRF24L01+ has a variant with an external antenna called NRF24L01+PA+LNA this should have improved the range. There are also some blog articles which show you how to modify the board to build your own rudimentary antenna. I have a single tranciever with an external antenna which I am using on the wifi gateway. At some point I will get myself another one and put it on the remote node to replace the one with the PCB antenna I am using at the moment. There are a couple of downsides to this:

* The NRF24L01+PA+LNA costs more although it does usually include the antenna.
* The external antenna would need me to drill a hole in my weatherproof box and might also not fit too well in the trap tunnel.

The benefits of NRF24L01 radios are:

* **its really really low power.** On a full battery charge I had one polling the gateway every 5 minutes for about 2 weeks before the battery went dead. This is way more polling than it needs to do so I am expecting that with a poll every few hours the battery will last in excess of a year.
* **Its really really small** - assuming I don't absolutely have to use an external antenna, the transciever, microcontroller, reed switch and battery will fit in an enclosure a little larger than the size of two AA batteries beside each other.

RFM69
-----

.. image:: ./_images/rfm69.jpg
    :height: 100px
    :align: left
    :alt: rfm69 image.

This is an alternative to the NRF24L01+ modules which is supported on the MySensors framework. I have not had a chance to play with these. They are somewhat more expensive than the NRF24l01+ and need a little coil antenna soldered to them. There is a suggestion that the radio has a slightly better range than the NRF24L01+ which given my experience could be good to explore. 

The module looks a little larger than the NRF24L01+ but still pretty small. I don't yet know what the battery life will be like using these, the slightly higher radio range might be because it uses a bit more power.

Another nice feature of these which is absent on the NRF24L01+ is the module has the ability to report radio signal strength and interference.

LoRa
----

.. image:: ./_images/lora-logo.jpg
    :height: 100px
    :align: left
    :alt: LoRa Logo.

`LoRa <https://en.wikipedia.org/wiki/LoRa>`_ appears to be used by commercially available trap sensors and other commercial IoT devices. There are some modules available for you to build your own projects with these radios but looked a little expensive. There is some promise that this type of radio will have really good range and performance. I will keep an eye out for inexpensive LoRa modules and hope to give them a try one day.
