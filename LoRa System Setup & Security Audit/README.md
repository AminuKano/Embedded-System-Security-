## LoRa Network Setup

The following instructions will guide you on the development of a LoRa embedded system for peer-to-peer communication. To complete the setup, you will require two Arduino’s and two Dragino LoRa v1.4 shields. Slot the LoRa shield onto the Arduino, and make sure that the antenna is attached. You should now have two identical machines setup.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_1.PNG">
</p>

### Arduino IDE

* To program the Arduino microcontroller, first download and install its IDE from the [official website](https://www.arduino.cc/en/software). When finished, load it open and you should be greeted with the Arduino template code.

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_2.PNG">
</p>

* When it comes to interacting with the LoRa shield, you will need to download a library compatible with Semtech SX1276 shields.

* Using the top navigation bar, head to Tools > Manage Libraries and search for “LoRa” by Sandeep Mistry; install the newest version of the library.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_3.PNG">
</p>

### Using LoRa Examples

* Luckily the LoRa library contains template examples for P2P communication, which we can build on top of. 

* Using the navigation bar head to File > Examples > LoRa > LoRaSender, which should have opened a new window, containing code for our sender microcontroller. Now follow the same route to open LoRaReceiver in another window.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_4.PNG">
</p>

### Uploading the Sketch

* The next step will be to upload the sketches onto the Arduino. This should be done one by one to avoid any problems with the ports.

* Connect your Arduino and computer using a USB A-B cable, and head to Tools > Port to choose the right Arduino port. If it is not visible, you can try restarting the IDE.

* Before uploading the sketch, make sure that the correct board is selected from the list, this usually switches automatically on port selection.

<p align="center" width="100%">
    <img width="30%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_5.PNG">
</p>

* With a single board connected, and the correct port/board type selected, you can click the upload sketch button. This might take a couple of seconds to process but eventually will load the LoRa sender or receiver program onto the microcontroller.

* When complete, plug in your other device and reset the IDE, then continue to upload the other program.

<p align="center" width="100%">
    <img width="30%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_6.PNG">
</p>

* When ready, you can plug in both the devices and inspect the receiver’s serial monitor, by going into Tools > Serial Monitor.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_7.PNG">
</p>

* Your board configuration might be different, but the receiver’s port should be selected in Tools, to monitor the correct connection. The above results should look like yours, with each message incrementing the number after hello, and RSSI indicating the connections strength.

### Sensor Installation

This section will demonstrate the installation of an ultrasonic sensor, and the transmission of its readings over our LoRa connection. This can be skipped, and the original hello messages program can be used for the following LoRa security tutorials.

* To begin with, you will need a breadboard, jumper wires and an ultrasonic sensor HC-SR04. Copy the diagram below to install your sensor. Make sure to install the sensor on the LoRa sender device.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_8.PNG">
</p>

* When you complete the installation, upload and run [this](https://github.com/ysj-HIoT/embedded-system-security/blob/master/LoRa/LoRaSenderUltrasonic/LoRaSenderUltrasonic.ino) sketch on your Arduino. The receiving device should now display a similar output to the one below.

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_9.PNG">
</p>

## LoRa Network Security

LoRa is one of the most recognized IoT networking technologies, popular for its long range and low power features, data is transmitted using a spread spectrum modulation technique. It has use cases for smart cities, buildings, metering, logistics, agriculture, and more. 

However, without additional configurations there is no security in LoRa P2P communication. Messages are broadcasted to all nearby LoRa devices by default, therefore compromising all security. Concluding that the default configurations are not appropriate for the transfer of sensitive data over LoRa. This section will present multiple attacks a malicious user can attempt, and the setup of LoRaWAN to protect the embedded system.

### LoRa Security Test

* This first section is designed to display that by default LoRa communication is scattered to any node in the signal strength radius.

* Connect another LoRa shield with an Arduino, this node will be referred to as LoRa C. Power it and upload the receiver code from File > Examples > LoRa > LoRaReceiver.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_10.PNG">
</p>

* When the upload is complete, power up the other two nodes and open the LoRa receivers’ serial monitors. They should both display identical packets received, with only the RSSI being different due to the devices’ position from the sender.

* . In case the normal devices are communicating over LoRa using custom encryption, a malicious user could use the captured encrypted packets for a replay attack.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_11.PNG">
</p>

## LoRaWAN Setup

LoRaWAN is a networking protocol that uses LoRa’s modulation, but rather than peer to peer communication, it utilises the star topology. It is a massive security extension, which ensures that authentication and encryption are mandatory for communication. 

During this tutorial, you will develop a LoRaWAN network using the Arduino Pro Gateway Kit. The first stage consists of assembling the gateway, which is then configured using ABP/OTAA methods and connected to the cloud. LoRa end-nodes must be reprogrammed to use the ABP/OTAA authentication before sending any data to the cloud application.

<b> LoRa Connectivity Gateway was not compatible </b>
<b> Idea: Demonstrate the setup of a LoRa gateway with this already developed tutorial and then use one of the already set up gateways on campus for the rest of the tutorial. </b>

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_12.PNG">
</p>

### LoRa Gateway Assembly

* Follow the instructions from the back of the box, it guides you through the gateway assembly and the device registration.

1.	Insert the SD card, then attach the fan as shown in picture 1. Screw together the enclosure panel with the SMA pigtail.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_13.PNG">
</p>

2.	Wire the Fan cables with the clips as shown in the image above.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_14.PNG">
</p>

3.	Connect the SMA pigtail to the X1 antenna connector.

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_15.PNG">
</p>

4.	Insert the boards into the enclosure - <b>Important</b>: make sure to take note of the serial number from the sticker on the radio module, before placing it inside the enclosure (It is required for online gateway registration).

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_16.PNG">
</p>

5.	Connect the antenna, then plug-in the power supply and Ethernet.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/lora_17.PNG">
</p>

### Device Registration



### LoRa Connection with the Gateway



