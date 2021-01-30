# Module 03 - Scanning Networks #
#### Lab 01 ####
#### Lab 02 ####
#### Lab 03 ####
#### Lab 08 ####
#### Lab 09 ####
#### Lab 10 ####
#### Lab 11 ####


### Nmap ### 
 * Zenmap -> GUI Nmap
 * ``` nmap -O <IP Range - Ex: 10.10.10.*> ``` -> OS Fingerprinting
   * Ports / Hosts found
   * Topology
   * Services found
 * ``` nmap --packet-trace <IP Range> ``` -> Breakdown of the messages sent
 * ``` nmap -sS -sU -T4 -A -v -PE -PP -PS80,443 -PA3389 -PU40125 -PY -g 53 --script "default or (discovery and safe)" <IP host>  ``` -> Slow comprehensive scan
   * **_[ TO DO ]_** Does it generate automatically from the results obtained before? So it personalizes the command?
   * Takes 15/20 minutes to run
 * ``` nmap -T4 -A -v <IP Range> ``` -> Intense Scan

 #### NULL Scan #### 
   * 'Profile Editor'
   * 'TCP Scan: Null Scan (-sN)'
   * 'Timing Template: Aggressive (-T4)'
   * - [x] 'Enable all advanced/aggressive options(-A)'

 * ``` nmap -sT -T3 -A <IP host> ``` -> TCP Connect Scan (5 minutes)
 * ``` nmap -sX -T4 <IP host> ``` -> XMAS Scan with Aggressive Timing
   * Linux
     * No response -> *Open*
     * RST -> *Closed*
   * Windows
     * RST -> *Open* and *Closed*
     * When the firewall is enabled -> No response: Nmap will show all ports as *'Open|Filtered'*.
 * ``` nmap -sA -v -T4 <IP> ``` -> ACK Scan. Displays port disposition.
 * ``` nmap -Pn -p80 -sI <IP IDLE Host> <IP Target Host> ``` -> IDLE Scan
   * If port is not open -> Probe other ports
 * ``` nmap -sP <IP Range> ``` -> Ping Sweep - For checking all the systems alive in the network
 * **_[ TO DO ]_** Try other types of scans such as TCP Flag Scan, Stealth Scan, etc

 #### Fragmentation of IP Packets to Avoid Detection #### 
   * ```nmap -f <IP> ``` -> IP Fragmentation
     * Windows with firewall -> Filtered (Won't appear on the list of open ports)
   * ``` nmap -mtu X <IP> ``` -> Maximum Transmission Unit (X byte fragments) - Also forces fragmentation, should get the same results as '-f'

 #### Multiple Decoy IP Addresses to Avoid Scanning Detection #### 
   * ``` nmap -D RND:X <IP> ``` -> Random X Decoys (Ex. 10 Decoys > X=10)
     * In the target machine, it will appear as the packets are coming from different IP addresses
  
#### NetScan Tools Pro #### 
 * Manual Tools
    * ARP Ping -> Ping an IPv4 address on the subnet (Option - Send Broadcast ARP, then Unicast ARP)
    * ARP Scan (MAC Scan) -> Find all active IPv4 devices on the subnet
    * Ping Scanner -> Results can be seen in the browser (Option - Use Default System DNS)
    * Port Scanner 

