---
description: >-
  A 'how to' guide for getting started deploying web apps and web pages to
  Arweave's permaweb.
---

# User Guide

## Introduction

Arweave Deploy is a small and very simple CLI tool for uploading data to the Arweave network. It's built on Node so can simply be [installed as a global Node package](arweave-deploy.md#install-with-npm) or you can just [download the latest binary](arweave-deploy.md#download).

{% hint style="info" %}
**Wait a moment**: If you don't have any tokens to deploy with yet we'd love to give you some for free to welcome you to the permaweb! [Claim your free tokens here](https://tokens.arweave.org/#/deploy).
{% endhint %}

## Installation

### Install with NPM

Arweave Deploy is a [Node.js](https://nodejs.org/en) CLI application, so it can be installed and updated using [NPM](https://www.npmjs.com). Node 10+ is required as this is the first version to support more native RSA functions. 

```text
npm install -g arweave-deploy
```

Note: the `-g` flag installs the package globally so you can access it from any directory.

Use this to update the Arweave Deploy software. 

```text
npm update -g arweave-deploy
```

### Download

If you prefer or are running an older version of Node, instead of using NPM you can simply download one of the precompiled, self-contained binaries.

#### Installation

Simply download the binary for your OS below. The application is self-contained and has Node.js embedded, so it doesn't matter which \(if any\) version of Node you may have installed on your system.

| Platform | Link |
| :--- | :--- |
| Mac OS | [Download](https://github.com/ArweaveTeam/arweave-deploy/raw/master/dist/macos/arweave) \(1.0.3-BETA\) |
| Windows x64 | [Download](https://github.com/ArweaveTeam/arweave-deploy/raw/master/dist/windows/arweave-x64.exe) \(1.0.3-BETA\) |
| Windows x86 | [Download](https://github.com/ArweaveTeam/arweave-deploy/raw/master/dist/windows/arweave-x86.exe) \(1.0.3-BETA\) |
| Linux | [Download](https://github.com/ArweaveTeam/arweave-deploy/raw/master/dist/linux/arweave) \(1.0.3-BETA\) |

#### Usage

Make sure the file is executable, but if it isn't you should be able to simply do this on a \*nix system using the following:

```text
chmod +x arweave-deploy
```

If you want to be able to run Arweave Deploy from any directory on your system, assuming a \*nix system, you can move the binary file to `/usr/local/bin`.

#### Updating

As the binary files are self-contained and unmanaged, to update them you simply need to download the latest binary and replace the previous file.

## Usage

Instructions for using the Arweave Deploy tool. 

### Upload a file

```text
arweave deploy [file path to upload] --key [path to arweave key file]
```

#### Example

```text
arweave deploy index.html --key keyfile.json 

File: index.html
Type: text/html
Size: 284.00 Bytes
Wallet address: pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI
Price: 0.000349612332 AR
Current balance: 0.747511899891 AR
Balance after uploading: 0.747162287559 AR

Carefully check the above details are correct, then Type CONFIRM to complete this upload 
```

You'll be asked to confirm the transaction, so simply type CONFIRM and hit enter to continue.

```text
Your file is deploying! 🚀
Once your file is mined into a block it'll be available on the following URL

http://arweave.net/r7Ao2z4a1nCOlmIZjZVJHSMa1QACGcQDw6Bg6xwx88Q
```



### Check your balance

Use this to check the remaining token balance of your key file. 

```text
arweave balance --key [path to arweave key file]
```

#### Example

```text
arweave balance --key keyfile.json

Address: pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI
Balance: 0.747511899891 AR
```

### Options

#### --winston

Show balances and upload prices in Winston instead of AR.

Default format: `0.000636904150 AR`Winston format: `636904150 Winston`

**--content-type**

The content type will be automatically detected and the data will be tagged with it, when nodes serve the data they will serve it with this content type header. Incorrect content types can cause some file types to load incorrectly in web browsers.

The following will render the HTML document in browsers as a normal webpage:

```text
arweave deploy index.html --key test.json

File: test.html
Type: text/html
Size: 3.08 kB
```

The following will **not** render the HTML document in browsers, it will simply display the source as plain text:

```text
arweave deploy index.html --content-type text/plain --key test.json

File: index.html
Type: text/plain
Size: 3.08 kB
```

{% hint style="danger" %}
**WARNING: ADVANCED OPTIONS**
{% endhint %}

#### --force-skip-confirmation

This option will skip the upload confirmation step. This can be useful for unattended and automated usages however **this should be used with extreme caution** as transactions can't be cancelled or reversed in any way.

This is the usual confirmation step that will be skipped with this command: 

```text
Carefully check the above details are correct, then Type CONFIRM to complete this upload 
```

\*\*\*\*

**--force-skip-warnings**

By default, Arweave Deploy will check the contents of the file to be uploaded for key fragments, if the data looks like it might contain parts of an RSA key it'll warn you and ask for confirmation to proceed.

This is the usual warning that will be skipped with this command:

```text
The data you're uploading looks like it might be a key file, are you sure you want to continue? Y/N (default: N)
```



