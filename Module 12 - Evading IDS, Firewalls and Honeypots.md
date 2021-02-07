# Module 12 - Evading IDS, Firewalls and Honeypots #

## Detecting Intrusions ##

### Snort ###
``` cmd ``` > ``` snort ``` - To start the service

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

To configure specific Protocol rules, in the protocol_-info.rules_ file, add the necessary lines. Ex. '_icmp-info.rules_' > ``` alert icmp $EXTERNAL_NET any -> $HOME_NET any (msg:"ICMP-INFO PING"; icode:0; itype:8; reference:arachnids,135; reference:cve,1999-0265; classtype:bad-unknown; sid:472; rev:7;) ```

``` snort -i <Nº of Interface> -A console -c <Snort.conf File Path> -l <Snort\log Dir Path> -K ascii ``` - To run Snort in **IDS mode**


- - - -

## Detecting Malicious Network Traffic ##

### HoneyBOT ###
Leave the default settings and add the 'Export logs to CSV' option. It will start running. Whenever any host is trying to make a connection to any port, it will be logged into the application, allowing to select and view the details of every packet, and showing the packets by port or by host.


- - - -

## Bypassing Windows Firewall ##

### Nmap ###
``` nmap -v -sS -f --mtu <Value - Ex. 32> --send-eth --data-length 500 --source-port 99 -T5 <Target IP> ``` - 
  * The _-f_ switch makes the scan use fragmented IP packets to avoid firewall inspection. 
  * The _mtu_ switch creates packets with the specified maximum size.
  * The _send-eth_ switch sends Ethernet level packets, to bypass the IP layer and send raw Ethernet frames within the traffic.
  * The _data-length_ switch will append the given number of random bytes, so it will not use any protocol-specific payloads.
  * The _source-port_ switch will spoof the source port number.

### HTTP/FTP Tunneling ###
??
### Metasploit ###
??



