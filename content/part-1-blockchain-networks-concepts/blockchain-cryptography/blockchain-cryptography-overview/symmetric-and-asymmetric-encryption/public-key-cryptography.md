# Public Key Cryptography - Concepts

Before introducing the **asymmetric key encryption** schemes and algorithms, we should first understand the concept of **public key cryptography**.

The **public key cryptography** uses a different key to encrypt and decrypt data (or to sign and verify messages). Keys come in **public-private key pairs**.

## Asymmetric Encryption / Decryption

Data **encrypted by a public key** is **decrypted** by the corresponding **private key**:

![](/assets/public-key-cryptography-encrypt-decrypt.png)

The encrypted data, obtained as result of encryption is called "**ciphertext**". The ciphertext is a binary sequence, unreadable by humans and typically cannot be restored without the decryption key.

Public key encryption can work also in the opposite scenario: encrypt data by a private key and decrypt it by the public key. Thus someone can prove that he is owner of certain private key, while revealing only its corresponding public key.

## Asymmetric Signing / Verification

A message **signed by a private key** is the signature is **verified** by the corresponding **public key**.

![](/assets/public-key-cryptography-sign-verify.png)

**Digital signatures** will be explained in more details later, but in short: a message signed by certain private key can be verified by the corresponding public key. A **signed message** cannot be altered after signing. A message signature proves that certain message (e.g. blockchain transaction) is created by the owner of certain public key (in blockchain -> by the owner of certain address).

## Key Pairs

The **public key cryptography** uses a **pair of keys**: **public key** + **private key**. These keys are mathematically connected and are used as **pair**.

In some public key cryptosystems (like the Elliptic-Curve Cryptography - **ECC**), the public key can be calculated from the private key. In other cryptosystems (like **RSA**), the public key and the private key are generated together but cannot be calculated from each other.

Usually, a **public / private key pair** is randomly generated in a secure environment (e.g. in a hardware wallet) and the public key is revealed, while the private key is securely stored in a crypto-wallet and is protected by a password or by multi-factor authentication.

**Example** of 256-bit public key and its corresponding 256-bit private key (both based on the classical elliptic curves cryptosystem, used in Bitcoin and Ethereum):
```
privKey: 648fc1fa828c7f185d825c04a5b21af9e473b867eeee1acea4dbab938433e158
pubKey: 02c324648931b89e3e8a0fc42c96e8e3be2e42812986573a40d46563bceaf75110
```

## Private Keys

Message **encryption** and **signing** is done by a **private key**. The private keys are always kept **secret** by their owner, just like passwords. In the blockchain systems the private keys usually stay in specific software or hardware apps / devices called "**crypto wallets**", which store securely a set of private keys.

**Example** of 256-bit private key:
```
648fc1fa828c7f185d825c04a5b21af9e473b867eeee1acea4dbab938433e158
```

## Public Keys

Message **decryption** and **signature verification** is done by the **public key**. Public keys are by design public information (not a secret). They are usually published as parts of the blockchain transactions.

**Example** of 256-bit public key:
```
02c324648931b89e3e8a0fc42c96e8e3be2e42812986573a40d46563bceaf75110
```

In most blockchain systems the **blockchain address** is derived from the public key, so if you have someone's public key, you are assumed to have his blockchain address as well.

A certain **public key** can be connected to certain **person** or **organization** or is used anonymously. You can never know who is the owner of the private key, corresponding to certain public key.
