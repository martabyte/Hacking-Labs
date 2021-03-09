# Module 04 - Enumeration #
Enumeration is the process of extracting usernames, machine names, network resources, shares and services from a system or network.

## NetBIOS Enumeration ##
NetBIOS enumeration is a process of obtaining sensitive information about the target such as list of computers belonging to a target domain, network shares, policies... Windows uses NetBIOS for file and printer sharing. NetBIOS enumeration allows attackers to read or write to a remote computer system or lauch DoS attacks.

### Global Network Inventory Scanner ###
It can be found at: `Module 03 Scanning Networks\Scanning Tools\`.

``` New Audit Wizard > IP Range Scan > Connect as the current logged on user / Connect as a different user (Administrator) ```

After the scan is done, you can select the IP and see all different information about it (NetBIOS, BIOS, User Groups, Users, Services, Installed Software, Shares, SNMP System, SNMP Devices, OS...).

### SuperScan ###
Can enumerate a lot a different information such as NetBIOS Name Table, MAC Addresses, Workstation Type, Users, Groups, RPC Endpoint Dump, Shares, Domains, Logon Sessions, Drives, Trusted Domains, Services, Registry...

### NetBIOS Enumerator ###
Shows NetBIOS Names, Usernames, Domain, MAC Address, Round Trip Time (RTT), Time-to-Live (TTL). It doesn't need any previous authentication.

It can be found at: `Module 04 Enumeration\NetBIOS Enumeration Tools\`.

### SoftPerfect Network Scanner ###
Gives Shared Resources and Basic Info about the node.

Right Click > Properties -> Shows all information.
Right Click > Open Device: As Web (HTTP), As Secure Web (HTTPS), As File Server (FTP), As Telnet, As Telnet to... -> Allows to connect to the remote machine.

### Nmap ###
``` nmap -O <IP> ``` - OS Fingerprinting
  * If ports 135, 139, 455... are open -> Port 139 is using NetBIOS

``` nmap -sV -v --script nbstat.nse <Target IP> ```  - NetBIOS enumeration NSE Script (Stealth Scan)

``` nmap -sU -p 137 --script nbstat.nse <Target IP> ```  - NetBIOS enumeration NSE Script (UDP Scan)

### Windows Command-Line Utilities ###
#### Nbtstat ####
``` nbtstat -A <Target IP> ``` -> Shows NetBIOS information of the target host. Scans port 139.

``` nbstat -c ``` -> Lists the contents of the NetBIOS Name Cache of the remote computer

#### Net Use ####
``` net use ``` -> Shows shared resources

``` net use \\<IP>\e ""\user:"" ``` -> To create a NULL session to the found resource. Also works with (_""/user:""_).


## Enumerating Resources in a Local Machine (NetBIOS Enumeration) ##
### Hyena ###
Shows local Drives, Connections, Users, Groups, Printers, Shares, Sessions, Open Files, Services, Drivers, Events, Disk Space, User Rights, Performance, Scheduled Jobs, Registry and WMI.


## Enumerating Network Resources (NetBIOS, SMB...) ##
### Advanced IP Scanner ###
Specify range to scan (Ex. 10.10.10.1-254). Shows all live hosts in the network. It shows IP Address, MAC Address and Manufacturer information. It also shows details like Web Server information and Shares. It can shutdown a remote machine.

It can be found at: `Module 03 Scanning Networks\Ping Sweep Tools\`.


## Enumerating Services ##
### Nmap ###
``` nmap -sP <IP Range> ``` - Ping Sweep Scan

``` nmap -sS <IP> ``` - Stealth SYN Scan. Shows list of most commonly used open ports.

``` nmap -sSV -O <IP> -oN <Output File> ``` - Stealth SYN, Version Detection and OS Fingerprinting. Shows more information about the open ports than just the Stealth SYN Scan.


## SNMP Enumeration ##
SNMP is a protocol that runs on UDP and maintains and manages routers, hubs and switches on an IP network. SNMP Enumeration uses SNMP to extract information about network resources (hosts, routers, devices, shares...) and network information (ARP tables, routing tables, device-specific information, traffic statistics...).

### Nmap ###
``` nmap -sU -p 161 <IP> ``` - SNMP Enumeration (Port 161 UDP)

``` nmap -sU -p 161 --script=snmp-brute <IP> ``` - Script that will extract the SNMP community string from the target machine

### Metasploit: snmp_enum ###
``` msfconsole ``` > ``` use auxiliary/scanner/snmp/snmp_login ```

``` show options ``` > ``` set RHOSTS ``` (Set target host) > ``` exploit ```

``` use auxiliary/scanner/snmp/snmp_enum ``` > ``` set RHOSTS ``` (Set target host) > ``` exploit ```

### snmp-check ###
``` snmp-check <IP> ``` - Enumerates system information, user accounts, network information, routing information, running processes, open ports, shares...

### SoftPerfect Network Scanner ###
It can ping computers, scan ports, discover shared folders and retrieve information about network devices via WMI, SNMP, HTTP, SSH and PowerShell.

It can be found at: `Module 04 Enumeration\SNMP Enumeration Tools\`.

'Options' > 'Remote SNMP' > Select all options. 

Select IP Range > 'Start Scanning' - When finished: Select a Node > Right Click > 'Properties' / 'Open Device' (As HTTP, HTTPS, FTP, Telnet...)

### Other SNMP Enumeration Tools ###
* Network Performance Monitor (https://solarwinds.com)
* OpUtils (https://www.manageengine.com)
* PRTG Network Monitor (https://www.paessler.com)
* Engineer's Toolset (https://www.solarwinds.com)
* WhatsUp Gold (https://www.ipswitch.com)


## LDAP Enumeration ##
LDAP enumeration is used to generate a list of distributed directory services on the target system, allowing you to gather information about usernames, addresses, departmental details, server names...

### Active Directory Explorer (ADExplorer) ###
Shows the hierarchical structure: DC (Domain Component), CN (Common Name - Usernames), OU (Organizational Unit). Allows to change the 'Attribute' values of users.

### Other LDAP Enumeration Tools ###
* Softerra LDAP Administrator (https://www.ldapadministrator.com)
* LDAP Admin Tool (https://www.ldapsoft.com)
* LDAP Account Manager (https://www.ldap-account-manager.org)
* LDAP Search (https://securityxploded.com)
* JXplorer (http://www.jxplorer.org)


## NFS Enumeration ##
NFS is a type of file system that enables computer users to access, view, store and update files over a remote server. NFS Enumeration is a method by which exported directories and shared data on target systems is extracted.

### Enable NFS Service ###
1. Open Server Manager (in a Windows Server machine)
2. Dashboard > 'Add roles and features'
3. 'Server Roles' > 'File and Storage Services' > 'File and iSCSI Services' > 'Server for NFS' 
4. Next... Install

`nmap -p 2049 <IP>` - To check if it's open

### RPCScan ###
It can be downloaded: `git clone https://github.com/hegusung/RPCScan`. Or in Windows at: `Module 04 Enumeration\GitHub Tools\`.

`python3 rpc-scan.py <IP> --rpc`

### SuperEnum ###
It can be downloaded: `git clone https://github.com/p4pentest/SuperEnum`. Or in Windows at: `Module 04 Enumeration\GitHub Tools\`.

First create a 'target.txt' file with the target IP(s), then `./superenum`.


## DNS Enumeration ##
DNS Enumeration is a process that locates and lists all possible DNS records for a target domain, including usernames. DNS Enumeration can be performed using the following techniques:
* Zone Transfer
* DNS Cache Snooping
* DNSSEC Zone Walking

### DNS Zone Transfer ###
DNS Zone Transfer is the process of transferring a copy of the DNS zone file from the primary DNS Server to a secondary DNS Server. If the DNS Transfer setting is enabled on the target DNS Server, it will give DNS information, if not, it will return an error saying it has failed or refusing to perform the zone transfer.

```
dig ns <URL / Target Domain> (Name Servers in URL)
dig @<Name Server> <URL / Target Domain> axfr (Retrieves zone information)

nslookup 
set querytype=soa (SOA - administrative information about the DNS zone of the target domain)
<domain>

nslookup
ls -d <Name Server> (Requests a Zone Transfer)
```

### DNSSEC Zone Walking ###
DNSSEC Zone Walking is a technique that is used to obtain the internal records of the target DNS Server if the DNS Zone is not properly configured. The enumerated zone information can assist you in building a host network map.

```
dnsrecon -h
dnsrecon -d <target domain> -z (To perform a DNS Zone Walk)
```

### Other DNS Enumeration Tools ###
* LDNS (https://www.nlnetlabs.nl)
* nsec3map (GitHub)
* nsec3walker (https://dnscurve.org)
* DNSWalk (GitHub)


## RPC, SMB and FTP Enumeration ##
* RPC Enumeration - Enumerating RPC endpoints enables vulnerable services on these service ports to be identified.
* SMB Enumeration - Enumeraing SMB services enables banner grabbing, which obtains info such as OS details and versions of services running.
* FTP Enumeration - Enumerating FTP services yields information about port 21 and any running FTP services. This info can be used to launch various attacks such as FTP Bounce, FTP Brute Force and packet sniffing.

### NetScanTools Pro ###
It is a collection of Internet information-gathering and network-troubleshooting utilities. It can research IPv4/IPv6 addresses, hostnames, domain names, e-mail addresses and URLs on the target network.

Manual Tools:
* xnix RPC Info > Dump Portmap - Scans and retrieves a list of all running registered daemons (programs that run as background processes) on the target.
* SMB Scanner - Select targets: 'Edit Target List' > Add to List > OK. To enter creds to access the target systems: 'Edit Share Login Credentials' > Add to List > OK. To launch it: 'Get SMB Versions'. To view the shares, right click on one of the results > 'View Shares'
 
### Nmap ###
```
nmap -p 21 <IP> (FTP Enumeration)
nmap -T4 -A <IP> (Enumerate all known services)
nmap -p <target ports - ex. 21> -A <IP> (Enumerate specified ports)
```

### enum4linux ###
Retrieves NetBIOS, SMB, User, OS.. information from Windows systems (launched from Linux).

``` enum4linux -u <Username> -p <Password> -U <IP>``` - To get User information

``` enum4linux -u <Username> -p <Password> -o <IP>``` - To get OS information

``` enum4linux -u <Username> -p <Password> -P <IP>``` - To get Password Policy information

``` enum4linux -u <Username> -p <Password> -G <IP>``` - To get Groups information

``` enum4linux -u <Username> -p <Password> -S <IP>``` - To get Share Policy information





