# Module 13 - Hacking Web Servers #

## Web Server Reconnaissance ##

### Skipfish ###
``` skipfish -o <Output Dir> -S <Dictionary File - Ex. /usr/share/skipfish/dictionaries/complete.wl> <URL> ``` - When finished, navigate to the output directory and open the _index.html_ file, where the findings will be shown.


- - - -

## Footprinting a Web Server ##

### httprecon ###
1. Configure the Target and port.
2. 'Analyze'

### ID Serve ###
1. Enter the URL, Query the Server, and it will provide you with the Server info it returns.


- - - -

## Cracking FTP Credentials ##

### Hydra ###
To perform a Dictionary Attack against an FTP service.

``` hydra -L <Username Wordlist File> -P <Password Wordlist File> ftp://<Target IP> ```


- - - -

## Web Server Fingerprinting ##

### Uniscan ###
``` uniscan -u <URL> -q ``` - The switch _-q_ is to enable directory checks.
``` uniscan -u <URL> -we ``` - The switch _-w_ and _-e_ used together is to enable file check, robots.txt and sitemap.xml check.
``` uniscan -u <URL> -d ``` - The switch _-d_ is to perform a dynamic scan. It can find vulnerabilities like SQL Injection, XSS, RCE, RFI...
