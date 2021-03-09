# Module 03 - Scanning Networks #

## Overview ##
Types of Scanning:
 * **Port Scanning**: List open ports and services.
 * **Network Scanning**: List the active hosts and IP Addresses on a network.
 * **Vulnerability Scanning**: Shows the presence of known weaknesses.


## Perform Host Discovery ##
Host Discovery is the primary task in the network scanning process. It is used to discover live hosts in a network.

Examples of Host Discovery techniques:
 - ARP Ping Scan
 - UDP Ping Scan
   - ICMP Ping Scan
   - TCP Ping Scan
 - IP Protocol Scan

### Nmap ###
Nmap is a utility used for network discovery, network administration and security auditing. Zenmap it's the GUI version of Nmap. Nmap is located at: _Module 03 Scanning Networks\Scanning Tools\Nmap_.

**ARP Ping Scan** - ``` nmap -sn -PR <IP> ```

**UDP Ping Scan** - ``` nmap -sn -PU <IP> ```

**ICMP Echo Ping Scan** - ``` nmap -sn -PE <IP> ``` - Useful to determine if ICMP traffic is passing through a firewall.

**ICMP Timestamp Ping Scan** - ``` nmap -sn -PP <IP> ``` - Useful to determine whether the target host is live specifically when administrators block ICMP traffic.

**Address Mask Ping Scan** - ``` nmap -sn -PM <IP> ``` - Useful to determine whether the target host is live specifically when administrators block ICMP traffic.

**TCP SYN Ping Scan** - ``` nmap -sn -PS <IP> ``` - ACK response -> Host is active.
 
**TCP ACK Ping Scan** - ``` nmap -sn -PA <IP> ``` - RST response -> Host is active.

**IP Protocol Ping Scan** - ``` nmap -sn -PO <IP> ``` - Sends different probe packets of different IP protocols. Any response -> Host is alive.
   
**Ping Sweep** - ``` nmap -sP <IP Range> ``` - For checking all the systems alive in the network


### Angry IP Scanner ###
Angry IP Scanner is an open-source and cross-platform network scanner designed to scan IP Addresses and ports. Angry IP Scanner is located at: _Module 03 Scanning Networks\Ping Sweep Tools\Angry IP Scanner_

 * Ping Method: Combined UDP+TCP
 * Display: Alive Hosts (Responding to Ping)
 
### IP Scanner ###
To scan for active hosts. Any host can be clicked and select for instance 'Traceroute' and see the route to the destination.

### IP Tools ###
Scanning Network Traffic going through a computer's adapter

 * Name Scanner - Enumerates all system names
 * Port Scanner - Scans for open ports in all hosts
 * UDP Scanner - Scans for open UDP ports in all hosts
 * Ping Scanner - Scans for alive hosts on the network

### Other Tools to Perform Ping Sweep ###
#### SolarWinds Engineer's Toolset ####
#### NetScan Tools Pro ####
#### Colasoft Ping Tool ####
#### Visual Ping Tester ####
#### OpUtils ####

- - - -

## Perform Port and Service Discovery ##
 * TCP Scanning
   * TCP Connect / Full Open Scan
   * Stealth TCP Scanning Methods
     * Half-Open / Stealth Scan
     * Inverse TCP Flag Scan
     * ACK Flag Probe Scan
     * Third Party and Spoofed TCP Scanning
 * UDP Scanning
 * SCTP Scanning
   * SCTP INIT Scanning
   * SCTP COOKIE / ECHO Scanning
 * SSDP and List Scanning
 * IPv6 Scanning

### MegaPing ###
MegaPing is a toolkit that provides essential utilities used to detect live hosts and open ports in a network. It can also provide information such as open shared resources, open ports, services/drivers active, key registry entries, users and groups, trusted domains, printers... Some of the integrated tools are Ping, Traceroute, Whois, IP Scanner, NetBIOS Scanner, Port Scanner... MegaPing is located at: _Module 03 Scanning Networks\Scanning Tools\MegaPing_.

### NetScanTools Pro ###
NetScanTools Pro is an integrated collection of utilities that gathers information on the Internet and troubleshoots networks. It can research IPv4/IPv6 addresses, hostnames, domain names, e-mail addresses and URLs on the target network. NetScanTools Pro is located at: _Module 03 Scanning Networks\Scanning Tools\NetScanTools Pro_.

#### Manual Tools #### 
 * ARP Ping -> Ping an IPv4 address on the subnet (Option - Send Broadcast ARP, then Unicast ARP)
 * ARP Scan (MAC Scan) -> Find all active IPv4 devices on the subnet
 * Ping Scanner -> Results can be seen in the browser (Option - Use Default System DNS)
 * Port Scanner 

### Nmap ###
Nmap is located at: _Module 03 Scanning Networks\Scanning Tools\Nmap_.

**TCP Connect Scan** - ``` nmap -sT -T3 -A -v <IP> ``` - (_-v_ is Verbose, to include all hosts and ports in the output)

**Stealth TCP Scan** - ``` nmap -sS -v <IP> ```

**TCP XMAS Scan** - ``` nmap -sX -T4 -v <IP> ```
 * Linux
   * No response -> *Open*
   * RST -> *Closed*
 * Windows
   * RST -> *Open* and *Closed*
   * When the firewall is enabled -> No response: Nmap will show all ports as *'Open|Filtered'*.

**TCP Maimon Scan** - ``` nmap -sM -v <IP> ``` - A FIN/ACK probe is sent to the target.
  * No Response -> Open|Filtered
  * RST -> Closed
  
**ACK Flag Probe Scan** - ``` nmap -sA -T4 -v <IP> ```
  * No Response -> Filtered - There's a stateful firewall
  * RST -> Not Filtered

**UDP Scan**  - ``` nmap -sU -T5 -v <IP> ```

#### NULL Scan #### 
 * 'Profile Editor'
   * 'TCP Scan: Null Scan (-sN)'
   * 'Timing Template: Aggressive (-T4)'
   * - [x] 'Enable all advanced/aggressive options(-A)'
  
``` nmap -sN -T4 -A -v <IP> ```
 * RST -> _Closed_
 * No Response -> _Open_ or _Filtered_

**Intense Scan** - ``` nmap -T4 -A -v <IP Range> ``` - The Aggressive flag performs: OS Detection (-O), Version Scanning (-sV), Script Scanning (-sC) and Traceroute (--traceroute).

**IDLE Scan** - ``` nmap -Pn -p80 -sI <IP IDLE Host> <IP Target Host> ``` - Spoof source address
 * If port is not open -> Probe other ports

**SCTP INIT Scan** - ``` nmap -sY -v <IP> ```
 * INIT + ACK Chunk Response -> Open
 * ABORT Chunk Response -> Closed

**SCTP COOKIE ECHO Scan** - ``` nmap -sZ -v <IP> ```
 * No Response -> Open
 * ABORT Chunk Response -> Closed

**Service Version Detection** - ``` nmap -T4 -sV <IP Range - Ex. 10.10.10.* or 10.10.10.0/24> ```

  
### Hping3 ###
Hping3 is a command-line network scanning and TCP/UDP/ICMP/IP packet crafting tool. Hping3 is in the Kali/Parrot machine.

``` hping3 -c X <IP> ``` - Only send X packets

**ACK Scan** - ``` hping3 -A <IP> -p 80 -c 5 ```
  * No Response -> Filtered - There's a stateful firewall
  * RST -> Not Filtered, Closed

**SYN Scan** - ``` hping3 -8 -p 0-100 -S <IP> -V ``` - Where _-8_ specifies a scan mode and _-V_ is verbose.

**FIN, PUSH and URG Scan** - ``` hping3 -F -P -U <IP> -p 80 -c 5 ```

**TCP Stealth Scan** - ``` hping3 --scan <Port Range> -S <IP> ```

**ICMP Scan** - ``` hping3 -1 <IP> -p 80 -c 5 ```

**Live Host Discovery in an Entire Network** - ``` hping3 -1 <Target Subnet> -rand-dest -I <Interface - Ex. eth0> ```

**UDP Scan** - ``` hping3 -2 <IP> -p 80 -c 5 ```

### Other Port Scanning Tools ###
#### Port Scanner ####

- - - -

## Perform OS Discovery ##
Banner Grabbing, or OS Fingerprinting, is a method used to determine the OS running on a remote system. There are two types:
 * **Active Banner Grabbing** - Crafted packets are sent to the remote OS and the responses are analyzed.
 * **Passive Banner Grabbing** - Analyzing error messaes, sniffing the network traffic and banner grabbing from page extensions.
 
The TTL and TCP Window Size fields values differ for different OSs. If these values can be recovered, the OS can be guessed.

OS | TTL | TCP Window Size
| :---: | :---: | :---:
Linux (Kernel 2.4 and 2.6) | 64 | 5840
Google Linux | 64 | 5720
FreeBSD | 64 | 65535
OpenBSD | 64 | 16384
Windows 95 | 32 | 8192
Windows 2000 | 128 | 16384
Windows XP | 128 | 65535
Windows Vista and 7 (Server 2008) | 128 | 8192
iOS 12.4 (Cisco Routers) | 255 | 4128
Solaris 7 | 255 | 8760
AIX 4.3 | 64 | 16384


### Wireshark ###
Using Wireshark, Ping and Nmap to analyze TTL and Window Sizes for OS Fingerprinting. Wireshark is located at: _Module 03 Scanning Networks\Banner Grabbing Tools\Wireshark_.

 1. ``` ping <IP> ``` from the target machine
 2. In Wireshark: Select the packet
 3. 'Internet Protocol Version 4' header -> TTL Header
 4. ``` nmap -sT <IP> ``` from the target machine [[ **TODO** - Check if this works ]]
 5. 'Transport Layer Protocol' header -> Window size

### Nmap ###
**OS Fingerprinting** - ``` nmap -O <IP> ```

**SMB Discovery** - ``` nmap --script smb-os-discovery.nse <IP> ``` - Determine OS, computer name, domain, workgroup and current time over SMB protocol (Ports 139 or 445).

### Unicornscan ###
Unicornscan is a command-line network information gathering and reconnaissance tool. It enables to disover open ports, services, TTL values (to discover the OS)...

**Immediate Mode with Verbose** - ``` unicornscan <IP> -Iv ``` - The TTL can be seen in the response, and can be compared to the table above to discover the OS.


- - - -

## Scan Beyond IDS and Firewall ## 
It consists of scanning without being detected by the network security perimeters. The techniques used to evade Firewalls and IDS are:
 * Packet Fragmentation
 * Source Routing
 * Source Port Manipulation
 * IP Address Decoy
 * IP Address Spoofing
 * Creating Custom Packets
 * Randomizing Host Order
 * Sending Bad Checksums - Sending the packets with bad or bogus TCP/UDP checksums
 * Proxy Servers
 * Anonymizers - To bypass Internet censors

### Nmap ###
#### Fragmentation of IP Packets to Avoid Detection #### 
```nmap -f <IP> ``` -> IP Fragmentation
 * Windows with firewall -> Filtered (Won't appear on the list of open ports)
 
``` nmap -mtu X <IP> ``` -> Maximum Transmission Unit (X byte fragments - Ex. 8) - Also forces fragmentation, should get the same results as '-f'

**Source Port Manipulation** - ``` nmap -g 80 <IP> ``` or ``` nmap --source-port 80 <IP> ```

#### Multiple Decoy IP Addresses to Avoid Scanning Detection #### 
``` nmap -D RND:X <IP> ``` -> Random X Decoys (Ex. 10 Decoys > X=10)
 * In the target machine, it will appear as the packets are coming from different IP addresses
 
**Append Custom Binary Data** - ``` nmap <IP> --data <Hex String - Ex. 0xdeadbeef> ```

**Append Custom String** - ``` nmap <IP> --data-string <String - Ex. "Ph34r mu l33t sk1lls"> ```

**Append Random Data** - ``` nmap --data-length <Length of the Random Data - Ex. 5> <IP> ```

**Randomizing Host Order** - ``` nmap --randomize-hosts <IP> ```

**Send Bad TCP/UDP Checksums** - ``` nmap --badsum <IP> ```

**Trace Sent and Received Packets** - ``` nmap --packet-trace <IP Range> ``` - Breakdown of the messages sent

### Colasoft Packet Builder ###
It allows to create custom network packets. Colasoft Packet Builder is located at: _Module 03 Scanning Networks\Packet Crafting Tools\Colasoft Packet Builder_.

0. Check the 'Adapter' settings
1. Add > ARP Packet - 0.1 Delta Second
2. Fields can be changed
3. Send All Packets - Burst Mode (No delay between packets)
4. Export All Packets - Can be opened in Wireshark

Now, if we had a Wireshark already running, we could analyze the ARP Responses to check the live systems in the network.

### Hping3 ###
**UDP Scan with a random source IP and a packet size of 500** - ``` hping3 <IP> --udp --rand-source --data 500 ``` 

**TCP SYN Scan** - ``` hping3 -S <IP> -p 80 -c 5 ```

**TCP Flooding the Target** - ``` hping3 <IP> --flood ```

### Other Packet Crafting Tools ###
#### NetScanTools Pro ####
#### Ostinato ####
#### WAN Killer ####

### Proxy Switcher ###
Proxy Switcher allows to surf the Internet anonymously without disclosing the IP Address of the system, and can access blocked sites in the organization. Proxy Switcher is located at: _Module 03 Scanning Networks\Proxy Tools\Proxy Switcher_.


### CyberGhost VPN ###
CyberGhost VPN hides the original IP and replaces it with one of their choice, allowing to surf the Internet anonymously and access blocked or censored content. It encrypts the connection and does not keep logs. CyberGhost VPN is located at: _Module 03 Scanning Networks\Proxy Tools\CyberGhost VPN_.

### Other Proxy Tools ###
#### Burp Suite ####
#### Tor ####
#### CCProxy ####
#### Hotspot Shield ####

- - - -

## Drawing Network Diagrams ##
It assists in identifying the topology or architecture of a target network. It also helps to trace the path to a target host in the network, and also identify the position of firewalls, IDSs, routers...

### SolarWinds Network Topology Mapper ###
Discovers a network and draws comprehensive network diagrams that integrate OSI Layer 2 and 3 topology data. SolarWinds Network Topology Mapper is located at: _Module 03 Scanning Networks\Network Discovery Tools\Network Topology Mapper_.

 * New Scan + Configure Password
 * SNMP Credentials
   * Stored Credentials -> Private
   * Discovery Credentials -> Public
 * Network Selection > IP Range
 * Discovery Settings > Scan Name
 * Scheduling > Frequency: Once, and 'Yes, run the discovery now'

#### Establish a Remote Desktop Connection ####
Right-Click on the node and select: 'Integration with Windows Tools' > 'Remote Desktop'
(It also has options for Ping, Telnet and Traceroute)

### Other Network Discovery Tools ###
#### OpManager ####
#### The Dude ####
#### NetSurveyor ####
#### Spiceworks Network Mapping Tool ####

- - - -

## Perform Network Scanning ##
Network Scanning tools can identify live hosts, information about all TCP/UDP open ports, running services on a target network, location information, NetBIOS information...

### Metasploit ###
Metasploit Framework is a tool that provides information about security vulnerabilities in the target system, and aids in penetration testing and IDS signature development. It has a modular approach, allowing the combination of any exploit with any payload. 

#### First Steps ####
1. ``` service postgresql start ```
2. ``` msfconsole ```
3. ``` db_status ``` - If the message is 'postgresql selected, no connection', continue the steps
4. ``` exit ```
5. ``` msfdb init ```
6. ``` service postgresql restart ```
7. ``` msfconsole ```
8. ``` db_status ``` - The message should be: 'Connected to msf'

#### Information Gathering using Metasploit ####
``` nmap -Pn -sS -A -oX <IP Range - Subnet> ``` - Once it is finished, type ``` db_import <Name - Ex. Test>```

Now, the information is saved in Metasploit. If we wanted to see the list of live hosts: ``` hosts ```. It will update itself with new information found when we continue scanning the hosts found. If we wanted to see the list of services running on the active hosts: ``` services ``` or ``` db_services ```.

#### Port Scanning using MSF Modules ####
* SYN Scan
  1. ``` search portscan ```
  2. ``` use auxiliary/scanner/portscan/syn ```
  3. ``` set INTERFACE <Interface - Ex. eth0> ```, ``` set PORTS <Target Port> ```, ``` set RHOSTS <Target IP or Range - Ex. 10.10.10.5-21> ```, ``` set THREADS <Concurrent Threads - Ex. 50> ```
  4. ``` exploit ```
 
* TCP Scan
  1. ``` back ```
  2. ``` use auxiliary/scanner/portscan/tcp ```
  3. ``` hosts -R ``` - To automatically set the RHOSTS option with the discovered hosts in the Information Gathering phase.
  4. ``` exploit ```
 
#### OS Version Discovery ####
* SMB Version Scan
  1. ``` back ```
  2. ``` use auxiliary/scanner/smb/smb_version ```
  3. ``` set RHOSTS <Target IP Range> ```, ``` set THREADS 11 ```
  4. ``` exploit ```

* FTP Version Identification
  1. ``` back ```
  2. ``` use auxiliary/scanner/ftp/ftp_version ```
  3. ``` set RHOSTS <Target IP (where port 21 has been identified)> ```
  4. ``` exploit ```

#### Export Scan Result ####
``` hosts -o <Output Path - CSV File> ```

- - - -

## Extra - Tools and Techniques ##

Category | Tools 
| :---: | :---
Frameworks | Kali Linux, Parrot OS, Backtrack5 R3, Security Onion
Reconnaissance | Smartwhois, MxToolbox, CentralOps, dnsstuff, nslookup, DIG, Netcraft
Discovery | Angry IP Scanner, Colasoft Ping Tool, Nmap, Maltego, NetResident, LanSurveyor, OpManager
Port Scanning | Nmap, MegaPing, Hping3, Netscan Tools Pro, Advanced Port Scanner
Service Fingerprinting | Xprobe, Nmap, Zenmap
Enumeration | Superscan, NetBIOS Enumerator, SnmpCheck, onesixtyone, Jxplorer, Hyena, DumpSec, WinFingerprint, Ps Tools, NsAuditor, Enum4Linux, nslookup, Netscan
Scanning | Nessus, GFI Languard, Retina, SAINT, Nexpose
Password Cracking | Ncrack, Cain & Abel, LC5, Ophcrack, pwdump7, fgdump, John the Ripper, Rainbow Crack
Sniffing | Wireshark, Ettercap, Capsa Network Analyzer
MiTM Attacks | Cain & Abel, Ettercap
Exploitation | Metasploit, Core Impact
