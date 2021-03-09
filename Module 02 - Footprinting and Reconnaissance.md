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


## Perform Email Footprinting ##
Email Footprinting allows you to collect information such as IP Addresses, mail servers, OS details, geolocation, service providers... This kind of tracking is possible through digitally time-stamped records that reveal the time and date when the target receives and opens a specific email.

### eMailTrackerPro ###
'View' > 'My Trace Reports' > 'New Email Trace' > 'Trace Headers' > 'Trace an email I have received', Paste the header of the email - To trace suspicious emails

### Other Email Tracking Tools ###
* Infoga (GitHub)
* Mailtrack (https://mailtrack.io)


## Perform Whois Footprinting ##
* DomainTools (http://whois.domaintools.com)
* SmartWhois (https://tamos.com)
* Batch IP Converter (http://www.sabsoft.com)


## Perform DNS Footprinting ##
### nslookup ###
```
nslookup
set type=<a, cname, any...>
<domain>
```
### Other DNS Lookup Tools ###
* Nslookup Online Utility (http://www.kloth.net/services/nslookup.php)
* Professional Toolset (https://tools.dnsstuff.com)
* DNS Records (https://network-tools.com)

### Reverse IP Domain Check and DNSRecon ###
* You Get Signal (https://www.yougetsignal.com > 'Reverse IP Domain Check')
* Dnsrecon (Command Line - `dnsrecon -r <IP/IP Range (X-X)>`)


## Perform Network Footprinting ##
### Network Range ###
* ARIN Whois Database Search Tool (https://arin.net/about/welcome/region)

### Network Tracerouting ###
#### Traceroute ####
* `tracert <URL>` (Windows)
* `traceroute <URL>` (Linux)

#### Path Analyzer Pro ####
It can be found at: `Module 02 Footprinting and Reconnaissance\Traceroute Tools\`.

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

#### Other Network Tracerouting Tools ####
* VisualRoute (http://visualroute.com)
* Traceroute NG (https://www.solarwinds.com)


## Perform Footprinting using Various Footprinting Tools ##
### Recon-ng ###
Web reconnaissance framework with independent modules and database interaction that provides an environment to perform web-based reconnaissance.

* Network Reconnaissance:
  ```
  recon-ng
  > help
  > marketplace install all (To install all modules)
  > modules search
  > workspaces 
  > workspaces create CEH
  > workspaces list
  > db insert domains
   > domain: <desired domain>
   > notes: <any notes>
  > show domains
  > modules load brute (To look for modules that contain 'brute')
  > modules load recon/domains-hosts/brute_hosts (To harvest hosts-related information)
  > run
  ```

  Other modules such as Netcraft or Bing can be used to harvest more hosts:
  ```
  > back
  > modules load recon/domains-hosts/bing_domain_web
  > run
  ```

  To perform a reverse lookup for each IP Address obtained during the reconnaissance:
  ```
  > back
  > modules load reverse_resolve
  > modules load recon/hosts-hosts/reverse_resolve
  > run
  > show hosts (To show all harvested hosts so far)
  ```

  To generate a report:
  ```
  > back
  > modules load reporting
  > modules load reporting/html
  > options set FILENAME <path>/results.html
  > options set CREATOR <Name>
  > options set CUSTOMER <Domain Name / Name of the Client>
  > run
  ```

* Gather Personnel Information
  To obtain the contacts related to the domains:
  ```
  recon-ng
  > workspaces create reconnaissance
  > modules load recon/domains-contacts/whois_pocs
  > info
  > options set SOURCE facebook.com (Sets facebook.com as the target domain)
  ```
  
  Validate the existence of usernames on specific websites:
  ```
  > back
  > modules load recon/profiles-profiles/namechk
  > options set SOURCE MarkZuckerberg (To look for the username MarkZuckerberg)
  > run
  ```
  
  To find the existence of user-profiles on various websites
  ```
  > back
  > modules load recon/profiles-profiles/profiler
  > options set SOURCE MarkZuckerberg (To look for the username on various websites)
  > run
  ```

### Maltego ###
Footprinting tool used to gather maximum information. It provides a library of transforms to discover data from open sources and visualizes that information in a graph format, suitable for link analysis and data mining.

It can be found at: `(Parrot) Applications > Pentesting > Information Gathering > Maltego > 'Maltego CE'`. To register a Maltego CE account: 'https://www.maltego.com/ce-registration'.

'Right Click' > 'All Transform' > Select the desired options.

### OSRFramework ###
OSRFramework is a set of libraries that are used to perform Open Source Intelligence tasks. They include references to many different applications related to username checking, DNS lookups, information leaks research, deep web search... It provides a way of making queries graphically as well as several interfaces to interact with such as OSRFConsole or a Web Interface.

It can be downloaded: `git clone https://github.com/i3visio/osrframework`. Or in Windows at: `Module 02 Footprinting and Reconnaissance\GitHub Tools\`.

```
pip3 install osrframework
pip3 install osrframework --upgrade
usufy.py -n <username> -p <target platforms - ex. twitter facebook youtube> (To check the existence of a profile of a user in target platforms)
domainfy.py -n <domain name - ex. eccouncil> -t all (Find existing domains using words and nicknames)
searchfy.py (Gather information about the users on social networking pages)
mailfy.py (Gather information about email accounts)
phonefy.py (Check for the existence of aa given series of phones)
entify.py (Extract entities using regular expressions from provided URLs)
```

### FOCA ###
FOCA (Fingerprinting Organizations with Collected Archives) is a tool that reveals metadata and shrouded data. It looks for records in Search Engines and examines a wide mixture of records, with the most widely recognized being Microsoft Office, Open Office or PDF documents. 

It can be found at: `Module 02 Footprinting and Reconnaissance\Footprinting Tools\FOCA\bin`.

### BillCipher ###
BillCipher is an information gathering tool for a website or IP address. It can gather information such as DNS Lookup, Whois Lookup, GeoIP Lookup, Subnet Lookup, Port Scanner, Page Links, Zone Transfer, HTTP Header...

It can be downloaded: `git clone https://github.com/GitHackTools/BillCipher`. Or in Windows at: `Module 02 Footprinting and Reconnaissance\GitHub Tools\`.

```
python3 billcipher.py
> website/IP
> <target website or IP>

  1) DNS Lookup
  2) Whois Lookup
  3) GeoIP Lookup
  4) Subnet Lookup
  5) Port Scanner
  6) Page Links
  7) Zone Transfer
  8) HTTP Header
  9) Host Finder
  10) IP-Locator
  11) Find Shared DNS Servers
  12) Get Robots.txt
  13) Host DNS Finder
  14) Reverse IP Lookup
  15) Email Gathering (Infoga)
  16) Subdomain Listing (Sublist3r)
  17) Find Admin Login Site (Breacher)
  18) Check and Bypass CloudFare (HatCloud)
  19) Website Copier (HTTrack)
  20) Host Info Scanner (WhatWeb)
  21) About
  22) Fuck Out Of Here (Exit)

> <Number - Type of information to collect>
> Yes (To continue extracting information)
```

### OSINT Framework ###
OSINT Framework is an open-source intelligence gathering framework that helps in performing automated footprinting and reconnaissance, OSINT research, and intelligence gathering. It is focused on gathering information from free tools or resources. (It is like a list of available online tools)

https://osintframework.com/
