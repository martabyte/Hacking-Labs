# Module 02 - Footprinting and Reconnaissance #
Footprinting (aka Reconnaissance) refers to collecting information about a target network and its environment, which is the first step in any attack on a system. It helps attackers to narrow down the scope of their efforts and aids in the selection of weapons and the strategy of the attack.

### Objectives ###
To gather:

* Organization Information - Employee details, partner details, weblinks, web technologies, patents, trademarks...
* Network Information - Domains, sub-domains, network blocks, network topologies, trusted routers, firewalls, IPs, Whois record, DNS records...
* System Information - OS, Web Servers OS, user accounts and passwords...

## Footprinting through Search Engines ##
## Footprinting through Web Services ##
## Footprinting through Social Networking Sites ##
## Perform Website Footprinting ##

## Open Source Information Gathering ##

### Windows Command Line Utilities ###

<kbd>Windows Key + R </kbd> > ``` cmd ```

#### Resolving the IP ####
``` ping <URL> ``` 

#### Find the Maximum Frame Size on the Network ####
``` ping <URL> -f -l <Length of the Packet - Ex. 1500> ``` - Analyze the response:

  * 'Packet needs to be fragmented but DF set' -> The frame is too large to be on the network. Try again reducing the length of the packet.
  * OK -> The frame size is smaller than the limit, try increasing the length of the packet.

#### Mapping the routers between you and the target ####
``` tracert <URL> ```


- - - -

## Collecting Information About a Target Website ##

### Firebug ###
Firefox browser > 'Firebug' extension

  * Inspector
  * Console
  * Debugger
  * Style Editor
  * Performance
  * Memory
  * Network
  * DOM


- - - -

## Mirroring a Website ##

### HTTrack Web Site Copier ###

'Set Options' > 'Scan Rules' - You can specify the type of files you want to download.


- - - -

## Advanced Network Route Tracing ##

### Path Analyzer Pro ###
Options:
* Protocol
  * ICMP
  * UDP
  * Source Port
  * Tracing Mode
* Advanced Probe Details
  * Length of Packet
  * Lifetime
  * Type-of-Service
  * Maximum TTL
  * Initial SEQ Number
* Advanced Tracing Details
  * Work-ahead Limit
  * Minimum Scatter
  * Prbes per TTL
  * Stop on Control Messages (ICMP)
  
Results:
* Report
* Synopsis
* Charts
* Geo
* Log
* Stats
