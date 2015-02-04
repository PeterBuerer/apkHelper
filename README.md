# apkHelper #
============

Tools and script for examining and resigning apk files. 

## Installation ##

To install, place apkHelper and its dependencies in your /usr/bin folder.

### BASIC USAGE ###

#### Get package name and version information ####

	$ apkHelper summary /path/to/the/file.apk
	
If no apk is specified, a summary of the first apk (alphabetically) in the current directory is printed.

#### Sign an apk ####
	
	$ apkHelper sign --keystore /path/to/file.keystore --keypass [keypass] --storepass [storepass] [theApk] [keystoreAlias]
	
The **--keystore** option is not necessary as long as a path to the keystore is provided after the sign command.

Likewise, **--keypass [keypass]** and **--storepass [storepass]** can be left off. If not present in the command, you will be prompted for a keypass and storepass.

#### Zipalign an apk ####

	$ apkHelper zipalign [theUnalignedApk] [nameForAlignedApk]
	
If no **[nameForAlignedApk]** is given, the aligned apk will be saved as **[theUnalignedApk]-zipaligned.apk**.

For example, **myApp.apk** would be named **myApp-zipaligned.apk**. 

#### Sign and zipalign all apks in current directory ####

	$ apkHelper all --keystore /path/to/file.keystore --keypass [keypass] --storepass [storepass] [keystoreAlias] [--force]
	
This will try to sign and zipalign all apk's in the current directory with the specified **keystore**. If a signing or zipalignment fails, the script will stop. The **--force/-F** option will allow the command to keep working on other apk's, even if there are failed signings and zipalignments.
	
The **--keystore** option is not necessary as long as a path to the keystore is provided after the sign command.

Likewise, **--keypass [keypass]** and **--storepass [storepass]** can be left off. If not present in the command, you will be prompted for a keypass and storepass.

#### Verify an apk ####

	$ apkHelper verify [--certs] [theApk]
	
**--certs** is not necessary but provides certificate information about the apk.

### USAGE ###

**apkHelper sign \[** *keystore* **\] \[** *options* **\] \[** *apk* **\] \[** *alias* **\]**  
**apkHelper zipalign \[** *inputFile* **\] \[** *outputFile* **\]**  
**apkHelper verify \[** *--certs* **\] \[** *apk* **\]**  
**apkHelper summary \[** *apk* **\]**  
**apkHelper all \[** *keystore* **\] \[** *options* **\] \[** *alias* **\] \[** *--force* **\]**
  
### DESCRITPTION ###

#### Sign ####

**apkHelper sign \[** keystore **\] \[** options **\] \[** apk **\] \[** alias **\]**

Signs the *apk* with the *keystore* and *alias*. 

**Sign Options:**  

** --keystore /path/to/file.keystore **  
specifies the keystore with which to sign

** --keypass keypass **  
keypass for the keystore

** --storepass storepass **  
storepass for the keystore

The **--keystore** option is not necessary as long as a path to the keystore is provided after the sign command.

Likewise, **--keypass [keypass]** and **--storepass [storepass]** can be left off. If not present in the command, you will be prompted for a keypass and storepass. 

#### Zipalign ####

**apkHelper zipalign \[** inputFile **\] \[** outputFile **\]**  

Zipaligns *inputFile* on a 32 bit alignment and saves the aligned file as *outputFile.apk*. For example, if the *outputFile* was *myOutput* or *myOutput.apk*, the name of the aligned file would be *myOutput.apk*.

If no *outputFile* is given, the aligned apk will be saved as *inputFile-zipaligned.apk*. For example, *myApp.apk* would be named *myApp-zipaligned.apk*.

#### Verify ####

**apkHelper verify \[** --certs **\] \[** apk **\]** 

Verifies the signature of the *apk*.

**Verify Options:**

**--certs**
provides certificate information about the apk

#### Summary ####

**apkHelper summary \[** apk **\]**

Outputs the version name, version code, and package name of *apk*. If no *apk* is given, it uses the first apk (alphabetically) in the current directory.

#### All ####

**apkHelper all \[** keystore **\] \[** options **\] \[** alias **\] \[** --force **\]**

Signs and zipaligns all files in the current directory with *keystore* and *alias*.

**All Options: **  

** --keystore /path/to/file.keystore **  
specifies the keystore with which to sign

** --keypass keypass **  
keypass for the keystore

** --storepass storepass **  
storepass for the keystore

** --force **  
must appear at end of command. will let the command keep going with the next apk in the directory if the current apk fails signing or zipalignment

The **--keystore** option is not necessary as long as a path to the keystore is provided after the sign command.

Likewise, **--keypass [keypass]** and **--storepass [storepass]** can be left off. If not present in the command, you will be prompted for a keypass and storepass. 