# PBKDF2: Derive Key from Password

**PBKDF2** is a simple cryptographic key derivation function, which is resistant to [dictionary attacks](https://en.wikipedia.org/wiki/Dictionary_attack) and [rainbow table attacks](https://en.wikipedia.org/wiki/Rainbow_table) . It is based on iteratively deriving **HMAC** many times with some padding. It is described in the Internet standard [RFC 2898 (PKCS #5)](http://ietf.org/rfc/rfc2898.txt).

Technically, the **input data** for **PBKDF2** consists of:
 - `password` – array of bytes / string, e.g. "_p@$Sw0rD~3_"
 - `salt` – securely-generated random bytes, e.g. "_df1f2d3f4d77ac66e9c5a6c3d8f921b6_"
 - `iterations-count`, e.g. 1024 iterations
 - hash-function for calculating **HMAC**, e.g. `SHA256`
 - `derived-key-len` for the output, e.g. 256 bits

The **output data** is the **derived key** (e.g. 256 bits).

## PBKDF2 and Number of Iterations

**PBKDF2** allows to configure the number of **iterations** and thus to configure the time required to derive the key.
 - **Slower key derivation** means high login time / slower decryption / etc. and **higher resistance** to password cracking attacks.
 - **Faster key derivation** means short login time / faster decryption / etc. and **lower resistance** to password cracking attacks.
 - PBKDF2 is **not resistant** to [GPU attacks](https://security.stackexchange.com/questions/118147/how-are-gpus-used-in-brute-force-attacks) (parallel password cracking using video cards) and to [ASIC attacks](https://en.wikipedia.org/wiki/Custom_hardware_attack) (specialized password cracking hardware). This is the main motivation behind more modern KDF functions.
 
## PBKDF2 - Example
 
Try PBKDF2 key derivation online here: https://asecuritysite.com/encryption/PBKDF2z.

![](/assets/PBKDF2-calculator.png)

Try to **increase the iterations count** to see how this affects the speed of key derivation.

## PBKDF2 Calculation in Python - Example

Now, we shall write some **code in Python** to derive a key from a password using the **PBKDF2** algorithm.

First, install the Python package `backports.pbkdf2` using the command:
```
pip install backports.pbkdf2
```

Now, write the Python code to calculate PBKDF2:
```python
import os, binascii
from backports.pbkdf2 import pbkdf2_hmac

salt = binascii.unhexlify('df1f2d3f4d77ac66e9c5a6c3d8f921b6')
passwd = "p@$Sw0rD~3".encode("utf8")
key = pbkdf2_hmac("sha256", passwd, salt, 50000, 32)
print("Derived key:", binascii.hexlify(key))
```

The **PBKDF2** calculation function takes several **input parameters**: **hash function** for the HMAC, the **password** (bytes sequence), the **salt** (bytes sequence), **iterations** count and the output **key length** (number of bytes for the derived key).

The **output** from the above code execution is the following:
```
Derived key: b'78856da569d1aa59c42c19f6b6c96ba773a4bb1f4d7a2787cd75095d6d7fd145'
```

Try to change the number of **iterations** and see whether and how the **execution time** changes.
