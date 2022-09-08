# Bluetooth & Ubertooth One

## Bluetooth System Setup

Before caputuring and analysing Bluetooth data, you must setup the communication between the two HC-05 modules. They need to be installed and connected to the Arduino MCUs, powered up in AT mode and configured as Master to Slave communication.

### Slave Node Setup

* The HC-05 module should be installed on a breadboard, but male to female cables would work as well.

* Begin by installing the receiver Bluetooth module, copying the circuit design below.

<p align="center" width="100%">
    <img width="100%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_1.PNG">
</p>

* Make sure that the TXD pin goes to TX and RXD to RX, these handle all the communication between the Bluetooth module and the MCU.

<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_2.PNG">
</p>

* The Bluetooth device must be launched in AT mode to interact with it. To do so, you will have to press down the small button at the bottom right of the HC-05. Holding onto the button, power on the device, if a red light begins to flash once per every two seconds, then you have successfully launched it in AT mode.

<p align="center" width="100%">
    <img width="20%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_3.PNG">
</p>

* Open the serial monitor through the Arduino IDE and change its settings to display Both NL & CR at a baud rate of 38400 (HC-05 AT Mode Default).

<p align="center" width="100%">
    <img width="30%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_4.PNG">
</p>

* Enter <i>AT</i>, which should return OK, as shown in the screenshot below. Use the following commands to make sure that the module is set as a receiver and to view its address.

  ``AT``<br>
  ``AT+ROLE=0``<br>
  ``AT+ADDR``
  
<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_5.PNG">
</p>

### Master Node Setup

* Now that you have the receiver Bluetooth setup, you will need to install the other HC-05 and configure it as a Master Node.

* Follow the same steps and circuit design as before to install the new module, this can be done on the same breadboard, just make sure you don’t cross any wiring between the two Arduinos.

<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_6.PNG">
</p>

* Launch the new Bluetooth module in AT mode, by holding onto the button while powering on your Arduino. Open the serial port for it and test the AT communication again using the following command.

  ``AT``

* The next commands instruct the module to search and connect to nearby compatible Bluetooth devices when launched, enter them in the serial monitor.

  ``AT+ROLE=1``<br>
  ``AT+CMODE=1``

### Wiring for Bluetooth Communication

* Before you begin transmitting messages, you will have to switch the RX pin to the 3rd Digital Pin, and TX pin to the 2nd Digital Pin on the Arduino.

* This will ensure that the Bluetooth Serial does not disturb the Arduino Serial monitor communication. Make sure to do this on both the devices.

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_8.PNG">
</p>

* In the Arduino IDE, select the port to your Master device and upload [this](https://github.com/ysj-HIoT/embedded-system-security/blob/master/Bluetooth/hc05_master/hc05_master.ino) code.

* Then switch to the receiver device and upload [this](https://github.com/ysj-HIoT/embedded-system-security/blob/master/Bluetooth/hc05_slave/hc05_slave.ino) code.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_9.PNG">
</p>

* Restart both the devices and let them launch normally, after a couple seconds you should notice the Bluetooth LEDs flashing asynchronously every second or two. This confirms that they have made a connection.

* Open the Master device’s serial monitor and input “send”, make sure the baud rate is set to 9600 when doing so.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_10.PNG">
</p>

* Open the serial monitor of your receiver device and select the baud rate of 9600, you should see a stream of the ‘t’ character.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_11.PNG">
</p>

* This confirms that there is data communication between the two devices.

## Packet Sniffing with Ubertooth One

Project Ubertooth is an open-source wireless development platform suitable for Bluetooth experimentation. Ubertooth ships with a capable BLE (Bluetooth Smart) sniffer and can sniff some data from Basic Rate (BR) Bluetooth Classic connections. Here is a [link](https://ubertooth.readthedocs.io/en/latest/ubertooth_one.html) to the original Ubertooth One documentation, in case you need it throughout this section.

### Ubertooth One Installation

* In Kali Linux environment, create a new folder for the Ubertooth prerequisites.

  ``mkdir ubertooth-one``<br>
  ``cd ubertooth-one``

* Install all the required packages.

  ``sudo apt install cmake libusb-1.0-0-dev make gcc g++ libbluetooth-dev wget \ pkg-config python3-numpy python3-qtpy python3-distutils python3-setuptools``

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_12.PNG">
</p>
 
 * Next, you will need to install the Libbtbb library which Ubertooth requires to decode Bluetooth packets.

  ``wget https://github.com/greatscottgadgets/libbtbb/archive/2020-12-R1.tar.gz -O libbtbb-2020-12-R1.tar.gz``<br>
  ``tar -xf libbtbb-2020-12-R1.tar.gz``<br>
  ``cd libbtbb-2020-12-R1``<br>
  ``mkdir build``<br>
  ``cd build``<br>
  ``cmake ..``<br>
  ``make``<br>
  ``sudo make install``<br>
  ``sudo ldconfig``
  
<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_13.PNG">
</p>

* When Libbtbb installation is complete, you will have to install the Ubertooth tools using the following commands.

  ``wget https://github.com/greatscottgadgets/ubertooth/releases/download/2020-12-R1/ubertooth-2020-12-R1.tar.xz``<br>
  ``tar -xf ubertooth-2020-12-R1.tar.xz``<br>
  ``cd ubertooth-2020-12-R1/host``<br>
  ``mkdir build``<br>
  ``cd build``<br>
  ``cmake ..``<br>
  ``make``<br>
  ``sudo make install``<br>
  ``sudo ldconfig``
  
<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_14.PNG">
</p>

* The final setup installation is the Wireshark plugin, which will help review captured packets later in the tutorial.

* Use the following instructions in the appropriate folders to complete the plugin installation.

  ``sudo apt-get install wireshark wireshark-dev libwireshark-dev cmake``<br>
  ``cd libbtbb-2020-12-R1/wireshark/plugins/btbb``<br>
  ``mkdir build``<br>
  ``cd build``<br>
  ``cmake -DCMAKE_INSTALL_LIBDIR=/usr/lib/x86_64-linux-gnu/wireshark/libwireshark3/plugins ..``<br>
  ``make``<br>
  ``sudo make install``
  
<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_15.PNG">
</p>
  
  ``sudo apt-get install wireshark wireshark-dev libwireshark-dev cmake``<br>
  ``cd libbtbb-2020-12-R1/wireshark/plugins/btbredr``<br>
  ``mkdir build``<br>
  ``cd build``<br>
  ``cmake -DCMAKE_INSTALL_LIBDIR=/usr/lib/x86_64-linux-gnu/wireshark/libwireshark3/plugins ..``<br>
  ``make``<br>
  ``sudo make install``
  
### Using the Spectrum Analyser

* The Spectrum Analyzer shows the wireless communication activity at the frequency of around 2400 MHz.

* First, connect your Ubertooth One device to one of the USB ports.
  
<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_16.PNG">
</p>
  
* Go to the specan_ui python tool in the Ubertooth directory.

  ``cd /ubertooth-2020-12-R1/host/python/specan_ui``
  
* Run the program using the following command.

  ``sudo ubertooth-specan -d -  -l 2400 -u 2483 -U -1``
  
* It is possible that the program returns a traceback error due to a wrong API implementation by the sip module.

<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_17.PNG">
</p>
  
* If that’s the case then run the following command to fix it, otherwise just ignore this step.

  ``sudo apt-get install –only-upgrade python3-pyqt5.sip``
  
<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_18.PNG">
</p>
  
* Run the Spectrum Analyzer again, if it still requests you to upgrade the firmware then use the following commands to do so.

* Use <b>cd ..</b> to return to the ubertooth-2020-12-R1 directory.

* Go to the <i>ubertooth-one-firmware-bin</i> directory and run:

  ``ubertooth-dfu -d bluetooth_rxtx.dfu -r``
  
* Open the spectrum analyser using:

  ``Sudo ubertooth-specan -d -  -l 2400 -u 2483 -U -1``
  
<p align="center" width="100%">
    <img width="90%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_19.PNG">
</p>

* The left screenshot is the output example before launching the Bluetooth devices, and the right is post-launch. Run your Bluetooth devices while the spectrum analyser is on, see if any changes appear on the graph.

### LAP Packet Sniffing

* LAP Packet sniffing is another Ubertooth utility, which displays a couple of details (including the LAP value) from the captured Bluetooth packets.

* Make sure that your previous Bluetooth communication is online and transmitting messages, throughout these next sections.

* Use ubertooth-rx to launch the packet sniffer.

  ``ubertooth-rx``
  
<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_20.PNG">
</p>

* Most of these messages contain the same LAP value, its likely that it is the LAP of the Bluetooth device that has been set up.

### Wireshark Display

* To get a better insight on the decoded Bluetooth packets, Ubertooth capture is passed to the Wireshark application.

* You should have already installed the Wireshark plugin from the previous preqrequisites, run the following command:

  ``mkfifo /tmp/pipe``

* Follow these steps to start capturing packets in Wireshark.

1.	Open Wireshark
2.	Click Capture -> Options
3.	Click “Manage Interfaces” button on the right side of the window
4.	Click the “New” button
5.	In the “Pipe” text box, type “/tmp/pipe”

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_21.PNG">
</p>

6.	Click Save, then click Close
7.	Click “Start”
8.	Start another Ubertooth sniffer using the command

  ``ubertooth-btle -f -c /tmp/pipe``

<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_22.PNG">
</p>

* You should expect a similar output to the example above.

* The Wireshark application displays a more organised version of these packets and offers tools for analysis.

<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/bt_23.PNG">
</p>

## [Hack RF One](https://github.com/CS-Outreach-Session/Network-Security-/tree/main/HackRFOne)
* HackRF One
* Installing GNU Radio Companion and Setting up the work environment
* Hardware Setup
* Visualising FM Radio using HackRF One
* Listening to FM Radio


