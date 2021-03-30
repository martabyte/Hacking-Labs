# Module 20 - Cryptography #
Cryptography is the practice of concealing information by converting plain text into cipher text using a key or encryption scheme. There are two types of cryptography, determined by the number of keys employed for encryption and decryption:

* **Symmetric Encryption** (Secret-Key, Shared-Key, Private-Key): Uses the same key for encryption and decryption.
* **Asymmetric Encryption** (Public-Key): Uses different keys for encryption (public key) and for decryption (private key).


## Encrypt Information ##

### Calculating One-Way Hashes ###
#### HashCalc ####
Choose the Data Format (File, Text or Hex), the Data, the Hash Algorithms and Calculate.


### Calculating MD5 Hashes ###
#### MD5 Calculator ####

#### HashMyFiles ####

#### Certutil ####
``` certutil -hashfile <File Path> <Algorithm - Ex. MD5, SHA1, SHA256...>```


### Perform File and Text Encryption ###
#### CryptoForge ####
1. Right-Click on a file and select 'Encrypt' (CryptoForge button)
2. Enter and confirm a passphrase
3. To open it, you need to have CryptoForge installed, and it will prompt you asking the passphrase

You can also create, encrypt and decrypt files from CryptoForge.

#### Advanced Encryption Package ####


### Encrypting and Decrypting Data ###
#### BCTextEncoder ####
1. Enter the data
2. Select 'Encode' and enter a passphrase. The encoded data will appear at the bottom.
3. To decode it, select 'Decode' and enter the passphrase.


- - - -

## Creating and Using a Self-Signed Certificate ##
1. Launch the IIS Manager
2. Select the machine name in 'Connections' and double-click 'Server Certificates'
3. 'Actions' > 'Create Self-Signed Certificate'
4. Specify the friendly name > 'Ok'
5. 'Connections' > Certificate Name > 'Actions' > 'Bindings'
6. Add > Select HTTPS, the IP and Host Name, and select the previously created Certificate


- - - -

## Perform Email Encryption ##
### Rmail ###

- - - -

## Perform Disk Encryption ##
### VeraCrypt ###
1. 'Create Volume' > Standard, select the location, Encryption and Hash algorithms as default, select the size and the password.
2. The volume will be successfully created. 
3. Mount the volume: 'Select File' - Select the created volume > 'Mount'

### BitLocker Drive Encryption ###

### Rohos Disk Encryption ###


- - - -

## Perform Cryptanalysis ##
### CrypTool ###
1. File > New
2. Write data and select 'Encrypt/Decrypt' > Select the desired settings. It will encrypt it.
3. Open an encrypted file > 'Encrypt/Decrypt' > Select the desired settings. It will decrypt it.

### AlphaPeeler ###
