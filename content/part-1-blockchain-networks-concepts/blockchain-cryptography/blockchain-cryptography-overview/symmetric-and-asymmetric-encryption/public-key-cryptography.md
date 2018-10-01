# Public Key Cryptography - Concepts

Before introducing the **asymmetric key encryption** schemes and algorithms, we should first understand the concept of **public key cryptography**.

The **public key cryptography** uses a different key to encrypt and decrypt data (or to sign and verify messages). Keys come in **public-private key pairs**.

Data encrypted by a public key is decrypted by the corresponding private key:

![](/assets/public-key-cryptography-encrypt-decrypt.png)

A message signed by a private key is verified by the corresponding public key.

![](/assets/public-key-cryptography-sign-verify.png)

## Key Pairs

The **public key cryptography** uses a **pair of keys**: **public key** + **private key**. These keys are mathematically connected and are used as **pair**.

In some public key cryptosystems (like the Elliptic-Curve Cryptography - ECC), the public key can be calculated from the private key. In other cryptosystems (like RSA), the public key and the private key are generated together but cannot be calculated from each other.

Usually, a **public / private key pair** is randomly generated in a secure environment (e.g. in a hardware wallet) and the public key is revealed, while the private key is securely stored in a crypto-wallet and is protected by a password or by multi-factor authentication.

Example of public key and its corresponding private key:
```
privKey: 648fc1fa828c7f185d825c04a5b21af9e473b867eeee1acea4dbab938433e158
pubKey: 02c324648931b89e3e8a0fc42c96e8e3be2e42812986573a40d46563bceaf75110
```

## Private Keys

Message **encryption** and **signing** is done by a **private key**. The private keys are always kept **secret** by their owner, just like passwords. In the blockchain systems the private keys usually stay in specific software or hardware apps / devices called "**crypto wallets**", which store securely a set of private keys.

## Public Keys

Message **decryption** and **signature verification** is done by the **public key**. Public keys are by design public information (not a secret). They are usually published as parts of the blockchain transactions.

In most blockchain systems the **blockchain address** is derived from the public key, so if you have someone's public key, you are assumed to have his blockchain address as well.

A certain **public key** can be connected to certain **person** or **organization** or is used anonymously. You can never know who is the owner of the private key, corresponding to certain public key.
