# Module 02 - Footprinting and Reconnaissance #
Footprinting (aka Reconnaissance) refers to collecting information about a target network and its environment, which is the first step in any attack on a system. It helps attackers to narrow down the scope of their efforts and aids in the selection of weapons and the strategy of the attack.

### Objectives ###
To gather:

* Organization Information - Employee details, partner details, weblinks, web technologies, patents, trademarks...
* Network Information - Domains, sub-domains, network blocks, network topologies, trusted routers, firewalls, IPs, Whois record, DNS records...
* System Information - OS, Web Servers OS, user accounts and passwords...

The tools are found at: `Module 02 Footprinting and Reconnaissance`.

## Footprinting through Search Engines ##
### Advanced Google Hacking Techniques ###
* intitle:
* site:
* filetype:
* cache:
* allinurl:
* inurl:
* allintitle:
* inanchor:
* link:
* related:
* info:
* location:

### Video Search Engines ###
* https://citizenevidence.amnestyusa.org/ -> Paste a Youtube video and get details such as Topic Abstract, ID, Upload Date and Time...
* Google Videos (https://video.google.com)
* Yahoo Videos (https://video.search.yahoo.com)
* Yahoo Images (https://images.search.yahoo.com)
* EZGif (https://EZGif.com)
* VideoReverser (https://videoreverser.com)
* TinEye Reverse Image Search (https://tineye.com)

### FTP Search Engines ###
* NAPALM FTP Indexer (https://www.searchftps.net)
* Global FTP Search Engine (https://globalfilesearch.com)
* FreewareWeb FTP File Search (https://freewareweb.com)
 
### IoT Search Engines ###
* Shodan (https://www.shodan.io)
* Censys (https://censys.io)
* Thingful (https://www.thingful.net)


## Footprinting through Web Services ##
### Find Domains and Subdomains ###
#### Netcraft ####
https://www.netcraft.com/ > Resources > Tools > Site Report: 'What's this site running?'

#### Other Tools ####
* Sublist3r
* Pentest-Tools Find Subdomains
* Fierce

### Gather Personal Information ###
* PeekYou Online People Search Service (https://www.peekyou.com)
* pipl (https://pipl.com)
* Intelius (https://www.intelius.com)
* BeenVerified (https://www.beenverified.com)

### Gather Email List ###
#### theHarvester ####
It gathers emails, subdomains, hosts, employee names, open ports and banners from different public sources...

``` theHarvester -d <domain> -l <n of results - ex. 200> -b <data source - ex. google, baidu, twitter, linkedin...> ```

### Gather Information using Deep and Dark Web Searching ###
#### Tor Browser ####
Tor Browser can be found at: `Module 02 Footprinting and Reconnaissance\Deep and Dark Web Footprinting Tools\`

* Hacker for Hire (https://hackerforhire.com)
* The Hidden Wiki - Listing of Onion websites
* FakeID - Create fake passports
* The Paypal Cent - Paypal accounts

#### Other Tools ####
* ExoneraTor (https://metrics.torproject.org)
* OnionLand Search Engine (https://onionlandsearchengine.com)

### Passive Footprinting to Determine the Target OS ###
* Censys (https://censys.io/domain?q=<domain>)
* Netcraft (https://www.netcraft.com)
* Shodan (https://www.shodan.io)


## Footprinting through Social Networking Sites ##
### theHarvester ###
It gathers emails, subdomains, hosts, employee names, open ports and banners from different public sources...

``` theHarvester -d <domain> -l <n of results - ex. 200> -b <data source - ex. twitter, linkedin...> ```

### Sherlock ###
```
git clone https://github.com/sherlock-project/sherlock.git (or from the Windows machine: File Explorer > 'smb://<IP>' and copy it)
cd sherlock
python3 -m pip install -r requirements.txt
(cd sherlock)
python3 sherlock.py <name to look for>
```

### Followerwonk ###
https://followerwonk.com/analyze

### Other Tools ###
* Social Searcher (https://www.socialsearcher.com)
* UserRecon (GitHub)
* Hootsuite (https://hootsuite.com)
* Sysomos (https://www.sysomos.com)


## Perform Website Footprinting ##
### Ping ###
#### Resolving the IP ####
``` ping <URL> ``` 

#### Find the Maximum Frame Size on the Network ####
``` ping <URL> -f -l <Length of the Packet - Ex. 1500> ``` - Analyze the response:

  * 'Packet needs to be fragmented but DF set' -> The frame is too large to be on the network. Try again reducing the length of the packet.
  * OK -> The frame size is smaller than the limit, try increasing the length of the packet.

#### Mapping the routers between you and the target ####
``` tracert <URL> ```

``` ping <URL> -i X ``` - i is the TimeToLive value, modify it until it does not respond with 'TTL expired in transit'.

### Website Informer ###
It gives information about the creation date, when it expires, owner, hosting company, registrar, IPs, DNS, email, whois... (https://website.informer.com).

### Web Data Extractor ###
It can be found at: `Module 02 Footprinting and Reconnaissance\Web Spiders\`.

(Up) 'New' > 'Session Settings' > 'Starting URL', 'Stay within full URL', 'Extract (All)' > 'Ok' > (Up) 'Start'

### Other Web Spiders ###
* ParseHub (https://www.parsehub.com)
* SpiderFoot (https://www.spiderfoot.net)

### HTTrack Web Site Copier ###
It can be found at: `Module 02 Footprinting and Reconnaissance\Website Mirroring Tools\`.

'Enter URL' > 'Set Options' > 'Scan Rules' - You can specify the type of files you want to download.

### Other Mirroring Tools ###
* NCollector Studio (http://www.calluna-software.com)
* WebCopy (https://www.cyotek.com)

### CeWL ###
To gather a wordlist from a target website.

` cewl -d <depth - ex. 2> -m <min word length - ex. 5> -w <output file> <URL> `


## Perform Email Footprinting ##
### eMailTrackerPro ###


## Perform Whois Footprinting ##
### DomainTools ###


## Perform DNS Footprinting ##
### nslookup ###
### Reverse IP Domain Check and DNSRecon ###


## Perform Network Footprinting ##
### Network Range ###
### Network Tracerouting ###
#### Path Analyzer Pro ####
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


## Perform Footprinting using Various Footprinting Tools ##
### Recon-ng ###
### Maltego ###
### OSRFramework ###
### FOCA ###
### BillCipher ###
### OSINT Framework ###




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

