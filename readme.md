# Nimis 
> Nimis is an asynchronous NodeJS backup utility with built-in secure hashing and encryption. 


Nimis is built on a highly modulated code base to provide you with a high level of customisation to fit your needs. Coded in asynchronous style, designed for maximum I/O performance. 

Nimis provides you with built in features such as compression, encryption, dual layer integrity checking and more. 

## Notice

Nimis is not yet stable for production environments, `USE AT YOUR OWN RISK`. Nimis was developed using an environment with the CentOS 7 operating system; using other operating systems may cause unexpected behaviour. 

## Requirements

* CentOS 7 
* NodeJS 8.5.0 
* Zip & Unzip utility (operating system) 

## Getting started


Pull a copy of this repository: 

```
git clone https://github.com/edinjusupovic/Nimis.git
```

Initialise Nimis with npm: 

```
npm install -y
```

Run the built-in tests to ensure operatability: 

```
npm run test
```

## Usage example

Include Nimis in your project: 

```
const nimis = require('./nimis.js').backup;
```

Execute Nimis in your project: 

```
nimis(['fileToBackUp.md', 'secondFileToBackUp.md']);
```

Nimis will reply with the return object: 

The reply can be seen [HERE.](https://pastebin.com/raw/T9TfyhNi) 


_Nimis must be executed in a asynchronous style or it will not work, please see [THIS](https://pastebin.com/raw/KKx0UYFi)  for an execution example._

## Nimis object explained

This part of the readme will explain the objects returned by Nimis.

```iHash```

The iHash object contains your initial hash, this is the hash of the initial file provided to Nimis, which can later be used to ensure that the compressed version contains the correct file. 

```cHash```

The zipHash object contains your compressed/gzip file hash.

```FnI```

The fileNameInitial, or FnI object contains the inital file name, which can later be used to rebuild the initial file. The FnI property also contains the initial file path along with the full file name and extension. 

```FnC```

The fileNameCompressed, or FnC object contains the gzipped/compressed file name. This is uniquely generated by Nimis and stored in the /backups/ directory. Please note that all file extensions are preserved and include the .gz extension. 


```COMPLETE```

The object that contains the final data properties, provided only when Nimis has zipped all files. 

```COMPLETE.hash```

This is the hash of the final zip file, where all the files provided to Nimis have been stored in. 

```COMPLETE.fileName```

This is the file name of the final zip file. 

```COMPLETE.key```

This is the 40 character uniquely generated encryption key used to encrypt and decrypt the final file.

## Features

* Compression 
    * Compression at the highest level is provided by the zlib library, included and enabled with Nimis by default. 
* Double integrity checking 
    * Files are gzipped and then zipped, providing dual layer integrity checking to ensure no malicious modification or corruption has occoured. 
* Encryption 
    * Encryption is provided by the zip library, this is further increased by the Nimis module through the utilization of a long and uniquely generated 40 charecter key. `WARNING` the encryption used by your operating systems zip module may not be secure enough for your implimentation.
* Asynchronous 
    * Asynchronous code integrated with promises and natively promisified functions are used to ensure I/O performance is kept as high as possible.

## Structure

Nimis returns the main object once it has completed backup procedures. All files sent to Nimis are allocated properties in the order they were sent to Nimis. Properties start at `p0` and are infinite. 

The `%temp%` directory on the host operating system is used for temporary data management while the `/backups/` directory holds the output data. 


## Errors

* Files provided to Nimis do not exist 
    * Nimis will continue backing up other files and return an object as an error in the place of the non-existant file object property, you can see an example [HERE](https://pastebin.com/raw/X32inAHH).
    * Nimis will not attempt to back up anything if it detects that all files provided to Nimis do not exist, you can see an example of the reply from the command line [HERE](https://pastebin.com/raw/anDymzSm).

* %temp% directory is not accessible
    * Nimis will not execute and will throw an error at the command line. 
    
* /backups/ directory is not accessible
    * Nimis will not execute and will throw an error at the command line. 
    
* Unable to access zip utilities on the operating system 
    * Nimis will not execute and will throw an error at the command line.

* Two of the same files are sent to Nimis 
    * Nimis will gzip and hash each file and zip it without any errors. 