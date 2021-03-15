# Module 08 - Sniffing #

## Perform Active Sniffing ##
Active Sniffing searches for traffic on a switched LAN by actively injecting traffic into the LAN.

### Perform MAC Flooding ###
Attackers use the MAC Flooding technique to force a switch to act as a hub, so they can easily sniff the traffic.

#### Macof ####
It floods the local network with random MAC addresses and IP addresses, flooding the switches CAM tables and causing some switches to fail and open in repeating mode, thereby facilitating sniffing.

` macof -i <Interface> -n <N of packets> `

### Perform DHCP Starvation Attack ###
Attackers flood the DHCP server by sending a large number of DHCP requests and uses all available IP addresses that the DHCP server can issue. As a result, the DHCP server cannot issue any more IP addresses, leading to DoS attacks.

#### Yersinia ####
` yersinia -I ` - To open Yersinia in interactive mode

* `h` - To display the 'Help' menu
* `q` - To exit the 'Help' menu
* `F2` - To select DHCP mode > `x` - To list available attack options > `1` - To select DHCP Starvation attack (DISCOVER packet)

#### Other DHCP Starvation Attack Tools ####
* Hyenae (https://sourceforge.net)
* dhcpstarv (GitHub)
* Gobbler (https://sourceforge.net)
* DHCPig (GitHub)


### Perform ARP Poisoning ###
ARP Spoofing succeeds by changing the IP address of the attacker's computer to the IP address of the target computer. The attacker sends forged ARP request and reply packets to find a place in the target ARP cache.

#### arpspoof ####
` arpspoof -i <Interface> -t <Target IP> <Gateway IP> `

#### Other ARP Poisoning Tools ####
* BetterCAP (https://www.bettercap.org)
* Ettercap (http://www.ettercap-project.org)
* dsniff (https://www.monkey.org)
* MITMf (GitHub)


### Perform a MiTM Attack ###
#### Cain & Abel ####
Cain & Abel is a password recovery tool that allows the recovery of passwords by sniffing the network and cracking encrypted passwords. The ARP Poisoning feature involves sending spoofed ARPs to the network's host victims, which facilitates MiTM attacks.

It can be found at: `Module 08 Sniffing\ARP Poisoning Tools\`.

1. Configure > Sniffer > Select the Adapter
2. Start the Sniffer (Sniffer tab > Upper blue 'Plus' icon) 
3. In the 'Sniffer' section, go to the 'APR' tab
4. Perform ARP Poisoning selecting the targets (Upper blue 'Plus' icon) 
5. When the victim inputs any password, for instance an ftp connection password, it will appear in the tab 'Passwords'


### Spoof a MAC Address ###
#### TMAC ####
It can be found at: `Module 08 Sniffing\MAC Spoofing Tools\`.

1. Choose the network adapter of the target machine
2. Specify a new MAC Address or choose 'Random MAC Address'
3. Click on 'Change Now!' to change the MAC Address

#### SMAC ####
It can be found at: `Module 08 Sniffing\MAC Spoofing Tools\`.

1. Choose the network adapter
2. Specify a new MAC Address or choose 'Random'
3. Select 'IPConfig' to look at the IPConfig information
4. Click on 'Update MAC' to change the MAC Address

#### Other MAC Address Changer Tools ####
* MAC Address Changer (https://www.novirusthanks.org)
* Change MAC Address (https://lizardsystems.com)
* Easy Mac Changer (GitHub)
* Spoof-Me-Now (https://sourceforge.net)


- - - -

## Perform Network Sniffing ##

### Password Sniffing ###
#### Wireshark ####
Wireshark is a network packet analyzer used to capture network packets and display packet data in detail. It uses Wincap to capture packets.

``` http.request.method=="POST" ```

To capture remote traffic in Windows (RDP):
   * In Windows: 'Control Panel' > 'System and Security' > 'Administrative Tools' > 'Services' > 'Remote Packet Capture' > Start
   * In Wireshark: 'Capture' > 'Options' > 'Manage Interfaces' > 'Remote Interfaces' > 'Add' Button > Select the host, port and credentials


### Analyze a Network ###
#### Capsa Network Analyzer ####
Capsa is a network analysis application for both LANs and WLANs which performs real-time packet capturing, 24x7 network monitoring, advanced protocol analysis, in-depth packet decoding and automatic expert diagnosis.

Select the network adapter > 'Start'. It shows MAC conversations, IP conversations, TCP conversations, UDP conversations, protocols, endpoints, services, process, applications, VoIP calls...

#### Omnipeek Network Protocol Analyzer ####
Omnipeek provides real-time visibility and expert analysis of each part of the target network. It performs analysis, drills down and fixes performance bottlenecks across multiple network segments.

'New Capture' > Select the 'Adapter' > 'OK' > 'Start Capture'. It shows packets, events, clients/servers, VoIP calls and media, flows, applications...

#### SteelCentral Packet Analyzer ####
SteelCentral provides a graphical console for high-speed packet analysis. It captures terabytes of packet data traversing the network, reads it, and displays it in a GUI.

Run it as Administrator. 'Devices' > 'Local System' > Select the Adapter.

#### Other Sniffing Tools ####
* Observer Analyzer (https://www.viavisolutions.com)
* PRTG Network Monitor (https://www.paessler.com)
* SolarWinds Deep Packet Inspection and Analysis (https://www.solarwinds.com)
* Xplico (https://www.xplico.org)


- - - - 

## Detect Network Sniffing ##
Network Sniffers can be detected by using various techniques, such as:
* Ping Method: Identifies a system on the network is running in promiscuous mode.
* DNS Method: Identifies sniffers in the network by analyzing the increase in network traffic.
* ARP Method: Sends a non-broadcast ARP to all nodes in the network; a node on the network running in promiscuous mode will cache the local ARP address.

### Detect ARP Poisoning in a Switched-Based Network ###
#### Cain & Abel ####
1. Configure > Sniffer > Select the Adapter
2. Click the 'Start/Stop Sniffer' icon (In between the folder icon and the 'nuclear' icon)
3. Go to the 'Sniffer' tab > Upper blue 'Plus' icon > 'Scan MAC Addresses'
4. Go to the APR tab (at the bottom) > Select the upper blue 'Plus' icon > Add the IPs to sniff
5. Click on the 'Start/Stop APR' icon ('nuclear' icon) - If 'Poisoning' appears in the 'Status', then an ARP Poisoning is taking place.

#### Hping3 ####
``` hping3 <IP> -c <N of packets - Ex. 10000> ``` - The victim machine pings the other ARP-poisoned machine

In the attacker machine, open Wireshark:
1. Preferences
2. Select the Protocol: 'ARP/RARP' > Select the option 'Detect duplicate IP address configuration' and 'Detect ARP Request Storms'
3. Start capturing packets
4. In the menu bar: 'Analyze' > 'Expert Info' - Warning messages will appear: 'Duplicate IP address configured'


### Detect ARP Attacks ###
#### Xarp ####
XArp is a security application that detects ARP-based attacks. It detects critical network attacks that firewalls cannot cover. It uses advanced techniques to detect ARP attacks. It can be found at: `Module 08 Sniffing\ARP Spoofing Detection Tools\`.

Set the Security Level to 'Aggressive' - Whenever an ARP Poisoning attack is detected, it will pop-up an alert.

#### Other ARP Spoofing Detection Tools ####
* Capsa Network Analyzer (https://www.colasoft.com)
* ArpON (https://sourceforge.net)
* ARP AntiSpoofer (https://sourceforge.net)
* ARPStraw (GitHub)


### Detect Promiscuous Mode ###
Promiscuous mode allows a network device to intercept and read each network packet that arrives in its entirety. The sniffer toggles the NIC of a system to promiscuous mode, so that it listens to all data transmitted on its segment. It can be detected using various tools.

#### Nmap ####
``` nmap --script=sniffer-detect <Target IP> ```

#### NetScan Tools Pro ####
'Manual Tools' > 'Promiscuous Mode Scanner' > 'Do Scan'
