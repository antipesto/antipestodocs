MQTT Broker
===========

Use of a Raspberry Pi is not mandatory for this project, if you have one then this is a use for it. If you already have another server that can run Linux then you could use that instead. Alternatively there are public brokers you could use; take a look at `<https://test.mosquitto.org/>`_

Set up raspberry pi
-------------------

Starting from a clean install on an SD card installed in a Raspberry Pi, get your Pi up and running and attached to the network so you can ssh into it. Look for guides on doing a "Headless install" of Raspberry Pi where you can enable the wifi and configure the Pi to accept ssh connections witout needing to connect a screen.


ssh pi@raspberrypi

change password

sudo apt-get update
sudo apt-get upgrade

sudo nano /etc/hostname

change hostname

sudo nano /etc/hosts
change raspberrypi to hostname

sudo nano /etc/dhcpcd.conf

#interface eth0

interface wlan0

static ip_address=10.1.1.7/24
static routers=10.1.1.1
static domain_name_servers=10.1.1.1


reboot

sudo apt-get install mosquitto mosquitto-clients

More Information
https://diyprojects.io/mqtt-mosquitto-communicating-connected-objects-iot/#.Wy4V7xyxVuQ

Install MyController
First install Java 8

sudo su
apt-get install dirmngr
echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list
gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
gpg --export --armor EEA14886 | apt-key add -

apt-get update
apt-get install oracle-java8-installer

Accept the license to install java
wait a few minutes for java to be installed

exit

wget https://github.com/mycontroller-org/mycontroller/releases/download/1.2.0.Final-mycontroller-dist-standalone-1.2.0.Final-bundle.tar.gz

gunzip -c mycontroller-dist-standalone-1.2.0.Final-bundle.tar.gz | tar -xvf -

sudo mv ./mycontroller /opt

./start.sh

https://<ipaddress>:8443


Add the gateway

Resources -> Gateways -> add

Enter a name for the gateway
Change network type to MySensors
change Type to MQTT
enter tcp://localhost:1883
Enter a client ID E.g. antipesto-mycontroller-mqtt-client

Topic Publish - enter the publish topic from the gateway firmware
Topic Subscribe - enter the subscribe topic from the gateway firmware
