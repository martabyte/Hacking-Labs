# Module 04 - Enumeration #

## NetBIOS Enumeration ##
#### Global Network Inventory Scanner ####
``` New Audit Wizard > IP Range Scan > Connect as the current logged on user / Connect as a different user (Administrator) ```

After the scan is done, you can select the IP and see all different information about it (NetBIOS, BIOS, User Groups, Users, Services, Installed Software, Shares, SNMP System, SNMP Devices, OS...).


## Enumerating Network Resources ##
#### Advanced IP Scanner ####
Specify range to scan (Ex. 10.10.10.1-254). Shows all live hosts in the network. It shows IP Address, MAC Address and Manufacturer information. It also shows details like Web Server information and Shares. It can shutdown a remote machine.

#### SuperScan ####
Can enumerate a lot a different information such as NetBIOS Name Table, MAC Addresses, Workstation Type, Users, Groups, RPC Endpoint Dump, Shares, Domains, Logon Sessions, Drives, Trusted Domains, Services, Registry...

#### NetBIOS Enumerator ####
Shows NetBIOS Names, Usernames, Domain, MAC Address, Round Trip Time (RTT), Time-to-Live (TTL). It doesn't need any previous authentication.

#### SoftPerfect Network Scanner ####
Gives Shared Resources and Basic Info about the node.

Right Click > Properties -> Shows all information.
Right Click > Open Device: As Web (HTTP), As Secure Web (HTTPS), As File Server (FTP), As Telnet, As Telnet to... -> Allows to connect to the remote machine.

#### Nmap ####
``` nmap -O <IP> ``` - OS Fingerprinting
  * If ports 135, 139, 455... are open -> Port 139 is using NetBIOS

#### Nbtstat ####
``` nbtstat -A <Target IP> ``` -> Shows NetBIOS information of the target host. Scans port 139.

#### Net Use ####
``` net use ``` -> Shows shared resources

``` net use \\<IP>\e ""\user:"" ``` -> To create a NULL session to the found resource. Also works with (_""/user:""_).


## Enumerating Resources in a Local Machine (NetBIOS Enumeration) ##
#### Hyena ####
Shows local Drives, Connections, Users, Groups, Printers, Shares, Sessions, Open Files, Services, Drivers, Events, Disk Space, User Rights, Performance, Scheduled Jobs, Registry and WMI.


## Enumerating Services ##
#### Nmap ####
``` nmap -sP <IP Range> ``` - Ping Sweep Scan

``` nmap -sS <IP> ``` - Stealth SYN Scan. Shows list of most commonly used open ports.

``` nmap -sSV -O <IP> -oN <Output File> ``` - Stealth SYN, Version Detection and OS Fingerprinting. Shows more information about the open ports than just the Stealth SYN Scan.


## SNMP Enumeration ##
#### Nmap ####
``` nmap -sU -p 161 <IP> ``` - SNMP Enumeration (Port 161 UDP)

``` nmap -sU -p 161 --script=snmp-brute <IP> ``` - Script that will extract the SNMP community string from the target machine

#### Metasploit: snmp_enum ####
``` msfconsole ``` > ``` use auxiliary/scanner/snmp/snmp_login ```

``` show options ``` > ``` set RHOSTS ``` (Set target host) > ``` exploit ```

``` use auxiliary/scanner/snmp/snmp_enum ``` > ``` set RHOSTS ``` (Set target host) > ``` exploit ```


## LDAP Enumeration ##
#### Active Directory Explorer (ADExplorer) ####
Shows: DC (Domain User details), CN (). Allows to change the 'Attribute' values of users.


## Windows / SMB enumeration ##
#### enum4linux ####
``` enum4linux -u <Username> -p <Password> -U <IP>``` - To get User information

``` enum4linux -u <Username> -p <Password> -o <IP>``` - To get OS information

``` enum4linux -u <Username> -p <Password> -P <IP>``` - To get Password Policy information

``` enum4linux -u <Username> -p <Password> -G <IP>``` - To get Groups information

``` enum4linux -u <Username> -p <Password> -S <IP>``` - To get Share Policy information





