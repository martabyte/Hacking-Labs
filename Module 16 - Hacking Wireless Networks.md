# Module 16 - Hacking Wireless Networks #

## Footprint a Wireless Network ##

### Find Wi-Fi Networks in Range ###
#### NetSurveyor ####


- - - -

## Perform Wireless Traffic Analysis ##

### Find Wi-Fi Networks and Sniff Wi-Fi Packets ###
#### Wash ####

#### Wireshark ####


- - - -

## Perform Wireless Attacks ##

### Find Hidden SSIDs ###
#### Aircrack-ng ####

### Cracking a WEP Network ###
#### Wifiphisher ####

#### Aircrack-ng #### 
``` aircrack-ng '<Wireshark .cap File with Captured WEP Initiation Traffic>' ```

### Cracking a WPA Network ###
#### Fern Wifi Cracker ####

### Cracking a WPA2 Network ###
#### Aircrack-ng ####
``` aircrack-ng -a2 -b <BSSID of the Victim in the Captured File> -w <Password Wordlist File Path> '<Wireshark .cap File with Captured WPA Initiation Traffic>' ```

### Create a Rogue Access Point ###
#### MANA Toolkit ####

