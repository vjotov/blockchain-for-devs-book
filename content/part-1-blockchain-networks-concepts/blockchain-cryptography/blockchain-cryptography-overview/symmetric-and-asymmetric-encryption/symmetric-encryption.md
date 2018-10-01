# Symmetric Encryption - Concepts and Algorithms

**Symmetric encryption** schemes use **the same key** (or password) to **encrypt** data and **decrypt** the encrypted data back to its original form:

![](/assets/symmetric-encryption.png)

The single **secret key** used to **cipher** and **decipher** data is typically of size 128, 192 or 256 bits and is sometimes referred as "**_shared key_**", because both sending and receiving parties should know it.

Most applications use a **[password-to-key-derivation](//content/part-1-blockchain-networks-concepts/blockchain-cryptography/blockchain-cryptography-overview/hmac-and-key-derivation.html)** scheme to extract secret key from given password, because users tend to remember passwords easier than binary data.

Widely used in modern cryptography symmetric encryption algorithms (cyphers) are: **[AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)** (AES-128, AES-192, AES-256), **[Twofish](https://en.wikipedia.org/wiki/Twofish)** and **[IDEA](https://en.wikipedia.org/wiki/International_Data_Encryption_Algorithm)**. We shall give some code examples using these algorithms a bit later.
