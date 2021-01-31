# Module 03 - Scanning Networks #

## Hping3 ##
UDP and TCP Packet crafting

``` hping3 -c X <IP> ``` - Only send X packets

``` hping3 --scan 1-3000 -S <IP> ``` - SYN Scan to ports 1-3000

``` hping3 <IP> --udp --rand-source --data 500 ``` - UDP Scan with random source IP(?) and Len=500

``` hping3 -S <IP> -p 80 -c 5 ``` - SYN Scan to port 80 and sending 5 packets

``` hping3 <IP> --flood ``` - Flooding the target


## Colasoft Packet Builder ##
Scanning the network

1. Add > ARP Packet - 0.1 Delta Second
2. Fields can be changed
3. Send All Packets - Burst Mode (No delay between packets)
4. Export All Packets - Can be opened in Wireshark


## Mega Ping ##
Basic network troubleshooting. Has options for Ping, Traceroute, Whois, IP Scanner, NetBIOS Scanner, Port Scanner...

#### IP Scanner ####
To scan for active hosts. Any host can be clicked and select for instance 'Traceroute' and see the route to the destination.

#### Port Scanner ####
Port Scanning on the target host(s).


## Nmap ## 
Zenmap -> GUI Nmap

#### OS Fingerprinting #### 
``` nmap -O <IP Range - Ex: 10.10.10.*> ```
  * Ports / Hosts found
  * Topology
  * Services found
 
#### Trace Sent and Received Packets #### 
``` nmap --packet-trace <IP Range> ``` - Breakdown of the messages sent
 
#### Slow Comprehensive Scan #### 
``` nmap -sS -sU -T4 -A -v -PE -PP -PS80,443 -PA3389 -PU40125 -PY -g 53 --script "default or (discovery and safe)" <IP host>  ``` 

**_[ TO DO ]_** Does it generate automatically from the results obtained before? So it personalizes the command?
(Takes 15/20 minutes to run)
   
#### Intense Scan #### 
``` nmap -T4 -A -v <IP Range> ``` -> Intense Scan

#### NULL Scan #### 
 * 'Profile Editor'
   * 'TCP Scan: Null Scan (-sN)'
   * 'Timing Template: Aggressive (-T4)'
   * - [x] 'Enable all advanced/aggressive options(-A)'
  
``` nmap -sN -T4 -A <IP> ```
 * RST -> _Closed_
 * No Response -> _Open_ or _Filtered_

#### TCP Connect Scan #### 
``` nmap -sT -T3 -A <IP host> ``` 
 
#### XMAS Scan #### 
``` nmap -sX -T4 <IP host> ``` 
 * Linux
   * No response -> *Open*
   * RST -> *Closed*
 * Windows
   * RST -> *Open* and *Closed*
   * When the firewall is enabled -> No response: Nmap will show all ports as *'Open|Filtered'*.
 
#### ACK Flag Scan #### 
``` nmap -sA -v -T4 <IP> ``` - Displays port disposition.
 
#### UDP Scan #### 
``` nmap -sU -T5 <IP> ```

#### IDLE Scan #### 
``` nmap -Pn -p80 -sI <IP IDLE Host> <IP Target Host> ``` 
 * If port is not open -> Probe other ports
   
#### Ping Sweep #### 
``` nmap -sP <IP Range> ``` - For checking all the systems alive in the network
 
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
 

## Wireshark ##
To analyze TTL and Window Sizes for OS Fingerprinting

 1. ``` ping <IP> ``` from the target machine
 2. In Wireshark: Select the packet
 3. 'Internet Protocol Version 4' header -> TTL Header
 4. ``` nmap -sT <IP> ``` from the target machine [[ **TODO** - Comprobar ]]
 5. 'Transport Layer Protocol' header -> Window size
 
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







