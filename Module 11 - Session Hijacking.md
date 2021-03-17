# Module 11 - Session Hijacking #
Session Hijacking refers to the exploitation of a session token-generation mechanism or token security controls that enables an attacker to establish an unauthorized connection with a target server. Session Hijacking can be divided into three broad phases:
1. Tracking the Connection
2. Desynchronizing the Connection
3. Injecting the Attacker's Packet

## Perform Session Hijacking ##
### Zed Attack Proxy (ZAP) ###
ZAP is an integrated penetration testing tool for finding vulnerabilities in web applications. It offers automated scanners as well as a set of tools that allow you to find security vulnerabilities manually.

It can be found at: `Module 11 Session Hijacking\`.

* To modify a request or response (like in Burp): Tabs > Plus Sign > 'Break' tab
* To set up the local proxy: Options > Local Proxies

### bettercap ###
bettercap is a powerful, flexible and portable tool created to perform various types of MiTM attacks against a network, manipulate HTTP, HTTPS and TCP traffic in real-time, sniff for credentials...

` bettercap -h `

``` 
bettercap -iface <Interface> 
> help
> net.probe on (This module will send different types of probe packets to each IP in the current subnet)
> net.recon on (This module is responsible for periodically reading the system ARP table to detect new hosts on the network)
> set net.sniff.regexp '.*password=.+' (This module will consider only the packets sent with a payload matching the given regular expression)
(Wait for someone to enter credentials and it will be displayed)

``` 


## Detect Session Hijacking ##
It can be detected manually, through tools like Wireshark or SteelCentral Packet Analyzer, or automatically with IDS and IPS systems.

### Wireshark ###
For instance, bettercap sends several ARP broadcast requests to the hosts, so a high number of ARP requests indicates that the attacker system is acting as a client for all the IP addresses in the subnet, which means that the target hosts will send the info to the attacker instead of the gateway (MiTM).
