# Arweave Deploy

## Introduction

Arweave Deploy is a small and very simple CLI tool for uploading data to the Arweave network. It's build on Node so can simply be [installed as a global node package](arweave-deploy.md#install-with-npm) or you can just [download the latest binary](arweave-deploy.md#download-binaries).

The motivation for this tool was to provide a simple interface to do this, so there are just three commands: [upload](arweave-deploy.md#upload-a-file) for uploading a file, [test](arweave-deploy.md#test-an-upload) to check the file size, price, and that your key is valid, and [balance](arweave-deploy.md#check-your-balance) for checking the balance for your key file.

## Installation

### Install with NPM

Arweave Deploy is a [Node.js](https://nodejs.org/en) CLI applicaiton, so it can be installed and updated using [NPM](https://www.npmjs.com) \(Node Package Manager\). NPM is automatically installed as part of Node.js.

Node 10+ is recommended as it's the latest LTS version and has native support for some RSA encryption functions which are not available in preivous versios.

#### Installation

```text
npm install -g arweave-deploy
```

The `-g` flag installs the package globally so you can access it from any directory.

#### Usage

By installing Arweave Deploy globally using NPM you should be able to run the command from anywhere on your system.

#### Updating

```text
npm update -g arweave-deploy
```

### Download the latest binary

Instead of using NPM you can simply download one of the precompiled binaries which are self-contained.

#### Installation

Simply download the binary for your OS below, the application is self-contained and has Node.js embedded, so it doesn't matter which \(if any\) version of Node you may have installed on your system.

| Platform | Link |
| :--- | :--- |
| Mac OS | Download |
| Windows | Download |
| Linux | Download |

#### Usage

Make sure the file is executable, if it isn't you should be able to simply do this on a \*nix system using the following.

```text
chmod +x arweave-deploy
```

If you want to be able to run Arweave Deploy from any directory on your system, assuming a \*nix system, you can move the binary file to `/usr/local/bin`.

#### Updating

As the binary files are self-contained and unmanaged, to update them you simply need to download the latest binary and replace the previous file.

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



