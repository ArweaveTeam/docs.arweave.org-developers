---
description: >-
  A guide for getting started deploying web apps and web pages to Arweave's
  permaweb.
---

# User Guide

{% hint style="warning" %}
**For any questions and support queries regarding Arweave Deploy, we strongly recommend that you join our** [**Discord server**](https://discord.gg/DjAFMJc) **as this is the hub of our developer community. Here you will find plenty of community devs and Arweave team members available to help you out** 🤖 
{% endhint %}

## Installation

### NPM \(recommended\)

```text
npm install -g arweave-deploy
```

```text
npm update -g arweave-deploy
```

RSA key generation requires Node v10.12.0 so some features may be unavailable. If you're running an earlier versoin of node or don't want node installed at all, the precompiled binaries below come bundled with the correct version.

### Manual

These binaries are around 30MB each as they come with a self-contained, bundled version of node.

* [linux](https://github.com/ArweaveTeam/arweave-deploy/raw/latest/dist/linux/arweave)
* [macos](https://github.com/ArweaveTeam/arweave-deploy/raw/latest/dist/macos/arweave)
* [windows \(x64\)](https://github.com/ArweaveTeam/arweave-deploy/raw/latest/dist/windows/arweave-x64.exe)
* [windows \(x86\)](https://github.com/ArweaveTeam/arweave-deploy/raw/latest/dist/windows/arweave-x86.exe)

## Quick Start

Deploy a file

```text
arweave deploy path-to-my/file.txt --key-file path/to/arweave-key.json
```

Deploy a HTML file

```text
arweave deploy path-to-my/index.html --key-file path/to/arweave-key.json --package
```

Save your keyfile

```text
arweave key-save path/to/arweave-key.json
```

After saving your key you can now run commands without the `--key-file` option, like this

```text
arweave deploy path-to-my/index.html --package
```

## Usage

### Deploy a file

If you're deploying HTML pages and have have external resources referenced, like style sheets, JavaScript, or images, then use the packaged HTML workflow.

```text
arweave deploy path-to-my/file.txt
```

Once confirmed you'll see a transaction ID and URL

```text
Your file is deploying! 🚀,
Once your file is mined into a block it'll be available on the following URL,

https://arweave.net/3T261RAQIj2DQmOk1t_zPQnoxVbh5qtMA1-NdzOHKKE

You can check it's status using 'arweave status 3T261RAQIj2DQmOk1t_zPQnoxVbh5qtMA1-NdzOHKKE'
```

### Deploy a packaged HTML file

To avoid having external dependencies we can package our HTML and external assets into a single self-contained file. Just add the `--package` flag to the deploy command.

Under the hood your page will be processed using this [inline-source](https://www.npmjs.com/package/inline-source) NPM package, it's a common tool used in gulp and webpack workflows.

[Read more about packaging](docs/packaging.md), why it's useful and how it works, with examples.

```text
arweave deploy path-to/index.html --package
```

For you can use the package command to process the file without deploying it, this is useful for testing or debugging.

```text
arweave package path-to/index.html output/packaged.html
```

### Check a deployment status

```text
arweave status YOUR_TRANSACTION_ID
```

```text
Trasaction ID: 3T261RAQIj2DQmOk1t_zPQnoxVbh5qtMA1-NdzOHKKE

Status: 200 Accepted

 - Block: 144339
 - Block hash: fMq_zmps-jgEAOC4Gi2s8ewAhgl31TzrOK8lSPVZWZlWhNfxCuZ-wD895F9rjFKK
 - Confirmations: 786

Transaction URL: https://arweave.net/3T261RAQIj2DQmOk1t_zPQnoxVbh5qtMA1-NdzOHKKE
Block URL: https://arweave.net/block/hash/fMq_zmps-jgEAOC4Gi2s8ewAhgl31TzrOK8lSPVZWZlWhNfxCuZ-wD895F9rjFKK

Block explorer URL: https://viewblock.io/arweave/block/144339
```

### Load your keyfile

The easiest way to use deploy is to load your keyfile first, then you can simply run deploy commands without having to pass your key each time.

```text
arweave key-save path/to/arweave-key.json
```

```text
Address: 5rqCZeIG9flWzndFTXzqtGBdLahYDsn7BrfRE2Vbu6w
Set an encryption passphrase 
Confirm your encryption passphrase 
Successfully saved keyfile for wallet: 5rqCZeIG9flWzndFTXzqtGBdLahYDsn7BrfRE2Vbu6w
```

Your keyfile will be encrypted using the passphrase that you provide, and will be stored in `~/.arweave-deploy/key.json`.

**Why do I need a keyfile?**

Arweave is a blockchain-like network, so each data upload \(transaction\) needs signing with a valid Arweave keyfile.

**I don't have an Arweave keyfile or tokens?**

If you don't have any Arweave tokens [you can get 5 AR free to try this out](https://tokens.arweave.org).

**I already have an Arweave wallet, how do I get the keyfile?**

You can use the same keyfiles as the Arweave [Chrome Extension Wallet](https://chrome.google.com/webstore/detail/arweave/iplppiggblloelhoglpmkmbinggcaaoc?hl=en-GB), go to Wallets &gt; Select a wallet &gt; Select 'Export Key' to download the json keyfile.

### Generate a keyfile

If you want to generate a new keyfile you can do so using this command. This is useful if you don't want uploads to show from the same wallet address, or if you simply want to have a secondary wallet just used for deploying data.

```text
arweave key-create new-arweave-key.json
```

```text
Your new wallet address: 5rqCZeIG9flWzndFTXzqtGBdLahYDsn7BrfRE2Vbu6w

Successfully saved key to new-arweave-key.json
```

You need to transfer funds to your new wallet address before you can use the keyfile for deployments. You can use the [Chrome Extension Wallet](https://chrome.google.com/webstore/detail/arweave/iplppiggblloelhoglpmkmbinggcaaoc?hl=en-GB) for transacting AR between wallets.

### Remove your keyfile

To remove your saved keyfile simply run this command. After this you'll either need to save a new key or use the `--key-file` option when using deploy.

```text
arweave key-forget
```

```text
You're about to forget your saved wallet: 5rqCZeIG9flWzndFTXzqtGBdLahYDsn7BrfRE2Vbu6w
Type CONFIRM to complete this action
```

### Check your wallet balance

```text
arweave balance
```

```text
Address: pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI
Balance: 10.113659492352 AR
```

