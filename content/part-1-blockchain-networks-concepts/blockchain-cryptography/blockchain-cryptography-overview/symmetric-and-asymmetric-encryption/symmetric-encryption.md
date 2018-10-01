# Symmetric Encryption - Concepts and Algorithms

**Symmetric encryption** schemes use **the same key** (or password) to **encrypt** data and **decrypt** the encrypted data back to its original form:

![](/assets/symmetric-encryption.png)

## Secret Keys

The single **secret key** used to **cipher** (encrypt) and **decipher** (decrypt) data is typically of size 128, 192 or 256 bits and is sometimes referred as "**_shared key_**", because both sending and receiving parties should know it.

Most applications use a **[password-to-key-derivation](//content/part-1-blockchain-networks-concepts/blockchain-cryptography/blockchain-cryptography-overview/hmac-and-key-derivation.html)** scheme to extract secret key from certain password, because users tend to remember passwords easier than binary data.

Example of **256-bit secret key**, encoded as hex string:
```
02c324648931b89e3e8a0fc42c96e8e3be2e42812986573a40d46563bceaf75110
```
In many blockchain systems keys are encoded as **[base58](https://en.wikipedia.org/wiki/Base58)** or **[base64](https://en.wikipedia.org/wiki/Base64)** for shorter string representation.

For example, the above key looks like this in **base58**:
```
pbPRqYDxnKZfs8j4KKiqYmx6nzipAjTJf1oCD1WKgy99
```

The same key looks like this in **base64**:
```
AsMkZIkxuJ4+ig/ELJbo474uQoEphlc6QNRlY7zq91EQ
```

In **decimal** system, the above key is the following integer number:
```
319849484316084980661994213716306415989897600164422912728298459349458028548368
```

## Modern Symmetric Encryption Algorithms

Widely used in modern cryptography symmetric encryption algorithms (cyphers) are: **[AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)** (AES-128, AES-192, AES-256), **[Twofish](https://en.wikipedia.org/wiki/Twofish)** and **[IDEA](https://en.wikipedia.org/wiki/International_Data_Encryption_Algorithm)**.

We shall give more details and code examples using these algorithms a bit later.

## Symmetric Encryption - Online Demo

In order to better understand the idea behind the symmetric encryption, you can play with some **online symmetric encryption tool** to encrypt and decrypt a sample message by sample secret key (or password). You can play a bit with this site: **[https://aesencryption.net](https://aesencryption.net)**.

![](/assets/aesencryption.net.png)

It demonstrates how we can encrypt and decrypt messages, using the **AES cipher** (with some default settings) and certain password-to-key-derivation function. In the above example if we encrypt "**_secret msg_**" by the password "**_p@ss_**", we will get the [base64-encoded](https://en.wikipedia.org/wiki/Base64) binary data "**_jVJwOBmH+qMqHdg22KwMyg==_**" as output. After decryption we get back the original text "**_secret msg_**".

Note that the above encrypted text is dependent to many parameters and algorithm settings, so if you encrypt the same at another "_AES live example_" web site, the result will be different.
