# Module 13 - Hacking Web Servers #

## Information Gathering ##
### Ghost Eye ###
It gathers info such as Whois lookup, DNS lookup, EtherApe, Nmap port scan, HTTP header grabbing, clickjacking test, scans robot.txt, link grabber, IP location finder, have i been pwned and traceroute.

It can be downloaded: ` git clone https://github.com/BullsEye0/ghost_eye.git `. Or in Windows at: `Module 13 Hacking Web Servers\GitHub Tools\`.

`cd ghost_eye`, `pip3 install -r requirements.txt` 
```
python3 ghost_eye.py
> (Enter your choice): 1 (for Whois Lookup), 2 (for DNS Lookup), 5 (for HTTP Header Grabber), 6 (for Clickjacking Test) ...
> (Enter the Domain or IP Address): <Target IP>
```

## Web Server Reconnaissance ##
### Skipfish ###
Skipfish is an active web application security reconnaissance tool. It prepares an interactive sitemap for the targeted site by carrying out a recursive crawl and dictionary-based probes. The resulting map is then annotated with the output from a number of active security checks. The final report provided by the tool is meant to serve as a foundation for deeper web application security assessments.

``` skipfish -o <Output Dir> -S <Dictionary File - Ex. /usr/share/skipfish/dictionaries/complete.wl> <URL> ``` - When finished, navigate to the output directory and open the _index.html_ file, where the findings will be shown.


## Footprinting a Web Server ##
### httprecon ###
It can be found at: `Module 13 Hacking Web Servers\Web Server Footprinting Tools\`.

1. Configure the Target and port.
2. 'Analyze'

### ID Serve ###
It can be found at: `Module 13 Hacking Web Servers\Web Server Footprinting Tools\`.

Enter the URL, Query the Server, and it will provide you with the Server info it returns.

### Netcat ###
```
nc -vv <URL> <Port>
> GET / HTTP/1.0
```

### Telnet ###
```
telnet <URL> <Port>
> GET / HTTP/1.0
```

## Enumerating a Web Server ##
### Nmap ###
`nmap -sV --script=http-enum <URL>` 

`nmap --script hostmap-bfk -script-args hostmap-bfk.prefix=hostmap- <URL>` - To discover the hostnames that resolve the targeted domain

`nmap --script http-trace -d <URL>` - To perform an HTTP trace

`nmap -p<Port - ex. 80> --script http-waf-detect <URL>` - To check whether there's a WAF configured


## Cracking FTP Credentials ##
### Hydra ###
To perform a Dictionary Attack against an FTP service.

``` hydra -L <Username Wordlist File> -P <Password Wordlist File> ftp://<Target IP> ```


## Web Server Fingerprinting ##
### Uniscan ###
``` uniscan -u <URL> -q ``` - The switch _-q_ is to enable directory checks.

``` uniscan -u <URL> -we ``` - The switch _-w_ and _-e_ used together is to enable file check, robots.txt and sitemap.xml check.

``` uniscan -u <URL> -d ``` - The switch _-d_ is to perform a dynamic scan. It can find vulnerabilities like SQL Injection, XSS, RCE, RFI...

In `/usr/share/uniscan/report` there will be the scan report for the URL in an _html_ file.

### Other Web Server Fingerprinting Tools ###
* SpiderFoot (https://www.spiderfoot.net)
* httprint (https://www.net-square.com)
* Winfingerprint (https://qpdownload.com)
* NetworkMiner (https://www.netresec.com)
