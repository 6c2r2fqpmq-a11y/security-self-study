# TryHackMe: Cryptography

## Overview

This module covers the concepts that quietly underpin almost everything else in security - encoding vs. encryption, symmetric vs. asymmetric ciphers, hashing, and the tools used to crack or verify each. It's easy to treat cryptography as pure theory, but this module kept tying every concept back to something concrete: an SSH key, a GPG-encrypted message, a leaked password hash.

## Rooms Covered

- Encryption - Crypto 101
- Hashing - Crypto 101
- John the Ripper: The Basics

## Key Concepts

Before any of the hands-on work, the rooms establish a shared vocabulary that everything else builds on:

- **Plaintext** - the original, readable data
- **Ciphertext** - the result of encrypting plaintext
- **Encoding** - *not* encryption. Formats like base64 or hex just represent data differently and are immediately, trivially reversible by anyone
- **Encryption** - transforms plaintext into ciphertext using a cipher and a key. Rreversible only if you have the key
- **Hash** - a one-way function's output. Hashes aren't decrypted, they're *cracked* by hashing guesses and comparing

Getting encoding and encryption straight early mattered more than I expected. A lot of "obfuscated" malware or CTF payloads is just base64/hex encoded, not actually encrypted, which changes the entire approach: you don't need a key, you just need to recognize the encoding and reverse it.

## Symmetric & Asymmetric Encryption

The room walked through the two families of encryption:

- **Symmetric** (**AES**): the same key encrypts and decrypts. Fast, but the key has to be shared securely beforehand, which is its core weakness.
- **Asymmetric** (**RSA**): a public/private key pair. Anyone can encrypt with the public key, but only the private key holder can decrypt, which solves the key-distribution problem symmetric encryption has.

**Hands-on work:**

- Cracked a passphrase-protected SSH private key using 'ssh2john' to convert it into a crackable hash format, then ran it through **John the Ripper** against the 'rockyou.txt' wordlist to recover the passphrase.
- Imported a provided GPG private key with 'gpg --import' and decrypted an encrypted message with 'gpg --decrypt' to reveal the hidden plaintext.
- Worked through an AES decryption task, reinforcing why AES-256 remains the standard for bulk data encryption even in a post-quantum-computing conversation (asymmetric algorithms like RSA are far more vulnerable to quantum attacks than symmetric ones like AES) .

## Hashing & John the Ripper

Hashing looks similar to encryption on the surface but serves a different purpose entirely: instead of protecting confidentiality, it verifies **integrity**. The same input always produces the same fixed-length output, and changing even a single bit of input completely changes the hash. That property is what makes hashes useful for detecting tampered files and for storing passwords without keeping the plaintext around.

I used **John the Ripper** to identify and crack multiple hash types:

- Identified an unknown hash as MD5, then cracked it against 'rockyou.txt' to recover the plaintext password
- Repeated the process against a SHA-1 hash

The room also covered **HMAC** (Hash-based Message Authentication Code), which combines a hash function with a secret key to provide both integrity *and* authenticity, proving not just that data wasn't altered, but that it came from someone who actually holds the shared secret. TryHackMe's own VPN, as an example the room points out, uses HMAC-SHA512 for exactly this reason.

## Takeaways

This module gave me the "why" behind tools I used elsewhere in the path. Decoding a base64 payload in CyberChef, recognizing a hash format during the OWASP room's cookie/session analysis, understanding why a stolen password hash isn't immediately game over. Cryptography ended up being less about memorizing algorithm names and more about knowing which property (confidentiality, integrity, or authenticity) a given tool is actually providing, and picking the right one for the job.
