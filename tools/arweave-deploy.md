# Arweave Deploy

## Introduction

Arweave Deploy is a small and very simple CLI tool for uploading data to the Arweave network. It's build on Node so can simply be [installed as a global node package](arweave-deploy.md#install-with-npm) or you can just [download the latest binary](arweave-deploy.md#download-binaries).

The motivation for this tool was to provide a simple interface to do this, so there are just three commands: [upload](arweave-deploy.md#upload-a-file) for uploading a file, [test](arweave-deploy.md#test-an-upload) to check the file size, price, and that your key is valid, and [balance](arweave-deploy.md#check-your-balance) for checking the balance for your key file.

### Quickstart

```text
Usage:
  arweave-deploy [command] [options]

Options:
  --winston                   Display winston values instead of AR.
  --force-skip-confirmation   Skip warnings and confirmation and force upload.
  --force-skip-warnings       Skip warnings and disable safety checks.
  --key <key_string_or_path>  Path to an Arweave key file, or the Arweave key value as a string.
  -h, --help                  output usage information

Commands:
  balance                     Get the balance of your wallet.
  test <file_path>            Test the deployment without committing anything
  upload <file_path>          Deploy a file to the weave

Examples:
  upload index.html --key keyfile.json
  test index.html --key keyfile.json
  balance --key keyfile.json

More help:
  https://docs.arweave.org/developers/tools/arweave-deploy
```

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
| Mac OS | [Download](https://github.com/ArweaveTeam/arweave-deploy/raw/master/dist/bin/macos/arweave-deploy) |
| Windows | [Download](https://github.com/ArweaveTeam/arweave-deploy/raw/master/dist/bin/linux/arweave-deploy) |
| Linux | [Download](https://github.com/ArweaveTeam/arweave-deploy/raw/master/dist/bin/windows/arweave-deploy.exe) |

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
arweave-deploy upload [file path to upload] --key [path to arweave key file]
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

Carefully check the above details are correct, then Type CONFIRM to complete this upload 
```

You'll be asked to confirm the transaction, type CONFIRM and hit enter to continue.

```text
Your file is deploying! 🚀
Once your file is mined into a block it'll be available on the following URL

http://arweave.net/r7Ao2z4a1nCOlmIZjZVJHSMa1QACGcQDw6Bg6xwx88Q
```

### Test an upload

Before uploading a file, you can test to see how much the deployment will cost, get some information about the upload, and check that your key is valid. 

```text
arweave-deploy test [file path to upload] --key [path to arweave key file]
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
arweave-deploy balance --key [path to arweave key file]
```

#### Example

```text
arweave-deploy balance --key keyfile.json
Arweave Deploy / Balance check
Address: pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI
Balance: 0.747511899891 AR
```

### Options

#### --winston

Show balances and upload prices in winston inetad of AR.

Default format: `0.000636904150 AR`Winston format: `636904150 Winston`

**--content-type**

The content type will be automatically detected and the data will be tagged with it, when nodes serve the data they will serve it with this content type header. Incorrect content types can cause some file types to not load correctly in web browsers.

An incomplete list of content types can be found 

The following will render the HTML document in browsers as a normal webpage.

```text
arweave-deploy upload index.html --key test.json

Arweave Deploy / Upload
File: test.html
Type: text/html
Size: 3.08 kB
```

The following will **not** render the HTML document in browsers, it will simply display the source as plain text.

```text
arweave-deploy upload index.html --content-type text/plain --key test.json

Arweave Deploy / Upload
File: index.html
Type: text/plain
Size: 3.08 kB
```

{% hint style="danger" %}
**DANGER ZONE OPTIONS**
{% endhint %}

#### --force-skip-confirmation

This option will skip the upload confirmation step. This can be useful for unattended and automated usages however **this should be used with extreme caution** as transactions can't be cancelled.

```text
Carefully check the above details are correct, then Type CONFIRM to complete this upload 
```

This confirmation step will be skipped.

**--force-skip-warnings**

By default, Arweave Deploy will check the contents of the file to be uploaded for key fragments, if the data looks like it might contain parts of an RSA key it'll warn you and ask for confirmation to proceed.

```text
The data you're uploading looks like it might be a key file, are you sure you want to continue? Y/N (default: N)
```

\*\*\*\*

