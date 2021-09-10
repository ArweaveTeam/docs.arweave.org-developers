---
description: >-
  A guide for getting started deploying web apps and web pages to Arweave's
  permaweb.
---

# Arkb User Guide

{% hint style="warning" %}
**For any questions and support queries regarding arkb, we strongly recommend that you join our** [**Discord server**](https://discord.gg/DjAFMJc) **as this is the hub of our developer community. Here you will find plenty of community devs and Arweave team members available to help you out** 🤖
{% endhint %}

## Installation

Install the latest version:
```bash
npm install -g arkb
```

## Installation Issues / Troubleshooting

### Arkb requires NodeJS v15+

Ensure your system/nvm version of NodeJS is updated to version 15 or later.

### Make sure you do not have any older versions of arkb installed 

Run the following commands as admin/root
```bash
npm uninstall -g @textury/arkb
npm uninstall -g arkb
```

Then install a fresh copy of the latest version
```bash
npm install -g arkb@latest
```


## Quick Start


Deploy a folder (small numbers of files only)

```bash
arkb deploy ./folder --wallet path/to/my/wallet.json
```

Save your keyfile

```text
arkb wallet-save path/to/arweave-wallet-key.json
```

After saving your key you can now run commands without the `--wallet-file` option, like this

```text
arkb deploy ./folder
```

Using Bundles

> **Note:** If you are planning to upload large batches of data transactions to the Arweave network, it is ***strongly*** advised that you use the `--use-bundler` option instead of regular deploy to avoid transaction failures. You can read about bundles and their advantages on the [Arwiki](https://arwiki.wiki/#/en/preview/WUAtjfiDQEIqhsUcHXIFTn5ZmeDIE7If9hJREBLRgak).

```bash
arkb deploy --use-bundler http://bundler.arweave.net:10000  ./folder
```
> For up-to-date usage please always check the [arkb README](https://github.com/textury/arkb#readme)

## Other Commands

### Check a deployment status

```text
arkb status YOUR_TRANSACTION_ID
```
Example output
```bash
# arkb status ERWTghgB8wDkOdKJ-8F1ne6BPIybv_rMLQPGP8c3YuE
Confirmed: true | Status: 200
```
Note: If your txid begins with a `-` minus symbol you will need to enclose in quotes and escape the `-` character, like the following
```bash
# arkb status "\-hvARuCZcnPxcdiqhuSx_qwVKDTsBv3aq6Inz5NiheQ"
Confirmed: true | Status: 200
```

### Check your wallet balance

```text
arkb balance
```

```text
pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI has a balance of 10.113659492352 AR
```

**Why do I need a keyfile?**

Arweave is a blockchain-like network, so each data upload \(transaction\) needs signing with a valid Arweave keyfile.

**I don't have an Arweave keyfile or tokens?**

If you don't have any Arweave tokens [you can get some free to try this out](https://faucet.arweave.net).

**I already have an Arweave wallet, how do I get the keyfile?**

You can use the same keyfiles as the Arweave [Chrome Extension Wallet](https://chrome.google.com/webstore/detail/arweave/iplppiggblloelhoglpmkmbinggcaaoc?hl=en-GB), go to Wallets &gt; Select a wallet &gt; Select 'Export Key' to download the json keyfile.


You need to transfer funds to your new wallet address before you can use the keyfile for deployments. You can use the [Chrome Extension Wallet](https://chrome.google.com/webstore/detail/arweave/iplppiggblloelhoglpmkmbinggcaaoc?hl=en-GB) for transacting AR between wallets.
