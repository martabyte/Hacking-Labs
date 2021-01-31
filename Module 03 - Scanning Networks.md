# Module 03 - Scanning Networks #
#### Lab 01 ####
#### Lab 02 ####
#### Lab 03 ####
#### Lab 08 ####
#### Lab 09 ####
#### Lab 10 ####
#### Lab 11 ####


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

