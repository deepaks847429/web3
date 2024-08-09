How Blockchains do auth?
If you ever want to create an account on a blockchain, you need to generate a public-private keypair.

Public private Keypair
A public-private key pair is a set of two keys used in asymmetric cryptography. These two keys have the following characteristics:

Public Key: The public key is a string that can be shared openly.
Private key: The private key is a secret string that must be kept confidential. 


->Bits and bytes
What is a Bit?
A bit is the smallest unit of data in a computer and can have one of two values: 0 or 1.
Think of a bit like a light switch that can be either off (0) or on (1). 

->What is a byte?
A byte is a group of 8 bits. It’s the standard unit of data used to represent a single character in memory. Since each bit can be either 0 or 1, a byte can have 2^8 (256) possible values, ranging from 0 to 255

What is the 11001010 converted to a decimals ?
2^7: 1×27=1×128=128
2^6: 1×26=1×64=64
2^5: 0×25=0×32=0
2^4: 0×24=0×16=0
2^3: 1×23=1×8=8
2^2: 0×22=0×4=0
2^1: 1×21=1×2=2
2^0: 0×20=0×1=0
= 202

Why use UInt8Array over native arrays ?
They use less space. Every number takes 64 bits (8 bytes). But every value in a UInt8Array takes 1 byte.
UInt8Array Enforces constraints - It makes sure every element doesn’t exceed 255.

->Encodings
Bytes are cool but highly unreadable. Imagine telling someone.
It’s easier to encode data so it is more human readable .
 Some common encodings include - 
Ascii
Hex
Base64
Base58



->ascii
1 character = 7 bits
Every byte corresponds to a text on the computer . 



->hex
Hex
1 character = 4 bits
A single hex character can be any of the 16 possible values: 0-9 and A-F.


->Base64
1 character = 6 bits
Base64 encoding uses 64 different characters (A-Z, a-z, 0-9, +, /), which means each character can represent one of 64 possible values.



->Base58
It is similar to Base64 but uses a different set of characters to avoid visually similar characters and to make the encoded output more user-friendly
Base58 uses 58 different characters:
Uppercase letters: A-Z (excluding I and O)
Lowercase letters: a-z (excluding l)
Numbers: 1-9 (excluding 0)



Hashing vs encryption
Hashing
Hashing is a process of converting data (like a file or a message) into a fixed-size string of characters, which typically appears random. 
Common hashing algorithms - SHA-256, MD5

->Encryption
Encryption is the process of converting plaintext data into an unreadable format, called ciphertext, using a specific algorithm and a key. The data can be decrypted back to its original form only with the appropriate key.
Key Characteristics:
Reversible: With the correct key, the ciphertext can be decrypted back to plaintext.
Key-dependent: The security of encryption relies on the secrecy of the key.
Two main types:
Symmetric encryption: The same key is used for both encryption and decryption.
Asymmetric encryption: Different keys are used for encryption (public key) and decryption (private key).


Asymetric Encryption
Asymmetric encryption, also known as public-key cryptography, is a type of encryption that uses a pair of keys: a public key and a private key. The keys are mathematically related, but it is computationally infeasible to derive the private key from the public key.
Public Key: The public key is a string that can be shared openly
Private Key: The private key is a secret cryptographic code that must be kept confidential. It is used to decrypt data encrypted with the corresponding public key or to create digital signatures.

Common Asymmetric Encryption Algorithms:
RSA - Rivest–Shamir–Adleman
ECC - Elliptic Curve Cryptography (ECDSA) - ETH and BTC
EdDSA - Edwards-curve Digital Signature Algorithm  - SOL

Common eleptic curves
secp256k1 - BTC and ETH
ed25519 - SOL
 
Few usecases of public key cryptography - 
SSL/TLS certificates
SSH keys to connect to servers/push to github
Blockchains and cryptocurrencies
 

 ->Creating a public/private keypair


 ->How to transactions work on the blockchain?
Ref - https://andersbrownworth.com/blockchain/
User side
User first creates a public/private keypair
They create a transaction that they want to do (send Rs 50 to Alice).  The transaction includes all necessary details like the recipient's address, the amount and some blockchain specific parameters (for eg - latestBlockHash in case of solana)
They hash the transaction 
They sign the transaction using their private key
They send the raw transaction , signature and their public key to a node on the blockchain.
Miner
Hashes the original message to generate a hash
Verifies the signature using the users public key and the hash generated in step 1
Transaction validation - The miner/validator checks additional aspects of the transaction, such as ensuring the user has sufficient funds
If everything checks out, adds the transaction to the block
 

 ->Hierarchical Deterministic (HD) Wallet
Hierarchical Deterministic (HD) wallets are a type of wallet that can generate a tree of key pairs from a single seed.  This allows for the generation of multiple addresses from a single root seed, providing both security and convenience.

->Problem 
You have to maintain/store multiple public private keys if you want to have multiple wallets. 
Solution - BIP-32
Bitcoin Improvement Proposal 32 (BIP-32) provided the solution to this problem in 2012. It was proposed by Pieter Wuilla, a Bitcoin Core developer, to simplify the recovery process of crypto wallets. BIP-32 introduced a hierarchical tree-like structure for wallets that allowed you to manage multiple accounts much more easily than was previously possible. It’s essentially a standardized way to derive private and public keys from a master seed.

