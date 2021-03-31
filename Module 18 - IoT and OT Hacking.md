# Module 18 - IoT and OT Hacking #

## Perform Footprinting ##
The first step in IoT and OT device hacking is to extract information such as IP Address, protocols used (MQTT, ModBus, ZigBee, BLE, 5G, IPv6LoWPAN...), open ports, device type, geolocation of the device, manufacturing number and manufacturer...

### Whois Footprinting ###
* https://www.whois.com/whois/

### Advanced Google Hacking ###
* https://www.exploit-db.com/google-hacking-database
* https://www.google.com (intitle:"index of", inurl, insite...)

### Shodan ###
* https://www.shodan.io/


- - - -

## Capture and Analyze IoT Device Traffic ##

### Wireshark ###
First, we'll need to install the MQTT Explorer, which is a comprehensive MQTT client that provides a structured overview of MQTT topics and simplifies working with devices on your broker: `sudo snap install mqtt-explorer`.

`mqtt-explorer` (Launch this while analyzing the traffic with Wireshark) > 'MQTT Connection' > 'CONNECT' > Analyze the traffic in Wireshark

Some of the headers of the 'Connect' command:
* Header Flags: Contains info about the MQTT control packet type
* Connect Flags: Contains parameters specifying the behaviour of the MQTT connection
* Clean Session: Indicates whether the client wants to establish a persistent connection with the broker or not
* Client ID: Indicates a unique identifier for each MQTT client connecting to a MQTT broker

Some of the headers of the 'Connect Ack' packet:
* Header Flags: Contains info about the MQTT control packet type
* Session Present: Indicates the session between the broker and the client: Bit 0 is the Connection Ack bit in the session present flag
* Return Code: 
    * 0: Connection Accepted
    * 1: Connection Refused, Unacceptable Protocol Version
    * 2: Connection Refused, Identifier Rejected
    * 3: Connection Refused, Server Unavailable
    * 4: Connection Refused, Bad Credentials
    * 5: Connection Refused, Not Authorized

Some of the headers of the 'Subscribe Request' packet:
* Header Flags: Contains info about the MQTT control packet type
* Message Identifier: Identifies a message in a message flow between a client and a broker
* Topic and QoS Level: A subscription is a pair of a topic (subject of interest) filter and a QoS level
* Payload: Contains a list of subscriptions

Some of the headers of the 'Subscribe Ack' packet:
* Header Flags: Contains info about the MQTT control packet type
* Message Identifier: Identifies a message in a message flow between a client and a broker
* Payload: Contains a list of return codes
* Return Code: For each Topic/QoS pair received, a return is sent by the MQTT broker in the 'Subscribe' message. The return code is in line with the QoS level in the case of a success
    * 0: Success - Maximum QoS 0
    * 1: Success - Maximum QoS 1
    * 2: Success - Maximum QoS 2
    * 128: Failure

Some of the headers of the 'Publish Message' packet:
* Header Flags: Contains info about the MQTT control packet type
* DUP Flag: If it's 0, it indicates the first attempt at sending this 'Publish' packet. If it's 1, it indicates a possible re-attempt at sending the message
* QoS: Determines the assurance level of a message
* Retain Flag: If it's 1, the server must store the message and its QoS, so it can cater to future subscriptions matching this topic
* Topic Name: Contains a UTF-8 string that can also include forward slashes when it needs to be hierarchically structured
* Message: Contains the actual data to be transmitted
* Payload: Contains the message that is being published


