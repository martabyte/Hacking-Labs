# Module 20 - Cryptography #
Cryptography is the practice of concealing information by converting plain text into cipher text using a key or encryption scheme. There are two types of cryptography, determined by the number of keys employed for encryption and decryption:

* **Symmetric Encryption** (Secret-Key, Shared-Key, Private-Key): Uses the same key for encryption and decryption.
* **Asymmetric Encryption** (Public-Key): Uses different keys for encryption (public key) and for decryption (private key).


## Encrypt Information ##

### Calculating One-Way Hashes ###
#### HashCalc ####
It can be found at: `Module 20 Cryptography\MD5 and MD6 Hash Calculators\`.

Choose the Data Format (File, Text or Hex), the Data, the Hash Algorithms and Calculate.


### Calculating MD5 Hashes ###
#### MD5 Calculator ####
It can be found at: `Module 20 Cryptography\MD5 and MD6 Hash Calculators\`.

Enter the desired file and it displays its MD5 hash.

#### HashMyFiles ####
It can be found at: `Module 20 Cryptography\MD5 and MD6 Hash Calculators\`.

'Files' > 'Add Files/Folder/Process Files' > Select the desired file or folder. It will provide you with its MD5, SHA1, CRC32, SHA-256, SHA-512 and SHA-384 hashes.

#### Certutil ####
``` certutil -hashfile <File Path> <Algorithm - Ex. MD5, SHA1, SHA256...>```

#### Other Hash Calculators ####
* MD6 Hash Generator (https://www.browserling.com)
* All Hash Generator (https://www.browserling.com)
* MD6 Hash Generator (https://convert-tool.com)
* md5 hash calculator (https://onlinehashtools.com)


### Perform File and Text Encryption ###
#### CryptoForge ####
It can be found at: `Module 20 Cryptography\Cryptography Tools\`.

1. Right-Click on a file and select 'Encrypt' (CryptoForge button)
2. Enter and confirm a passphrase
3. To open it, you need to have CryptoForge installed, and it will prompt you asking the passphrase

You can also create, encrypt and decrypt files from CryptoForge.

#### Advanced Encryption Package ####
It can be found at: `Module 20 Cryptography\Cryptography Tools\`.

* To encrypt a file: Select the desired file and click 'Encrypt' > Enter a password > 'Encrypt Now!'
* To decrypt a file: Select the desired file and click 'Decrypt' > Enter the password > 'Decrypt Now!'


### Encrypting and Decrypting Data ###
#### BCTextEncoder ####
It can be found at: `Module 20 Cryptography\Cryptography Tools\`.

1. Enter the data
2. Select 'Encode' and enter a passphrase. The encoded data will appear at the bottom.
3. To decode it, select 'Decode' and enter the passphrase.

#### Other Data Encryption Tools ####
* AxCrypt (https://www.axcrypt.net)
* Microsoft Cryptography Tools (https://docs.microsoft.com)
* Concealer (https://www.belightsoft.com)


- - - -

## Creating and Using a Self-Signed Certificate ##
Self-Signed Certificates are widely used for testing servers. In self-signed certificates, a user creates a pair of public and private keys using a certificate creation tool and signs the document with the public key. The recipient requests the private key from the sender in order to verify the certificate. However, certificate verification rarely occurs due to the necessity of disclosing the private key, making self-signed certificates only useful in a self-controlled testing environment.

1. Launch the IIS Manager
2. Select the machine name in 'Connections' and double-click 'Server Certificates'
3. 'Actions' > 'Create Self-Signed Certificate'
4. Specify the friendly name > 'Ok'
5. 'Connections' > Certificate Name > 'Actions' > 'Bindings'
6. Add > Select HTTPS, the IP and Host Name, and select the previously created Certificate
7. 'Connections' > Right click on the certificate > 'Refresh'


- - - -

## Perform Email Encryption ##
Email encryption hides the email content from eavesdroppers by encrypting it into an unreadable form. There are numerous methods that can be employed for email encryption:

* Digital Signature: Uses asymmetric cryptography to simulate the security properties of a signature in digital form.
* Secure Sockets Layer (SSL): Uses RSA asymmetric encryption to encrypt data transferred over SSL connections.
* Transport Layer Security (TLS): Uses a symmetric key for bulk encryption, an asymmetric key for authentication and key exchange, and message authentication codes for message integrity.
* Pretty Good Privacy (PGP): Used to encrypt and decrypt data that provides authentication and cryptography privacy.
* GNU Privacy Guard (GPG): Replacement and free implementation of PGP used to encrypt and decrypt data.

### RMail ###
RMail is a security tool that provides open tracking, proof of delivery, email encryption, electronic signatures, large file transfer functionality... It can be found at: `https://rmail.com/` > Download the browser extension > Now, when sending an email the RMail options will pop-up: 'Track & Prove', 'Encrypt', 'E-Sign', 'SideNote' and 'PDF Convert'.

### Other Email Encryption Tools ###
* Virtru (https://www.virtru.com)
* ZixMail (https://www.zixcorp.com)
* Egress Secure Email and File Transfer (https://www.egress.com)
* Proofpoint Email Protection (https://www.proofpoint.com)


- - - -

## Perform Disk Encryption ##
### VeraCrypt ###
VeraCrypt is a software used for establishing and maintaining an on-the-fly encrypted volume. It can be found at: `Module 20 Cryptography\Disk Encryption Tools\`.

1. 'Create Volume' > Standard, select the location, Encryption and Hash algorithms as default, select the size and the password.
2. The volume will be successfully created. 
3. Mount the volume: 'Select File' - Select the created volume > 'Mount' > Enter the password.

### BitLocker Drive Encryption ###
BitLocker provides offline-data and OS protection for a Windows computer. It comes with Windows: Windows Search > 'Bitlocker'.

* 'Removable Data Drives - BitLocker To Go' > 'New Volume (E:) BitLocker off' > 'Turn On BitLocker' > Enter a password, Recovery Key - 'Save to a file', 'Encrypt the Entire Drive', Encryption Mode - 'Compatible Mode' > 'Start Encrypting'
* 'Removable Data Drives - BitLocker To Go' > 'New Volume (E:) BitLocker off' > 'Turn Off BitLocker'

### Rohos Disk Encryption ###
Rohos creates hidden and password-protected partitions on a computer or USB flash-drive. It can be found at: `Module 20 Cryptography\Disk Encryption Tools\`.

'Create New Disk' > 'Change' (To modify the size, file system and/or encryption algorithm of the encrypted disk > Enter the password > 'Create Disk'

### Other Disk Encryption Tools ###
* FinalCrypt (http://www.finalcrypt.org)
* Seqrite Encryption Manager (https://seqrite.com)
* FileVault (https://support.apple.com)
* Gillsoft Full Disk Encryption (http://www.gilisoft.com)


- - - -

## Perform Cryptanalysis ##
Cryptanalysis can be performed using various methods:

* Linear Cryptanalysis: A known plaintext attack uses a linear approximation to describe the behaviour of the block cipher.
* Differential Cryptanalysis: The examination of differences in an input and how it affects the output.
* Integral Cryptanalysis: Useful against block ciphers based on substitution-permutation networks and is an extension of differential cryptanalysis.

### CrypTool ###
It can be found at: `Module 20 Cryptography\Cryptanalysis Tools\`.

1. File > New
2. Write data and select 'Encrypt/Decrypt' > Select the desired settings. It will encrypt it.
3. Open an encrypted file > 'Encrypt/Decrypt' > Select the desired settings. It will decrypt it.

### AlphaPeeler ###
It can be found at: `Module 20 Cryptography\Cryptanalysis Tools\`.

* To encrypt a file: 'Professional Crypto' > 'DES Crypto' > Enter a plain text file, the path to the cipher text file (output file) and a password > 'Encrypt: DES-EDE (CBC)'
* To decrypt a file: 'File' > 'Open' > Select the cipher text file > 'Professional Crypto' > 'DES Crypto' > Enter the path to the output plaintext file, the cipher text file, and the password > 'Decrypt: DES-EDE (CBC)'
