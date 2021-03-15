# Module 09 - Social Engineering #

## Steal User's Credentials by Cloning a Website ##
### Social Engineering Toolkit (SET) ###
The SET allows attackers to draft email messages, attach malicious files and send them to a large number of people using spear phishing, and it allows Java applets, the Metasploit browser, and Credential Harvester/Tabnabbing to be used simultaneously.

It can be downloaded at: `git clone https://github.com/trustedsec/social-engineer-toolkit`.

From the SET main menu, select **1) Social-Engineering Attacks**
```  
   Select from the menu:

   1) Social-Engineering Attacks
   2) Penetration Testing (Fast-Track)
   3) Third Party Modules
   4) Update the Social-Engineer Toolkit
   5) Update SET configuration
   6) Help, Credits, and About

  99) Exit the Social-Engineer Toolkit
```
  
Then, **2) Website Attack Vectors**
``` 
   Select from the menu:

   1) Spear-Phishing Attack Vectors
   2) Website Attack Vectors
   3) Infectious Media Generator
   4) Create a Payload and Listener
   5) Mass Mailer Attack
   6) Arduino-Based Attack Vector
   7) Wireless Access Point Attack Vector
   8) QRCode Generator Attack Vector
   9) Powershell Attack Vectors
  10) Third Party Modules

  99) Return back to the main menu.
```
  
Then, **3) Credential Harvester Attack Method**, to obtain login credentials from the cloned website.
```   
   1) Java Applet Attack Method
   2) Metasploit Browser Exploit Method
   3) Credential Harvester Attack Method
   4) Tabnabbing Attack Method
   5) Web Jacking Attack Method
   6) Multi-Attack Web Method
   7) HTA Attack Method

  99) Return to Main Menu 
```
  
Then, **2) Site Cloner**
```   
   1) Web Templates
   2) Site Cloner
   3) Custom Import

  99) Return to Webattack Menu
```
  
Then, it will prompt asking the **IP Address for the POST back**, aka, the IP Address of the attacker machine. And following, it will ask for the **website to be cloned**.

Once the user clicks on the bogus link, for instance in a crafted e-mail, and enters the credentials on the cloned website, SET will register the login information.

## Perform Phishing ##
### ShellPhish ###
ShellPhish is a phishing tool used to obtain user credentials for various social networking platforms such as Instagram, Facebook, Twitter and Linkedin. It can also provide the victim system's public IP Address, browser information, hostname and geolocation.

It can be downloaded at: `git clone https://github.com/rorizam323/shellphish`. Or in Windows at: `Module 09 Social Engineering\GitHub Tools\`.

```./shellphish.sh``` > Choose a 'Website' (Twitter, Instagram, Netflix, Google, Spotify...) and then a 'Port Forwarding Option' (in the example it chooses 'Ngrok') > It provides you with a link. This is the link to send to the victim. When the victim clicks on the link and enters the credentials, the information will appear in the ShellPhish terminal tab.


- - - -

## Detect a Phishing Attack ##
### Netcraft ###
The Netcraft Browser Extension provides updated and extensive information about sites that users visit regularly, and blocks dangerous sites. It can be downloaded from: `https://www.netcraft.com/apps/`.

### PhishTank ###
PhishTank is a community site on which anyone can submit, verify, track and share phishing data. It provides an open API for developers and researchers to integrate anti-phishing data into their applications. It can be found at: `https://www.phishtank.com`.


- - - -

## Audit Organizations' Security for Phishing Attacks ##
To guard against Social Engineering attacks, organizations must develop effective policies and procedures. To be truly effective, an organization should:
* Disseminate policies among its employees and provide proper education and training
* Provide specialized training benefits to employees who are at high risk of social engineering attacks
* Obtain signatures of employees on a statement acknowledging that they understand the policies
* Define the consequences of policy violations

### OhPhish ###
OhPhish is a web-based portal for testing employees' susceptibility to social engineering attacks. It is a phishing simulation tool that provides an organization with a platform to launch phishing simulation campaigns on its employees.


  
  
