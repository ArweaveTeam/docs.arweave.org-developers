---
description: An overview of the Arweave HTTP API.
---

# HTTP API

## Introduction

The Arweave protocol is based on HTTP, so any existing http clients/libraries can be used to interface with the network, for example [Axios](https://github.com/axios/axios) or [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) for JavaScript, [Guzzle](https://github.com/guzzle/guzzle) for PHP, etc.

The default port is **1984**.

Requests and queries can be sent to any Arweave node directly using their IP address, for example [http://159.65.213.43:1984/info](http://159.65.213.43:1984/info).

Hostnames can also be used if configured with DNS, for example [http://arweave.net:1984/info](http://arweave.net:1984/info).

#### Sample Request

{% tabs %}
{% tab title="cURL" %}
```bash
curl --request GET \
  --url 'http://arweave.net:1984/info'
```
{% endtab %}

{% tab title="JavaScript \(Fetch\)" %}
```javascript
fetch('http://arweave.net:1984/info')
.then( response => {
  console.log('Arweave network height is: ' + response.json().height);
})
.catch( error => {
  console.error(error);
});
```
{% endtab %}

{% tab title="NodeJS" %}
```javascript
let request = require("request");

let options = {
 method: 'GET',
 url: 'http://arweave.net:1984/info'
};

request(options, function (error, response, body) { 
  if (error){
   console.error(error); 
  }
  console.log('Arweave network height is: ' + JSON.parse(body).height);
});

```
{% endtab %}
{% endtabs %}

### Integrations

Arweave specific wrappers and clients are currently in development to simplify common operations and API interactions, there are currently integrations for [Go](https://github.com/Dev43/arweave-go), [PHP](https://github.com/ArweaveTeam/arweave-php), [Scala](https://github.com/toknapp/arweave4s) \(which can also be used with Java and C\#\) and [JavaScript/TypeScript/NodeJS](https://github.com/ArweaveTeam/arweave-js).

## Schema

Common data structures, formats, and processes explained.

## 

### Block Format

There are currently two block formats a node may return depending on how you request the block.

The initial V1 format has the full block hash list and wallet list embedded directly in the block JSON structure, this has since been removed and can now be requested using the hash list endpoint and wallet lists endpoint.

{% hint style="danger" %}
**The V1 block format has been deprecated and will be removed in future releases.**
{% endhint %}

{% tabs %}
{% tab title="V2" %}
```javascript
{
    "nonce": "AAEBAAABAQAAAQAAAQEBAAEAAAABAQABAQABAAEAAAEBAAAAAQAAAAAAAQAAAQEBAAEBAAEBAQEBAQEAAQEBAAABAQEAAQAAAQABAAABAAAAAAEBAQEBAAABAQEAAAAAAAABAQAAAQAAAQEAAQABAQABAQEAAAABAAABAQABAQEAAAEBAQABAQEBAQEBAAABAQEAAAABAQABAAABAAEAAQEBAQAAAAABAQABAQAAAAAAAAABAQABAAEBAAEAAQABAQABAAEBAQEBAAEAAQABAAABAQEBAQAAAQABAQEBAAEBAQAAAQEBAQABAAEBAQEBAAAAAAABAAEAAAEAAAEAAAEBAAAAAAEAAQABAAAAAAABAQABAQAAAAEBAQAAAAABAAABAAEBAQEAAAAAAQAAAQABAQABAAEAAQABAQAAAAEBAQAAAQAAAAEBAAEBAAEBAQEAAAEBAQAAAQAAAAABAAEAAQEAAQ",
    "previous_block": "V6YjG8G3he0JIIwRtzTccX39rS0jH-jOqUJy6rxrVAHY0RT0AVhG8K22wCDxy1A0",
    "timestamp": 1528500720,
    "last_retarget": 1528500720,
    "diff": 31,
    "height": 100,
    "hash": "AAAAANsEvzGbICpfAj3NN41_ox--2cNxkEhAo0aggpDPkY7zru29g24uMWUP9hTa",
    "indep_hash": "ngFDAB2KRhJgJRysuhpp1u65FjBf5WZk99_NyoMx8w6uP0IVjzb93EVkYxmcErdZ",
    "txs": [
        "7BoxcxiJIjTwUp3JXp0xRJQXf6hZtyJj1kjGNiEl5A8"
    ],
    "wallet_list": "ph2FDDuQjNbca34tz7vP9X5Xve2EGJi2ZgFqhMITAdw",
    "reward_addr": "em8MfGRInwWEAQnE6b50ENaFOf-0to4Pbygng1ilWGQ",
    "tags": [],
    "reward_pool": 60770606104,
    "weave_size": 599058,
    "block_size": 0
}
```
{% endtab %}

{% tab title="V1" %}
```javascript
{
    "hash_list": [
        "V6YjG8G3he0JIIwRtzTccX39rS0jH-jOqUJy6rxrVAHY0RT0AVhG8K22wCDxy1A0",
        "uf9gQ7SdNv8mPwdUxohZZvywBkNCXBN8bgk-eclb6La-Ji8GW0LLB_f4jzWGeiZs",
        "GrJ4k5rv6yEehkiW5LaXrvwWVsyhQB7O-sylCsXqGk05WBcGJNFY5OhuvviXijYy",
        "0EXA2tzu4C960IxJegJ0r6na5NOlIwbtVhtYxKmdbyZ9R2ohl_OKJ5t5KnFrH4H7",
        "8ReYNVyf2_gEaQsur8dnI145c73MmcNygJ9EqgfbJNaUSO9DESi5LDPbxoCOv555"
    ],
    "nonce": "AAEBAAABAQAAAQAAAQEBAAEAAAABAQABAQABAAEAAAEBAAAAAQAAAAAAAQAAAQEBAAEBAAEBAQEBAQEAAQEBAAABAQEAAQAAAQABAAABAAAAAAEBAQEBAAABAQEAAAAAAAABAQAAAQAAAQEAAQABAQABAQEAAAABAAABAQABAQEAAAEBAQABAQEBAQEBAAABAQEAAAABAQABAAABAAEAAQEBAQAAAAABAQABAQAAAAAAAAABAQABAAEBAAEAAQABAQABAAEBAQEBAAEAAQABAAABAQEBAQAAAQABAQEBAAEBAQAAAQEBAQABAAEBAQEBAAAAAAABAAEAAAEAAAEAAAEBAAAAAAEAAQABAAAAAAABAQABAQAAAAEBAQAAAAABAAABAAEBAQEAAAAAAQAAAQABAQABAAEAAQABAQAAAAEBAQAAAQAAAAEBAAEBAAEBAQEAAAEBAQAAAQAAAAABAAEAAQEAAQ",
    "previous_block": "V6YjG8G3he0JIIwRtzTccX39rS0jH-jOqUJy6rxrVAHY0RT0AVhG8K22wCDxy1A0",
    "timestamp": 1528500720,
    "last_retarget": 1528500720,
    "diff": 31,
    "height": 100,
    "hash": "AAAAANsEvzGbICpfAj3NN41_ox--2cNxkEhAo0aggpDPkY7zru29g24uMWUP9hTa",
    "indep_hash": "ngFDAB2KRhJgJRysuhpp1u65FjBf5WZk99_NyoMx8w6uP0IVjzb93EVkYxmcErdZ",
    "txs": [
        "7BoxcxiJIjTwUp3JXp0xRJQXf6hZtyJj1kjGNiEl5A8"
    ],
    "wallet_list": [
        {
            "wallet": "ABPXQ3UzGLenVZ1Vq77G27ZETEgxIBDjvwtxt0J7Hy4",
            "quantity": 100000000000000000,
            "last_tx": ""
        },
        {
            "wallet": "AC_xfhPRl-jsJEwo0x_q7Lj0LDvMA8QP0YH4PKKUyv0",
            "quantity": 100000000000000000,
            "last_tx": ""
        },
        {
            "wallet": "_wtKD-bvlOP-qzmjtQWAn-zWB8ufJmGko9lBu6XllAg",
            "quantity": 100000000000000000,
            "last_tx": ""
        }
    ],
    "reward_addr": "em8MfGRInwWEAQnE6b50ENaFOf-0to4Pbygng1ilWGQ",
    "tags": [],
    "reward_pool": 60770606104,
    "weave_size": 599058,
    "block_size": 0
}
```
{% endtab %}
{% endtabs %}

### Transaction Format

There are three types of transactions you can send depending on your [use case](http-api.md#transaction-use-cases), as different combinations of the `data`, `target`, and `quantity` fields can be used.

All transaction fields are strings with the exception of tags, which is an array of objects containing key/value pairs, this includes  the `quantity` and `reward` fields as they are represented by [winston strings.](http-api.md#ar-and-winston)

See the [sample transactions](http-api.md#sample-transactions) below for full examples.



#### Field Definitions

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Required</th>
      <th style="text-align:left">Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>id</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">The transaction ID is derrived from the Base64 URL encoding of a SHA-256
        hash of the Base64 decoded <a href="http-api.md#transaction-signing">transaction signature</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>last_tx</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">
        <p>The last outgoing transaction ID from the sending wallet. If this is the
          first transaction from the wallet then an empty string should be used.</p>
        <p></p>
        <p>Use the value returned from the <a href="http-api.md#get-last-transaction-id">last transaction</a> endpoint.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>owner</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">The full RSA modulus value of the sending wallet, Base64 URL encoded.
        The modulus is the <code>n</code> value from the <a href="http-api.md#key-format">JWK</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>tags</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">If no tags are being used then use an empty array <code>[]</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>target</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">The target address to send AR to (if required), the amount to transfer
        should be specified in the <code>quantity</code> field. If no AR is being
        transferred to another wallet then use an empty string.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>quantity</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">The amount to transfer from the <code>owner</code> wallet to the <code>target</code> wallet
        address as a <a href="http-api.md#ar-and-winston">winston string</a>. If
        no AR is being transferred then use an empty string.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>data</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">The data to be submitted as a Base64 URL encoded string. If no data is
        being submitted then this should be an empty string.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reward</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">The transaction fee as a <a href="http-api.md#ar-and-winston">winston string</a>,
        this should be calculated using the <a href="http-api.md#get-transaction-price">price endpoint</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>signature</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">The transaction signature is derrived from concatenating the transaction
        data then signing it, the signature should then be Base64 URL encoded.
        See <a href="http-api.md#transaction-signing">Transaction Signing</a> for
        more.</td>
    </tr>
  </tbody>
</table>

#### **Transaction Use Cases**

**1. Data Transaction**

This is the most common transaction format used to store a piece data on the network. The data should should be base64 URL encoded and go in the `data` field. The `target` and `quantity` fields should be set to empty strings as they are not needed.

**2. Wallet to Wallet AR Transfer**

This type of transaction is used to move AR from one wallet to another. The `data` field should be set to an empty string as it it not needed.

**3. Wallet to Wallet AR transfer with Data**

This type of transaction is for transferring AR with a piece of data attached, this is useful for attaching a message or some other piece of data to a transaction sent to another wallet, for example a reference number or identifier to help account for the transaction. The `data`, `target`, and `quantity` fields should all be used for this type of tranasaction.



#### Sample Transactions

{% tabs %}
{% tab title="Data Transaction" %}
```javascript
{
  "id": "BNttzDav3jHVnNiV7nYbQv-GY0HQ-4XXsdkE5K9ylHQ",
  "last_tx": "jUcuEDZQy2fC6T3fHnGfYsw0D0Zl4NfuaXfwBOLiQtA",
  "owner": "posmE...psEok",
  "tags": [],
  "target": "",
  "quantity": "0",
  "data": "PGh0b...RtbD4",
  "reward": "124145681682",
  "signature": "HZRG_...jRGB-M"
}
```

Some long values have been abbreviated, the full transaction can be found here: [**http://arweave.net/tx/BNttzDav3jHVnNiV7nYbQv-GY0HQ-4XXsdkE5K9ylHQ**](http://arweave.net/tx/BNttzDav3jHVnNiV7nYbQv-GY0HQ-4XXsdkE5K9ylHQ)\*\*\*\*
{% endtab %}

{% tab title="Wallet to Wallet AR Transfer" %}
```javascript
{
  "id": "UEVFNJVXSu7GodYbZoldRHGi_tjzNtNcYjeSkxKCpiE",
  "last_tx": "knQ5gf4Z_3i-NQ6_jFT2a9zShUOHh4lDZoAUzsWMxMQ",
  "owner": "1nPKv...LjJMc",
  "tags": [],
  "target": "WxLW1MWiSWcuwxmvzokahENCbWurzvwcsukFTGrqwdw",
  "quantity": "46598403314697200",
  "data": "",
  "reward": "321179212",
  "signature": "OYIJU...j9Mxc"
}
```

Some long values have been abbreviated, the full transaction can be found here: [**http://arweave.net/tx/UEVFNJVXSu7GodYbZoldRHGi\_tjzNtNcYjeSkxKCpiE**](http://arweave.net/tx/UEVFNJVXSu7GodYbZoldRHGi_tjzNtNcYjeSkxKCpiE)\*\*\*\*
{% endtab %}

{% tab title="Wallet to Wallet AR Transfer with Data" %}
```javascript
{
  "id": "3pXpj43Tk8QzDAoERjHE3ED7oEKLKephjnVakvkiHF8",
  "last_tx": "NpeIbi93igKhE5lKUMhH5dFmyEsNGC0fb2Qysggd-kM",
  "owner": "posmE...psEok",
  "tags": [],
  "target": "pEbU_SLfRzEseum0_hMB1Ie-hqvpeHWypRhZiPoioDI",
  "quantity": "10000000000",
  "data": "VGVzdA",
  "reward": "321579659",
  "signature": "fjL0N...f2UMk"
}
```

Some long values have been abbreviated, the full transaction can be found here: [**http://arweave.net/tx/3pXpj43Tk8QzDAoERjHE3ED7oEKLKephjnVakvkiHF8**](http://arweave.net/tx/3pXpj43Tk8QzDAoERjHE3ED7oEKLKephjnVakvkiHF8)\*\*\*\*
{% endtab %}
{% endtabs %}



### Transaction Signing

Transaction signatures are generated by concatenating the raw and unencoded values from the following fields: **owner, target, data, quantity, reward, last\_tx**, then signing the raw data.

Signatures are **RSA-PSS** with **SHA-256** as the hashing function.

#### Transaction Signing Examples

{% tabs %}
{% tab title="JavaScript" %}
```javascript
function sign(jwk, {owner, target, data, quantity, reward, last_tx}){

    let buffers = [
        this.utils.b64ToBuffer(this.utils.b64urldec(owner)),
        this.utils.b64ToBuffer(this.utils.b64urldec(target)),
        this.utils.b64ToBuffer(this.utils.b64urldec(data)),
        this.utils.stringToBuffer(quantity),
        this.utils.stringToBuffer(reward),
        this.utils.b64ToBuffer(this.utils.b64urldec(last_tx)),
    ];

    let key = await crypto.subtle.importKey(
        'jwk',
        jwk,
        {
            name: 'RSA-PSS',
            modulusLength: 4096,
            publicExponent: new Uint8Array([0x01, 0x00, 0x01]),
            hash: {
                name: 'SHA-256',
            }
        },
        false,
        ['sign']
    );

    let signature = await crypto.subtle.sign(
        {
            hash: 'SHA-256',
            subtle: {
                name: 'RSA-PSS',
                saltLength: 0,
            }
        },
        key,
        buffers
    );
    
    return signature;
}
```
{% endtab %}
{% endtabs %}

### Key Format

Arweave uses the JSON Web Key \(JWK\) format \([RFC 7517](https://tools.ietf.org/html/rfc7517)\) with 4096 length RSA-PSS keys. This JWK format allows for cryptographic keys to be represented as a JSON object where each property represents a property of the underlying cryptographic key.

It's widely supported with libraries for most popular languages. It's possible to convert a JWK to a PEM file or other crypto key file format, support for this this will vary from language to language.

If you're generating your own keys manually **the public exponent \(e\) must be 65537**. If any other value is used then transactions signed by these keys will be invalid and rejected.

#### Addressing

The `n` value is the public modulus and is used as the [transaction owner field](http-api.md#transaction-format), and the address of a wallet is a Base64 URL encoded SHA-256 hash of the `n` value from the JWK.

#### Sample JWK

The address for this wallet is `GRQ7swQO1AMyFgnuAPI7AvGQlW3lzuQuwlJbIpWV7xk`.

```javascript
{
    "kty": "RSA",
    "e": "AQAB",
    "n": "ovFF6EbOtXeg7VnojIgtChgxfU6GZ16JjVj5JFHh6NGHJnq4p059BnMphcDx1mqb3yxM73FxhEszSFLcJiPzway6eIDiXuYiT-Sf_0Wl6_wDLvEmlz43psp7WYJumwpaSyiI_1FWmOVQnTnoAIKaOYKVqzUlteiECQj7XjJl0MZH16RlEfVqVpJ_8Ier4_QXIJ8Y3pe2KF3Lg9UANFU97nuvEM94CSzX-0WIju6Lykt3DBb2YtFFg4bJjOFv3T38nCZmDh8lYjm25_1qILalsB0XRoDxQy9FLxWb4zd09JsDhL0EYAQ_hNfOnQFVOBtYEHVYMCHYH6GoTcNgxmUkZPk4AfpAqZmjDzKfVJrw4Fr68pPTEQOQEzBcIWp61P21BSkhqO4QuFinkQsSH6NdTB_3FpbhYf34Hjf-iH7hdpdWo4aoRLb8eZeZcqBRZoRmlhQnOD-PVxQR_vb9rjXSjGkCWwRbsurVLWdBh_FQn0S9Q6EHqiV8nbW-R0Rk2E76JwgMFkqGUtZj8DeEqXJ2jlAvuzp56fXeAViPEtvUj1HheO8O3LxdVYCiapWWKq4qQVoRzdiyvydYSmbztgFUhekvmjNkxLNKOh71i3hFtoXycegqZ6izrUGoF2oD24lsTKsV5lV5pwfmUjVvxtHZm54bJIMfUDYbOV6yeDjYBb8",
    "d": "EePSrJeFn4f0a8rozPEwnMCeQmdKO3Q2PwYrSJES8Ch9IbzspDXqZThksTJHeya2WXD4O3vlnkRRa5npYOimnTeVO6DO-eNjlgkAhhsEBh5jzRYeChIDMzVdCK1Y7n3a_xCCxiGMk_nteW2_qrqsKy9KtoL90nSmdoV9b9CxvBPhFGyQykF7POkV0fdbaIpGtcayCNJ4ZgMyUpWi0ZwgUhxTUtGsmLlLN2Phg-vt_jZ96h5lS-E1NCUq4ORpj018fDp9DwTdamTyz5LTwaa8F1OCWDPVCW7Ztjs1o-NVXHvejYbhQZeFz9SP804PqLrb1ubDWXmFzKdHns4aRH4bWivh9L8HwSJUl5UEXprJUpYilT0tb3VauI7Cih2LBfhU3fUIDJFYm_j9etgNcPlqt64T7_TI8elgj7-sciXa1XEqIje9Mn8spxT6lpn4nhxJ9qelERCJwiWbuPnW2VsJHeqXZTly52KQEP_UBC4z8a0tDm7HIQw7WQ-OAuNUOu8ongOHaOexkqKYIcF3f812sOIVEJufoBXUUTIvJk-buH0ytgtTjkrO64zZeIvFHa1MFU-6UXh8jipSZ617znNR2Pc1-l3s7pACdbXvy2-5VWE3psRr1L5HM4KNwm6Rs5BXXqBSifzfiJ5qNGqKabfXvPXI8wYyl3mhUQtHW6sUUl0",
    "p": "0q_DP_FzSi8JEd-NNXoIaeL5MOxmNiXmDHGNxP3noKPyr-N6h3CrK5G59Rj2vWAJMhKToz1eSQ1p0-X0Ku2DvdT5LQOGIXVPtojw0OcOI8G8SoqMGAGehaLsnV3vexwtwjLfIM99XccKAxWMA1SMuL48nuBpMUhO0MlagbrL5vfpKB9kL7XCQqspAnN_vBmQZGWYczQmBgfC6v6xGQV3xHJmL--dn-qF2XU9pKuqd0J-cKYcdLPrccdJtGLid4nrSOTDfEbr77IUI5VGWV8CFJ-n8Vki-GwUxUkJpIoRyp5DxnYtSJb7cV-xOf7kBTCEUFn5B8fb2q-d8011cgnp5Q",
    "q": "xfzB-Yf4fa2y2q4ubJCJA5H-IG9-mr7fVRTUbj-gTqVL-I7MCDIImdAPbA-3EoIR5H70GVbAFGQJyYDq6eDeTbNs1zfnU0JPurASE3fKbOpoRdLwXwaSdRJRP9qnqUe-BzuloIzWc-dI-6TJxmHUSA1X9CtHvIdfNdKPCVFKUMrb1bv5arAI8tRbNRfy3tnbiw4wfKhYEQ1e6RPpxAR5F4We9RJ81-sIlfAy7WfliwmcGmgcPNdUinGR299CiVYKf5ktoqGFQ9n6K-v4gNZV23f33-tuD8pMVxyc3xG34j4frH57bsbm7v8Qz-92ZxHWzOUgxIVhGgSaa4E51d9m0w",
    "dp": "yArepo4I230BbZkHKKlv56n81PkAq5UccuA2rb4u-ZXxThP9OTA_NiUtnYxQassOsB53U91m8pHr06hZR5ExL0NSO-1Go-oQ_83SaWeZQ1YmA9i83-ZZr6VcaKbSReAhimxm825PKIVd-kOxJ1BWNOtb_7Yv6v0u6IrmhproE6t8E_6KT8qSYl7Fl3A27lCPiuPz9h6jo8Imzp15ZbqNV1cPs6Ad18MDx8_L8diVCJt4FlmCV0Sl3uhMERx6zumDHzkma4-jYXmCKa8Ilr7g6NgWy8_Ipnto1VFd-H6oGexficaXhH7my2UCj4B23H6OgwSKsVqQY3mvzV3Uj6zeCQ",
    "dq": "a0_ey6OZWnWFleYHH60PtrGw7l_AXZvLbVBG_CLcfwQ1M1oi2OZVpxkQ4t95uTxq-lCdegZ9QhAfBessaOwLUk5IVjbk2Un98RByG784JuS-8-mrg7YKOA5fn56idax_IWiBE46Cxnu8ITlmbHKmHw-sdpnm3hb50jB4evJmt3fcw_KI8_zKPORBM3vxljy7NJnSSh7s7QE0Sl0Svb427Drut6L3rAimtK5mzCseTcg9pkp707ZbClcYWfafF9VdB2A9TgMCOo6xfJEANsT18GkMH4B6PXDHBAhsNrRh2O0XOeWsfZStoyj5Mdt3b9JJfPFMW3h38yQ_lrmKYZQfJQ",
    "qi": "aDsPYxE-JBYsYhCYXSU7WsCrnFxNsRpFMcYXdmdryYIdQUpeemChDGzVJXLnJhE4cAS9TtLcNg82xZSKZvHrnkbFpRfSJxzEnvIXW4V0LHkxkxbmM0e9B7UrpYm6LKtvEY6I7L8wHFpHdOwV6NjY925oULEV156X0r55V7N0XF-jy3rbm71DCWRh6IDRghhCZQ3aNgJxE-OtnABqasaY6CQnTDRXLkGE0kq9GCx85-92fQLHMzvrMhr9m_2MHYJ_gZehL4j95CQzhD3Zh602D0YYYwRSsU4h5HGjlmN52pe-rfTLgwCJq5295s7qUP8TTMzbZAOM_hehksHpAaFghA"
}
```

### AR and Winston

Winston is the smallest possible unit of AR, similar to a [satoshi](https://en.bitcoin.it/wiki/Satoshi_%28unit%29) in Bitcoin, or [wei](http://ethdocs.org/en/latest/ether.html#denominations) in Etherium.

**1 AR** = 1000000000000 Winston \(12 zeros\) and **1 Winston** = 0.000000000001 AR.

The HTTP API will return all amounts as winston strings, this is to allow for easy interoperability between environments that do not accommodate arbitrary-precision arithmetic.

JavaScript for example stores all numbers as double precision floating point values and as such cannot natively express the integer number of winston. Providing these values as strings allows them to be directly loaded into most 'bignum' libraries.

## Transactions

Endpoints for interacting with transactions and related resources.

{% api-method method="get" host="http://arweave.net:1984" path="/tx/{id}" %}
{% api-method-summary %}
Get Transaction by ID
{% endapi-method-summary %}

{% api-method-description %}
Get a transaction by its ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Transaction ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
The transaction as a JSON object.
{% endapi-method-response-example-description %}

```javascript
{
  "id": "BNttzDav3jHVnNiV7nYbQv-GY0HQ-4XXsdkE5K9ylHQ",
  "last_tx": "jUcuEDZQy2fC6T3fHnGfYsw0D0Zl4NfuaXfwBOLiQtA",
  "owner": "posmE...psEok",
  "tags": [],
  "target": "",
  "quantity": "0",
  "data": "PGh0b...RtbD4",
  "reward": "124145681682",
  "signature": "HZRG_...jRGB-M"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}
The transaction ID is known but is still pending, it has not been mined into a block yet.
{% endapi-method-response-example-description %}

```
Pending
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
The provided transaction ID is not valid.
{% endapi-method-response-example-description %}

```
Invalid hash.
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
A transaction with the given ID could not be found.
{% endapi-method-response-example-description %}

```
Not Found.
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
The **quantity** and **reward** values are always represented as winston strings. [**What and why?**](http-api.md#winston-and-ar)\*\*\*\*
{% endhint %}

See the [Transaction Format](http-api.md#transaction-format) section for details about transaction structure and contents, with examples.

{% api-method method="get" host="http://arweave.net:1984" path="/tx/{id}/{field}" %}
{% api-method-summary %}
Get Transaction Field
{% endapi-method-summary %}

{% api-method-description %}
Get a single field from a transaction.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Transaction ID
{% endapi-method-parameter %}

{% api-method-parameter name="field" type="string" required=true %}
Field name. Acceptable values: id, last\_tx, owner, tags, target, quantity, data, reward, signature
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
The field value as plain text
{% endapi-method-response-example-description %}

```
jUcuEDZQy2fC6T3fHnGfYsw0D0Zl4NfuaXfwBOLiQtA
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}
The transaction is pending.
{% endapi-method-response-example-description %}

```
Pending
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
The provided transaction ID is not valid or the field name is not valid.
{% endapi-method-response-example-description %}

```
Invalid hash.
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
A transaction with the given ID could not be found.
{% endapi-method-response-example-description %}

```
Not Found.
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://arweave.net:1984" path="/tx/{id}/data.{extension}" %}
{% api-method-summary %}
Get Transaction Data
{% endapi-method-summary %}

{% api-method-description %}
Get the raw base64 decoded data from a transaction.  
  
  
The `Content-Type` will default to `text/html` so this endpoint will return a browser renderable response by default.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Transaction ID
{% endapi-method-parameter %}

{% api-method-parameter name="extension" type="string" required=true %}
Any extension can be specified depending on the clients use case. Web pages can be requested with `data.html` .
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```markup
<html lang="en-GB" class="b-pw-1280 no-touch orb-js id-svg bbcdotcom ads-enabled bbcdotcom-init bbcdotcom-responsive bbcdotcom-async bbcdotcom-ads-enabled orb-more-loaded  bbcdotcom-group-5" id="responsive-news">
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=1">
...
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}
The transaction is pending.
{% endapi-method-response-example-description %}

```
Pending
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
The provided transaction ID is not valid or the field name is not valid.
{% endapi-method-response-example-description %}

```
Invalid hash.
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
A transaction with the given ID could not be found.
{% endapi-method-response-example-description %}

```
Not Found.
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
A **Content-Type** tag can be submitted with a transaction, the tag will then be used as the Content-Type header when serving the data response, this allows you to submit binary files like images and have them served with correct content type headers over HTTP.

The default Content-Type is **text/html**.
{% endhint %}

{% api-method method="get" host="http://arweave.net:1984" path="price/{bytes}/{target}" %}
{% api-method-summary %}
Get Transaction Price
{% endapi-method-summary %}

{% api-method-description %}
This endpoint is used to calculate the minimum fee \(reward\) for a transaction of a specific size, and possibly to a specific address.  
  
This endpoint should always be used to calculate transaction fees as closely to the submission time as possible. Pricing is dynamic and determined by the network, so it's not always possible to accurately calculate prices offline or ahead of time.  
  
**Transactions with a fee that's too low will simply be rejected.**  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="bytes" type="string" required=true %}
The number of bytes to go into the transaction data field.  
**If sending AR to another wallet with no data attached, then 0 should be used.**
{% endapi-method-parameter %}

{% api-method-parameter name="target" type="string" required=false %}
The target wallet address if sending AR to another wallet.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
**The fee for the first transaction sent to a new wallet address will be 0.25 AR more expensive than other transactions.** This is intentional and to discourage wallet spam.
{% endhint %}

**Examples**

If sending 10 AR to a wallet with address `abc` we would use `/price/0/abc`.

If sending a data transaction with 123 bytes we would use `/price/123`.

If sending 10 AR to another wallet with a data segment of  123 bytes we would use `/price/123/abc`.

{% api-method method="post" host="http://arweave.net:1984" path="/tx" %}
{% api-method-summary %}
Submit a Transaction
{% endapi-method-summary %}

{% api-method-description %}
Submit a new transaction to the network.The request body should be a JSON object with the following attributes.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
application/json
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=false %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
The transaction ID.
{% endapi-method-parameter %}

{% api-method-parameter name="last\_tx" type="string" required=true %}
The last outgoing transaction ID from the sending wallet.
{% endapi-method-parameter %}

{% api-method-parameter name="owner" type="string" required=true %}
The full RSA modulus value for the sending wallet, base64 URL encoded. The modulus is the `n` value from a JWK.
{% endapi-method-parameter %}

{% api-method-parameter name="tags" type="array" required=true %}
\[\]
{% endapi-method-parameter %}

{% api-method-parameter name="target" type="string" required=true %}
The recipient address \(if sending AR to another wallet\). **Use an empty string for data transactions.**
{% endapi-method-parameter %}

{% api-method-parameter name="quantity" type="string" required=true %}
The amount in winston to transfer to the `target` wallet. **Use an empty string for data transactions.**
{% endapi-method-parameter %}

{% api-method-parameter name="data" type="string" required=true %}
The data to be uploaded, base64 URL encoded. **Use an empty string if not required.**
{% endapi-method-parameter %}

{% api-method-parameter name="reward" type="string" required=true %}
The transaction fee.
{% endapi-method-parameter %}

{% api-method-parameter name="signature" type="string" required=true %}
The transaction signature, base64 URL encoded.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
OK
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=208 %}
{% api-method-response-example-description %}
The transaction has already been submitted.
{% endapi-method-response-example-description %}

```
Transaction already processed.
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
The transaction is invalid, couldn't be verified, or the wallet does not have suffucuent funds.
{% endapi-method-response-example-description %}

```
Transaction verification failed.
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=429 %}
{% api-method-response-example-description %}
The request has exceeded the clients rate limit quota.
{% endapi-method-response-example-description %}

```
Too Many Requests
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=503 %}
{% api-method-response-example-description %}
The nodes was unable to verify the transaction.
{% endapi-method-response-example-description %}

```
Transaction verification failed.
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
**Find more information** about these fields and examples in the [transaction format](http-api.md#transaction-format) section.
{% endhint %}

## Wallets

Endpoints for getting information about a wallets.

{% api-method method="get" host="http://arweave.net:1984" path="/wallet/{address}/balance" %}
{% api-method-summary %}
Get a Wallet Balance
{% endapi-method-summary %}

{% api-method-description %}
Get the ballance for a given wallet. Unknown wallet addresses will simply return 0.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="address" type="string" required=false %}
Wallet address.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
The balance as a winston string.
{% endapi-method-response-example-description %}

```
9554799572505
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Error response if the given address is incorrectly formatted.
{% endapi-method-response-example-description %}

```
Invalid address.
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Wallet balances are always represented as winston strings. [**What and why?**](http-api.md#winston-and-ar)\*\*\*\*
{% endhint %}

{% api-method method="get" host="http://arweave.net:1984" path="/wallet/{address}/last\_tx" %}
{% api-method-summary %}
Get Last Transaction ID
{% endapi-method-summary %}

{% api-method-description %}
Get the last outgoing transaction for the given wallet address.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="address" type="string" required=false %}
Wallet address.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
The last transaction ID a sa string.
{% endapi-method-response-example-description %}

```
7SRpf0dWDqN4hbnCMPkdg02u_tzyMBtqwjDBy3EU9dg
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Error response if the given address is incorrectly formatted.
{% endapi-method-response-example-description %}

```
Invalid address.
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Blocks

Endpoints for getting blocks and block data.

{% api-method method="get" host="http://arweave.net:1984" path="block/hash/{block\_hash}" %}
{% api-method-summary %}
Get Block by ID
{% endapi-method-summary %}

{% api-method-description %}
Get a block by its hash \(idep\_hash\).  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="block\_hash" type="string" required=false %}
The block hash \(indep\_hash\).
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
application/json
{% endapi-method-parameter %}

{% api-method-parameter name="X-Block-Format" type="string" required=false %}
2
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
A successful block response using the V2 format.
{% endapi-method-response-example-description %}

```javascript
{
    "nonce": "AQEBAAEBAQAAAAAAAQABAAABAAEAAAEBAAAAAQEBAQAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
    "previous_block": "5M2ADEdNw0m5FnF62eBfFJ82lrizaAbb-gI6h3SNCOcV8JP5S7QQzy7_qf9ZxJsQ",
    "timestamp": 1541689556,
    "last_retarget": 1541688945,
    "diff": 34,
    "height": 78419,
    "hash": "AAAAABXiIEay0l1jH9ibJWKNvCUlxVQrQiZGVyW-4MuDX6Pn_uq6-oOGk3kwAxRa",
    "indep_hash": "fv5jRd2TDURBIJAS0BJCtqY3eXpoXvLu7XE6zFU2sgiKFDZc3D6qChS5V99SRuH0",
    "txs": [],
    "wallet_list": "XYkvWyf0HG2OE1c1_61S6JYew13cKafmshIQ5MGmcAk",
    "reward_addr": "G5m6plnC8pKBQFDZOjZvCscbGL216zE_bCexAzM-7UI",
    "tags": [],
    "reward_pool": 3232,
    "weave_size": 160604943,
    "block_size": 0
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Error response if block hash is not valid or not available.
{% endapi-method-response-example-description %}

```
Block not found.
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="danger" %}
**It's strongly recommended that you specify X-Block-Format: 2  for V2 formatted blocks. The default V1 format is deprecated and will be removed in future releases.** [What's the difference?](http-api.md#block-format)

By default the endpoint returns V1 formatted blocks to maintain backwards compatibility.
{% endhint %}

See the [Block Format](http-api.md#block-format) section for details about the block structure and contents, with examples.

## Network and Node State

Endpoints for getting information about the current network and node state.

{% api-method method="get" host="http://arweave.net:1984" path="/info" %}
{% api-method-summary %}
Network Info
{% endapi-method-summary %}

{% api-method-description %}
Get the current network information including height, current block, and other properties.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "network": "arweave.N.1",
  "version": 3,
  "release": 16,
  "height": 78309,
  "current": "o8ahQ55Omd7Fdi4UgGP82bD2-TZ66JYY33NzGyvpLL3_V3wCmsq8NJmnkJl1p_ew",
  "blocks": 97375,
  "peers": 64,
  "queue_length": 0,
  "node_state_latency": 18
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://arweave.net:1984" path="/peers" %}
{% api-method-summary %}
Peer list
{% endapi-method-summary %}

{% api-method-description %}
Get the list of peers that the node. Nodes can only respond with peers they currently know about, so this will not be an exhaustive or complete list of nodes on the network.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  "127.0.0.1:1984",
  "0.0.0.0:1984"
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



