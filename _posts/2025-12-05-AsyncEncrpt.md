---
title: Asynchronous Encryption 
description: BYU CTF 2026
author: Zinko
date: 2025-12-05
categories: [Crypto]
---

In this challenge we are given plaintext and ciphertext. We are also given a encrpytion file and are to brute force the key.

I started off by looking at one of the functions that we were given.
```python
def example(mode):

    print("Testing")

    public_key, private_key = call_generate_key_pair("automatic")

    test_message = "The Quick Brown Fox Jumped Over The Lazy Dog"

    encrypted_message = call_encrypt(test_message, public_key)

    if mode == "return_encrypted_message":
        return encrypted_message
    elif mode == "return_encrypted_message_and_plaintext":
        return encrypted_message, test_message
    else:
        decrypted_message = call_decrypt(encrypted_message, private_key)

        return decrypted_message
```

Looking at the encryption function that is called, it's calling from a set character set.
(Asymetric.py)
```python
DEFAULT_CHARS = (
    list("abcdefghijklmnopqrstuvwxyz") +
    list("ABCDEFGHIJKLMNOPQRSTUVWXYZ") +
    list("0123456789") +
    list(".,<>?'[]@#$%&*~!") +
    [" "]  # include space if you want it treated as a symbol
)

# Directly build hardcoded mappings at import time
DEFAULT_NTL = {i: ch for i, ch in enumerate(DEFAULT_CHARS)}
```

It only has 79 characters that it can pull from, easy enough to brute force.

Helpfully they gave us a function to use and some epic helper functions that we saw in the example function earlier! I took those, copied them, and did some slight modification.
```python
def brute_force(to_decrypt, plaintext):
    print("Create a brute force function to get the key!")
    while True:
        public_key, private_key = call_generate_key_pair("automatic")

        decrypted_message = call_decrypt(to_decrypt, private_key)

        if decrypted_message==plaintext:
            print("Found the keys!")
            print("Public Key" + str(public_key))
            print("Private Key" + str(private_key))
            break
```

Now it's as simple as calling the function, grabbing the keys, and then using them to decrpyt the flag with Asymetric.py! 

Flag: `byuctf{Mar15,44BC,CuriaDiPompeo}`
