# Module 08 - Sniffing #

## Perform Active Sniffing ##

### Perform MAC Flooding ###
#### Macof ####

### Perform DHCP Starvation Attack ###
#### Yersinia ####

### Perform a MiTM Attack ###
#### Cain & Abel ####
1. Configure > Sniffer > Select the Adapter
2. Start the Sniffer
3. In the 'Sniffer' section, go to the 'APR' tab
4. Perform ARP Poisoning selecting the targets
5. When the victim inputs any password, for instance an ftp connection password, it will appear in the tab 'Passwords'


### Spoof a MAC Address ###
#### TMAC ####

#### SMAC ####
1. Choose the network adapter
2. Specify a new MAC Address or choose 'Random'
3. Select 'IPConfig' to look at the IPConfig information
4. Click on 'Update MAC' to change the MAC Address


- - - -

## Perform Network Sniffing ##

### Password Sniffing ###
#### Wireshark ####
``` http.request.method=="POST" ```

* To capture remote traffic in Windows (rdp) -> 'Services' > 'Remote Packet Capture' > Start
    * In Wireshark:
        * 'Capture' > 'Options' > 'Manage Interfaces' > 'Remote Interfaces' > 'Add Button' > Select the host, port and credentials

### Analyze a Network ###
#### Capsa Network Analyzer ####
Select the network adapter > 'Start'

#### Omnipeek Network Protocol Analyzer ####

#### SteelCentrak Packet Analyzer ####


- - - - 

## Detect Network Sniffing ##

### Detect ARP Poisoning in a Switched-Based Network ###
``` hping3 <IP> -c <N of packets - Ex. 10000> ``` - The victim machine pings the other ARP-poisoned machine

In the attacker machine, open Wireshark:
1. Preferences
2. Select the Protocol: 'ARP/RARP' > Select the option 'Detect duplicate IP address configuration'
3. Start capturing packets
4. In the menu bar: 'Analyze' > 'Expert Info' - Warning messages will appear: 'Duplicate IP address configured'


### Detect ARP Attacks ###
#### Xarp ####
Set the Security Level to 'Aggressive' - Whenever an ARP Poisoning attack is detected, it will pop-up an alert.


### Detect Promiscuous Mode ###
#### Nmap ####

#### NetScan Tools Pro ####


