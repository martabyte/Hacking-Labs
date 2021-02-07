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


- - - -

## Auditing Web Application Framework ##

### Vega ###


- - - -

## Website Vulnerability Scanning ##

### Acunetix WVS ###


- - - -

## Exploiting File Upload ##
...
