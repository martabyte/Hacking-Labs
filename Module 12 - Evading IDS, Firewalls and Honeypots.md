# Module 12 - Evading IDS, Firewalls and Honeypots #

## Detecting Intrusions ##
### Snort ###
Snort is an open-source network IDS capable of performing real-time traffic analysis and packet logging on IP networks. It can perform protocol analysis and content searching/matching, and it is used to detect a variety of attacks and probes such as buffer overflows, stealth port scans, CGI attacks, SMB probes and OS fingerprinting attempts.

It can be found at: `Module 12 Evading IDS, Firewalls and Honeypots\Intrusion Detection Tools\`.

``` cmd ``` > (`cd <path>\Snort\bin`) > ``` snort ``` - To start the service

``` snort -W ``` - Lists the local machine's Physical Address, IP Address and Ethernet Drivers (Name and Description).

``` snort -dev -i <Nº of the Interface - Ex. 1> ``` - To enable the interface's Ethernet Driver. Leave this window open, and observe the communication messages that appear.

To configure Snort rules: _'Snort\etc\snort.conf'_
* Configure the IP Address Snort is protecting - By default, it protects All the IPs in the network
    * In 'Step #1' > 'Setup the network addresses you are protecting' of the config file change the value 'any' to the IP (_ipvar HOME_NET any_)
* If the network is running any Server:
    1. Go the corresponding server line _DNS_SERVERS_, _SMTP_SERVERS_, _HTTP_SERVERS_, _SQL_SERVERS_, _TELNET_SERVERS_ or _SSH_SERVERS_, 
    2. Replace _$HOME_NET_ with the IP of the Server
* Configure the Rule Path (_var RULE_PATH_) to an absolute value - Ex. _C:\Snort\rules_. The same with the _SO_RULE_PATH_ and _PREPROC_RULE_PATH_, _WHITE_LIST_PATH_, _BLACK_LIST_PATH_, _dynamicpreprocessor_, _dynamicengine_, _classification.config_ and _reference.config_.
* Create the whitelist and blacklist files: _white_list.rules_ and _black_list.rules_.
* Replace all _ipvar_ to _var_.
* Comment the _dynamicdetection_ line and all the _preprocessor_ lines.
* Delete (only) 'lzma' from the _decompress_swf_ line.

To configure specific Protocol rules, in the protocol_-info.rules_ file, add the necessary lines. Ex. '_icmp-info.rules_' > ``` alert icmp $EXTERNAL_NET any -> $HOME_NET any (msg:"ICMP-INFO PING"; icode:0; itype:8; reference:arachnids,135; reference:cve,1999-0265; classtype:bad-unknown; sid:472; rev:7;) ```

``` snort -i <Nº of Interface> -A console -c <Snort.conf File Path> -l <Snort\log Dir Path> -K ascii ``` - To run Snort in **IDS mode**


## Detecting Malicious Network Traffic ##
### ZoneAlarm Free Firewall 2019 ###
ZoneAlarm manages and monitors all incoming and outgoing traffic and shields the network from attackers. It can be found at: `Module 12 Evading IDS, Firewalls and Honeypots\Firewalls\`.

'FIREWALL' > 'Basic Firewall' > 'View Zones' > 'Add >>' > 'Host/Site'. Select 'Zone': 'Blocked', 'Host Name': (the name of the site to be blocked), 'Description': (Whatever you want) > 'Lookup'. When the IP appears, select 'OK'.

### Other Firewalls ###
* ManageEngine Firewall Analyzer (https://www.manageengine.com)
* pfSense (https://pfsense.org)
* Sophos XG Firewall (https://www.sophos.com)
* Comodo Firewall (https://personalfirewall.comodo.com)

### HoneyBOT ###
HoneyBOT is a medium-interaction honeypot for Windows. A Honeypot creates a safe environment to capture and interact with unsolicited traffic on a network. It can be found at: `Module 12 Evading IDS, Firewalls and Honeypots\Honeypot Tools\`.

Run it as Administrator. Leave the default settings and add the 'Export logs to CSV' option. It will start running. Whenever any host is trying to make a connection to any port, it will be logged into the application, allowing to select and view the details of every packet, and showing the packets by port or by host.


- - - -

## Bypassing Windows Firewall ##
### Nmap ###
``` nmap -v -sS -f --mtu <Value - Ex. 32> --send-eth --data-length 500 --source-port 99 -T5 <Target IP> ``` - 
  * The _-f_ switch makes the scan use fragmented IP packets to avoid firewall inspection. 
  * The _mtu_ switch creates packets with the specified maximum size.
  * The _send-eth_ switch sends Ethernet level packets, to bypass the IP layer and send raw Ethernet frames within the traffic.
  * The _data-length_ switch will append the given number of random bytes, so it will not use any protocol-specific payloads.
  * The _source-port_ switch will spoof the source port number.

``` nmap -sI <Zombie IP> <Target IP> ``` - To perform a Zombie scan by choosing another machine as the source IP


## Bypass Firewall Rules ##
Some firewall bypassing techniques: Port Scanning, Firewalking, Banner Grabbing, IP Address Spoofing, Source Routing, Proxy Servers, ICMP Tunneling, ACK Tunneling, HTTP Tunneling, SSH Tunneling, DNS Tunneling, MiTM...

### HTTP/FTP Tunneling ###
#### HTTHost ####
It can be found at: `Module 12 Evading IDS, Firewalls and Honeypots\HTTP Tunneling Tools\`.

In the victim machine:
1. 'Options' > Leave 90 as the port number, enter a personal password (ex. 'magic'), ensure that 'Revalidate DNS names' and 'Log Connections' is ticked on > 'Apply'
2. Go to 'Application Log' tab and ensure the listener is listening on port 90. Leave it running. 

#### HTTPort ####
It can be found at: `Module 12 Evading IDS, Firewalls and Honeypots\HTTP Tunneling Tools\`.

In the attacker machine: We will want to connect to HTTHost because in that machine the desired port is blocked (for instance: 'ftp: 21'). So we need to connect to port 90 to bypass the restriction.
1. 'Proxy' tab > Enter the hostname or IP, enter the Port number (in this example: 90), 'Bypass Mode': 'Remote Host', in the 'Use personal remote host at' re-enter the IP and port and put the password previously set ('magic'). > Do not click 'Start' yet
2. 'Port Mapping' tab > 'Add' > New Mapping - Right click: 'Edit' >  Select a name, 'Local Port': 21 (in this example for 'ftp'), 'Remote Host': victim host, and 'Remote Port': 21.
3. Go back to the 'Proxy' tab and select 'Start'

Now, if you want to ftp the victim, you still won't be able to do it with 'ftp <Target IP>' (in the cmd), but you will be able to by entering: 'ftp 127.0.0.1'.

