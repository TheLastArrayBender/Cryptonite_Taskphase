## 1. New Caesar

In this problem, the encryption procedure is a two-step process:

1. The flag is first converted to base16 using the function `b16_encode`
2. The base16 flag is then shifted using the `shift` function. Here, each character of the flag is replaced by the character at the index in the `ALPHABET` list obtained by adding the alphabetical index of the character and the key (mod 16).

To decrypt the message, you need to follow the reverse procedure:

1. Unshift the characters: For this, you define the `unshift` function that does the reverse of what the `shift` function does. It subtracts the alphabetical index of the key from the alphabetical index of the given character (mod 16). This gives you the original base16 flag.

2. Decode the base16 flag: For this, you define the `decode` function. This function takes two characters at a time from the base16 flag, converts them to binary, and then converts them to ASCII to get the original flag.

Here is the Python code for this:

```python
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

def unshift(c, k):
    t1 = ord(c) - LOWERCASE_OFFSET
    t2 = ord(k) - LOWERCASE_OFFSET
    return ALPHABET[(t1 - t2) % 16]

def decode(enc):
    dec = ""
    for i in range(0, len(enc), 2):
        binary = "{0:04b}{1:04b}".format(ALPHABET.index(enc[i]), ALPHABET.index(enc[i+1]))
        dec += chr(int(binary, 2))
    return dec

flag = "dcebcmebecamcmanaedbacdaanafagapdaaoabaaafdbapdpaaapadanandcafaadbdaapdpandcac"

for key in ALPHABET:
    b16 = ""
    for c in flag:
        b16 += unshift(c, key)
    print(decode(b16))
```

This code first tries all possible keys from 'a' to 'p' to unshift the characters in the given encrypted flag. It then decodes the unshifted flag and prints the result. The correct decrypted flag is the one that contains meaningful words [Source 3](https://www.scaler.com/topics/caesar-cipher-python/), [Source 4](https://www.geeksforgeeks.org/caesar-cipher-in-cryptography/), [Source 9](https://the-algorithms.com/algorithm/caesar-cipher?lang=python).

## 2. miniRSA

In this problem, the ciphertext is encrypted using RSA encryption with a small exponent `e`. This makes it vulnerable to brute force attacks.

The RSA encryption is done using the formula `c = m^e mod N`, where `m` is the plaintext message, `e` is the public exponent, `c` is the ciphertext, and `N` is the product of two prime numbers.

The decryption is done using the formula `m = c^d mod N`, where `d` is the private exponent.

In this case, because `e` is small, you can use brute force to find the plaintext message `m` that, when encrypted, equals the given ciphertext `c`.

You can use online tools like the dcode RSA decryptor to decrypt the ciphertext [Source 4](https://www.geeksforgeeks.org/caesar-cipher-in-cryptography/).

## 3. basic-mod1

In this problem, a message is encrypted by converting each number to its remainder when divided by 37 (mod 37), and then using these remainders as indices in a list of characters.

The decryption procedure is to reverse this process:

1. Convert each character back to its index in the list.
2. Multiply each index by 37 to get back the original numbers.

Here is the Python code for this:

```python
import string

message = [350, 63, 353, 198, 114, 369, 346, 184, 202, 322, 94, 235, 114, 110, 185, 188, 225, 212, 366, 374, 261, 213]
keys = [i for i in string.ascii_uppercase + string.digits + '_']

for char in message:
    print(keys[char % 37])
```

This code first creates a list of characters, where the indices are the remainders when divided by 37. It then converts each number in the message back to its character representation by finding its remainder when divided by 37 and using this as an index in the list of characters [Source 0](https://dev.to/ramakm/caesar-cipher-encryption-decryption
