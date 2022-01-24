# XBee Network Setup

* To begin the XBee network development, you will first have to download and install the XCTU software, which you can find by following [this](https://www.digi.com/products/embedded-systems/digi-xbee/digi-xbee-tools/xctu) link. If you are stuck on anything regarding this software, have a look at their [user guide](https://www.digi.com/resources/documentation/digidocs/90001458-13/default.htm). When the installation is complete, boot up the application and you should see a similar window to the one below.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_1.PNG">
</p>

* The next step is to connect your Xbee modules to the development boards which you can find in the Digi kits. Install the Xbee by lining up the pins to the slots, on the top section of the board. To power your device, connect it to a computer via USB-B cable. If prompted with the installation of any drivers, please accept.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_2.PNG">
</p>

* After powering up the devices, go back to your XCTU application and click the Discover Modules button, located in the top left of the window.

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_3.PNG">
</p>

* In the first window click Select All to ensure all ports will be scanned, then click next. Keep all the port parameters set to default and click finish to begin the scan.

* After a couple of seconds, the application should have identified the two plugged in Xbee’s, select them, and click the Add selected devices button.

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_4.PNG">
</p>

* The next section’s objective is to achieve communication in transparent mode, between the two XBees. With both the devices discovered in XCTU, select the top one from the list and load the default firmware settings.

<p align="center" width="100%">
    <img width="30%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_5.PNG">
</p>

* In the configurations, certain parameters must be updated to make sure that the Xbee’s are on the same channel and can identify each other. Use the table below to guide you through configuration.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_6.PNG">
</p>

* To confirm that the devices are now visible to each other, press the discover radio nodes button.

* The scan should take a couple of seconds and display the other visible device. If you run into any problems at this stage, try reloading the default firmware settings and applying the configurations again.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_7.PNG">
</p>

* When complete successfully, you can press cancel and head into console mode.

* Writing anything inside the console log, should display it letter-by-letter in the other XBee’s console. If you would like to see both the consoles simultaneously, you can use the detach button. 

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_8.PNG">
</p>

* Next we will connect a MQ-9B sensor, responsible for CO and CH4 gas detection, to the XBEE_B.

* After configuring the XBee’s, a script will be deployed to collect the readings over the network (XBEE_A to XBEE_B). The script will also handle the readings decoding and display.

* To begin with, connect the sensor into the Grove AD2 slot on XBEE_B and power up both the devices. Search for them in the XCTU application and open the configuration panel.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_9.PNG">
</p>

* Load in the default settings and write them to both the devices. Next the devices must be switched to API mode, with the XBEE_B having its destination defined to XBEE_A. Use the following table to edit the settings.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_10.PNG">
</p>

* When you finish with the configurations, close the XCTU application and check if your computer has Python installed. You can do so by going into CMD and entering the following command.

  ``python --version``

* If the reply reveals that it doesn’t exit, then you can find the latest version to install [here](https://www.python.org/downloads/). Make sure your installation is complete before you proceed. 

* Python will be required to interact with XBees and decode the sensor data, the digi-xbee library must be installed as well. The easiest method for downloading libraries correctly is using Pip. Use the following command to check if you have Pip installed.

  ``pip –-version``

* In case there is no version of Pip found on the system, use this command to download and install it.

  ``py -m ensurepip -–upgrade``
  
* Repeating the version command should now show that it exists. If you run into any problems during installation, then have a look at this [guide](https://pip.pypa.io/en/stable/installation/)

* With Python and Pip setup, install the XBee library by running the following commands.

  ``pip install pyserial``<br>
  ``pip install srp``<br>
  ``pip install digi-xbee``<br>

<p align="center" width="100%">
    <img width="20%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_11.PNG">
</p>

* Open a Python IDE and copy the code from [this GitHub repository](https://github.com/ysj-HIoT/embedded-system-security/blob/master/XBee/Python%20Remote%20IO/XBee-Remote.py). Before running the program, make sure that the variable PORT is set to the COM of your XBEE_A. You can check this by using the XCTU application. 

* With both the XBee’s connected, run the program and you should begin to see the sensor’s readings.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_12.PNG">
</p>

# XBee Security

XBee technology is one of the most utilised low powered WAN network in the world of IoT. The implementation of XBee can appear in home security, streetlights, power plants, agriculture and more. All these sectors are dependent on data communication and can have extreme consequences if exploited. This technology’s popularity is mainly due to its flexible star/mesh topology and electronic reliability, however like any wireless device it has multiple vulnerabilities. 

This section will explore the different existing XBee vulnerabilities, as well as the security configurations that need to be applied to prevent security breaches. Without any set up at all, the devices will communicate in plain text, publicly visible. The following sections display how this can be utilised by an attacker.

## Packet Sniffer

Packet sniffing is a method where network payloads are detected, captured, and observed. It is used by administrators to monitor and fix their system, and attackers performing cybersecurity breaches. 

* To capture Zigbee packets, the CC2531 USB evaluation kit will be used. Before connecting the USB stick, you will first need to download and install the drivers; head to [this site](https://www.ti.com/tool/PACKET-SNIFFER) and begin the download.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_13.PNG">
</p>

* Open the downloaded file and start the Setup_SmartRF_Packet_Sniffer_x.xx.x.exe.

* During installation keep all the settings as default and confirm if any window pops up asking for admin authorisation. When complete, click the close button and plug in the USB packet sniffer.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_14.PNG">
</p>

* If not already on the desktop or taskbar, use the windows search bar to find the Packet Sniffer application. Select the IEEE 802.15.4/ZigBee protocol and press the start button. You should have the following window open.

<p align="center" width="100%">
    <img width="50%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_15.PNG">
</p>

* Before starting the scan, make sure that the correct Capturing Device and channel is set in the Radio Configuration tab.

* Since there are only 16 channels, it would not take very long for an attacker to find the correct one manually, but we already have the right one from the previous XBee setup. In my case the CH is 0x0C (2410 MHz).

<p align="center" width="100%">
    <img width="100%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_16.PNG">
</p>

* With the correct channel set and the XBee python or XCTU program running, begin the packet capture. With one or two packets captured, you can stop the scan.

<p align="center" width="100%">
    <img width="100%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_17.PNG">
</p>

* The first packet is a request by XBee_A for the sensor reading from XBee_B, which is returned in the second packet.

* In this case the data is not important but if it was more sensitive then we could find it in the MAC Payload section in hexadecimal. Every packet will be different, but in my scenario the sensor reading was 52 in decimal which is stored at the end of the MAC Payload.

<p align="center" width="100%">
    <img width="100%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_18.PNG">
</p>

* The packet leaks more critical information, which will later allow us to connect another device to the network. The network ID and the XBee MAC addresses are revealed in the Dest. PAN, Dest. Address, and Source Address fields.

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_19.PNG">
</p>

* Save the details you have captured, you will neex them in the following section.

## XBee Attacker Node

* You will require another XBee module with a Digi development board for this part of the tutorial.

* Connect it to a different device to make sure its remote, and load it onto the XCTU application, naming it “XBEE_C”. Hopefully, this will ensure that the XCTU doesn’t automatically configure this device onto the same network.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_20.PNG">
</p>

* With the remote XBee connected, it is possible that it is already on the same network as the other devices, you can test this by first switching to the API mode.

<p align="center" width="100%">
    <img width="40%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_21.PNG">
</p>

* When the configuration is successfully uploaded, begin scanning for remote devices.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_22.PNG">
</p>

* If the scan failed to find any devices, the make sure that the Channel and ID settings are the same as XBee_A/B, which you should have captured in the Packet Sniffer section.

<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_23.PNG">
</p>

* At this stage, you will be able to configure the remote device’s settings using AT commands, which the GUI simplifies. 

<p align="center" width="100%">
    <img width="30%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_24.PNG">
</p>

* Before editing anything, return to your main network’s XCTU application, using the console create a packet which sends a simple “test” message from XBEE_A to XBEE_B. Deploy this packet in an infinite sequence, with an interval of 5000ms.

* Confirm that the test message has been received on XBEE_B’s console, if successful then you can head back to the remote device. 

* Remotely enter XBEE_B’s configurations and edit the SL number to the attacking XBee’s (XBEE_C) DL, this should redirect the stream of messages to our infiltrating device. 

* You can confirm the results in the console window. Similarly, the ID could be edited to disconnect the device from the current network.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_25.PNG">
</p>

## Security Configuration

* To protect the packet data and node visibility, AES encryption should be set up using the XCTU application.

* First, on the XBEE_B, head to configuration and enable AES Encryption. The other setting you must change is the AES Encryption Key which for this example will be:

    ``“AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA” (allowed range of 0-32 bit)``
    
<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_26.PNG">
</p>

* Repeat the steps on XBEE_A and attempt to communicate using the console again, you should have the same results as before.

* However, if you return to the remote XBEE_C, there you should no longer be able to see any nearby devices, even with the correct network settings.

* Packet sniffing will result in the capture of AES encrypted packets as well, ensuring that transmitted data is safe from eavesdropping.

## Hack RF

The HackRF One is a wide band software defined radio that can receive and transmit a frequency range of 1MHz to 6GHz. To program the HackRF One, we use a software known as GNU radio companion which is a front-end graphical user interface that allows us to create python programs simply by using blocks to create flowcharts.

Signal jamming and a replay attack will be demonstrated, to show how a Zigbee network can be disrupted using a software-defined radio. Before continuing with the tutorials, you will have to setup the Hack RF and the software, using the separate document “HackRF Setup (main)”. If for any reason the first setup does not work, try the backup setup.

The Wireless Telegraphy Act 2006 states that using any apparatus for the purpose of interfering with wireless communication is illegal, even in a controlled environment. Therefore, these tutorials have been developed to show the GNU Radio Companion designs, but they are not meant to be executed.

### Signal Jammer / Noise Source

* Firstly, you must identify the channel frequency that your Xbees are communicating over.

* Going back into the configuration tab, look for the CH setting and take a note of it. Use the below table to match the channel ascii to the hex column, that should give you the correct frequency.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_27.PNG">
</p>

* In my example the channel is “C” and the frequency is 2.410GHz. Going back to the GNU Radio Companion, copy the below diagram, and change the target_freq so that it matches the one you identified.

    <i>Tip: use ctrl + f to search through the functions faster</i>
    
<p align="center" width="100%">
    <img width="100%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_28.PNG">
</p>

* On compile the GNU Companion converts the diagram into a Python program; using the HackRF it creates noise around our targeted frequency.

* Assuming the amplitude is adequate, and no signal jamming protection is present, this program will interfere Zigbee communication.

### Replay Attack

Another method for the offensive use of SDRs on Zigbee embedded systems is replaying captured signals. A replay attack occurs when a cybercriminal eavesdrops on a secure network communication, intercepts it, and then fraudulently delays or resends it to misdirect the receiver into doing what the hacker wants. The added danger of replay attacks is that a hacker doesn't even need advanced skills to decrypt a message after capturing it from the network. The attack could be successful simply by resending the whole thing.

* You can either follow the tutorial or try to implement the solution [from github yourself](https://github.com/norbertdajnowski/embedded-system-security/tree/master/XBee/replay-attack). 

* Create a new folder where you will store the input and output GRC files and the captured recording of XBee’s communication. 

* Open a new GRC file and call it replay-input.grc. Copy the diagram from below, making sure to use the same target frequency as before.

<p align="center" width="100%">
    <img width="100%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_29.PNG">
</p>

* In the folder that you’ve just created, create a new file, and make sure that it ends with the .dll filetype; set the File Sink’s path to the new .dll.

* Back inside the XCTU, make sure both the XBee’s are in transparent modes and switch to the console tab. Create a new packet filled with the repeating characters “A” and make sure its couple hundred bytes in size.

<p align="center" width="100%">
    <img width="70%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_30.PNG">
</p>

* Click add packet and return to GNU Radio Companion, compile your input diagram, and execute it.

* All the signals on XBee’s frequency will be recorded by the HackRF when the new window pops up. Quickly send the packet through the XCTU application and end the SDR program to stop the recording.

* If the recording happened to have a lot of white noise, then you can try it again since the program will just overwrite the file.

* You should now have the recording of the XBee packet saved, the next step is to create the replay-output diagram. Use the image below and make sure your frequency and file path are adjusted.

<p align="center" width="100%">
    <img width="100%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_31.PNG">
</p>

* When ready, compile and run this program while monitoring the XBee through XCTU. If successful, you should have received the recorded packet from the SDR, with the XBEE_A believing that it has come from XBEE_B.

<p align="center" width="100%">
    <img width="60%" src="https://github.com/CS-Outreach-Session/Embedded-System-Security-/blob/main/Images/xbee_32.PNG">
</p>
