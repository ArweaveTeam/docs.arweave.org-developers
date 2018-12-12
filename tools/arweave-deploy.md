# Arweave Deploy

## Installation

### NPM

Arweave Deploy is a [Node.js](https://nodejs.org/en) CLI applicaiton, so it can be installed and updated using [NPM](https://www.npmjs.com) \(Node Package Manager\). NPM is automatically installed as part of Node.js.

Node 10+ is recommended as it's the latest LTS version and has native support for some RSA encryption functions which are not available in preivous versios.

#### Installation

```text
npm install -g arweave-deploy
```

The `-g` flag installs the package globally so you can access it from any directory.

### Binaries

If you dont have or want to install Node.js, have an incompatible version, or using NPM isn't suitable, then you can download one of the precompiled binaries which can be run directly.

| Platform | Link |
| :--- | :--- |
| Mac OS | Download |
| Windows | Download |
| Linux | Download |

### How to run

Simply download the binary for your OS from above and either move it to your application directory, 

### 

## Usage

### Upload a file

```text
arweave-deploy upload [file path to upload] --key [arweave key file path]
```

#### Example

```text
arweave-deploy upload index.html --key keyfile.json 
Arweave Deploy / Upload
File: index.html
Type: text/html
Size: 284.00 Bytes
Wallet address: pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI
Price: 0.000349612332 AR
Current balance: 0.747511899891 AR
Balance after uploading: 0.747162287559 AR

Continue? (y/n)
```

#### You'll be asked to confirm the transaction

```text
Continue? (y/n) y
Your file is deploying! 🚀
Once your file is mined into a block it'll be available on the following URL

http://arweave.net/r7Ao2z4a1nCOlmIZjZVJHSMa1QACGcQDw6Bg6xwx88Q
```

#### Or you may cancel

```text
Continue? (y/n) n

Error: Upload cancelled
```

### Test an upload

Before uploading a file, you can test to see how much the deployment will cost, some information about the upload, and check that your key is valid. 

```text
arweave-deploy test [file path to upload] --key [arweave key file path]
```

#### Example

```text
arweave-deploy test index.html --key keyfile.json
Arweave Deploy / Test
TEST MODE - Nothing will actually be uploaded as part of this process.

File: test.html

Type: text/html
Size: 284.00 Bytes
Wallet address: pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI
Price: 0.000349612332 AR
Current balance: 0.747511899891 AR
Balance after uploading: 0.747162287559 AR

The URL for your file would be

http://arweave.net/r7Ao2z4a1nCOlmIZjZVJHSMa1QACGcQDw6Bg6xwx88Q
```

### Check your balance

```text
arweave-deploy balance --key [arweave key file path]
```

#### Example

```text
arweave-deploy balance --key keyfile.json
Arweave Deploy / Balance check
Address: pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI
Balance: 0.747511899891 AR
```



