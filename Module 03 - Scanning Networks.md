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

**UDP Scan with random source IP and Len=500** - ``` hping3 <IP> --udp --rand-source --data 500 ``` 

**Flooding the Target** - ``` hping3 <IP> --flood ```


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

## Scan Beyond IDS and Firewall ## (p247)

### Colasoft Packet Builder ###
Scanning the network

1. Add > ARP Packet - 0.1 Delta Second
2. Fields can be changed
3. Send All Packets - Burst Mode (No delay between packets)
4. Export All Packets - Can be opened in Wireshark

### Hping3 ###

### Nmap ###

### Proxy Switcher ###

### CyberGhost VPN ###


- - - -





- - - -

#### IP Scanner ####
To scan for active hosts. Any host can be clicked and select for instance 'Traceroute' and see the route to the destination.

#### Port Scanner ####
Port Scanning on the target host(s).


## Nmap ## 

 
#### Trace Sent and Received Packets #### 
``` nmap --packet-trace <IP Range> ``` - Breakdown of the messages sent
 
#### Slow Comprehensive Scan #### 
``` nmap -sS -sU -T4 -A -v -PE -PP -PS80,443 -PA3389 -PU40125 -PY -g 53 --script "default or (discovery and safe)" <IP host>  ``` 
**_[ TO DO ]_** Does it generate automatically from the results obtained before? So it personalizes the command?
(Takes 15/20 minutes to run)
 
#### TO DO #### 
**_[ TO DO ]_** Try other types of scans such as TCP Flag Scan, Stealth Scan, etc

#### Fragmentation of IP Packets to Avoid Detection #### 
```nmap -f <IP> ``` -> IP Fragmentation
 * Windows with firewall -> Filtered (Won't appear on the list of open ports)
``` nmap -mtu X <IP> ``` -> Maximum Transmission Unit (X byte fragments) - Also forces fragmentation, should get the same results as '-f'

#### Multiple Decoy IP Addresses to Avoid Scanning Detection #### 
``` nmap -D RND:X <IP> ``` -> Random X Decoys (Ex. 10 Decoys > X=10)
 * In the target machine, it will appear as the packets are coming from different IP addresses
  
  
## NetScan Tools Pro ## 
#### Manual Tools #### 
 * ARP Ping -> Ping an IPv4 address on the subnet (Option - Send Broadcast ARP, then Unicast ARP)
 * ARP Scan (MAC Scan) -> Find all active IPv4 devices on the subnet
 * Ping Scanner -> Results can be seen in the browser (Option - Use Default System DNS)
 * Port Scanner 


## SolarWinds Network Topology Mapper ##
To draw network diagrams.

 * New Scan + Configure Password
 * SNMP Credentials
   * Stored Credentials -> Private
   * Discovery Credentials -> Public
 * Network Selection > IP Range
 
#### Establish a Remote Desktop Connection ####
Right-Click on the node and select: 'Integration with Windows Tools' > 'Remote Desktop'
(It also has options for Ping, Telnet and Traceroute)


## Angry IP Scanner ##
Checking for Live systems

 * Ping Method: Combined UDP+TCP
 * Display: Alive Hosts (Responding to Ping)


## IP Tools ##
Scanning Network Traffic going through a computer's adapter

 * Name Scanner - Enumerates all system names
 * Port Scanner - Scans for open ports in all hosts
 * UDP Scanner - Scans for open UDP ports in all hosts
 * Ping Scanner - Scans for alive hosts on the network
 







