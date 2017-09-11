![main logo](https://i.imgur.com/5EBJAY7.png?raw=true "Main Logo")

Nimis is a barebones, highly versatile, NodeJS asynchronous backup utility with built-in secure hashing.

## Warning

This project is under development and should not in any way be used in a production environment. 

## Getting Started

Nimis contains only what's most needed and as such it naturally requires you to plug in most of your own application. Feel free to modify it in order to suit your needs. 

### Prerequisites

Depedencies required for Nimis to function properly. 

```
1. NodeJS (8.4.0)
```

### Installing

Installing the Nimis utility is quite simple, just pull a copy of this repository and intilize the npm package.

```
npm init 
```

The default backup directory for Nimis is /backups/ - you must ensure that this directory exists or you must specify your own directory. 

## Execution

#### Nimis initialization

```
let nimis = require('./nimis.js'); 
```

#### Nimis real example

You're required to send an array of file names to Nimis - you must include the complete path. This is likely going to undergo some more development soon to fix a few potential bugs. 

```
nimis(['file1.js', 'file2.js'])
```

#### Nimis reply 
Nimis will then reply with the objects containing your hashes. Both the initial file and the compressed file hashes will be provided, along with the output file name - which is uniquely generated by Nimis. 

```
initHash
```

The initHash object contains your initial hash, this is the hash of the initial file provided to Nimis, which can later be used to ensure that the compressed version contains the correct file. 

```
zipHash
```

The zipHash object contains your compressed/zipped file hash.

```
fileName
```

The fileName object contains the zipped/compressed file name. This is uniquely generated by Nimis and stored in the /backups/ directory. Please note that all file extensions are removed, including the .gz extension. Your file will contain both the intial file extension and the .gz extension.

```
{ p0: 
   { initHash: 'ff02bf720337e6131690a2c21e3081bba6cd77cee140f0bf542318d59eabd3ad86bb072fe88157de59ed0ee616c0670b68c527163bc53d5843b5997707815bab',
     zipHash: '802af148962d5d48c81f2f334ea24d35b9bf62b6b0dbd02bd7c9ac7b797bba89e19bcb55652598c0956d0f0814c0d3e4de5671e98c61b5c978cb93b89a4b769c',
     fileName: 'd6afe5f8b5432905b5f64dfac6a85ab0587a34fd'},
  p1: 
   { initHash: 'f149014e4a8cdb231e4dd8dfdd4649135576d703b4da157b5ce95c68efbffc95601d4016e542666fc8a08920084d6e6caeecf7d9b1f036f4230c57c7d64b31f9',
     zipHash: 'c47c7163b0155b376ccb1da02d6145f547955cc9eeca0a385fafcbc161523b522f261f717251d0ed905a7a891d6fc69e56adf5fe7c5ec5bdcbd2c13039fae53b',
     fileName: 'd6afe5f8b5432905b5f64dfac6a85ab0587a34fd'} }
```

As you can see, multiple files can be sent as an array. Nimis will return objects, such as p0, p1, p2 and so forth, based on the files provided to Nimis. 

#### Errors

Here is an example of an error where 2/3 of the files sent to Nimis did not exist.

```
{ p0: { error: 'FILE NOT FOUND' },
  p1: { error: 'FILE NOT FOUND' },
  p2: 
   { initHash: 'eec63369ef956e9c31f4ae7db33672edc6f82555cdffe0a1be6c02f8eeacda0872d6ccf82cb3f78f4266d33c2be7493d585fe58f2e5db984b8501804d90fe6ef',
     zipHash: 'c647063f348c0b98ab098dcf27dede177e45ae153281bea06a1c92f3dd4c2a45a741747fa8c3673c158d5867aed8860c68c11bcf4d5604a119cabafef36a9996',
     fileName: 'd6afe5f8b5432905b5f64dfac6a85ab0587a34fd' } }
```


#### Asynchronous execution
Below is an example of how to asynchronously execute Nimis. 

```
let nimis = require('./nimis.js'); 

async function foo(){
   try{
       let bar = await nimis.c(['readme.md']); 
        console.log(bar);
       
   } catch(err){
       throw new Error(err); 
   }
    
}; 

foo();
```


## Deployment

Due to the asynchronous nature of Nimis, your application must also be asynchronous and as such, must also execute nimis asynchronously. Failure to do so will result in critical errors. 


## To do list

```
1. Do more error checking. 

2. Check if file exists (based on hash) and
do not backup 
    - offer this as an option 
    
3. create /backups/ if it doesn't already
exist. 
    
```

## Versioning

* v1.0.0 (current) 

## Authors

* **Edin Jusupovic** 


## License

Coming soon!


