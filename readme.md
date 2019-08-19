<!-- WEEK 2 -->

Ethereum Incentive Model

1. Ethereum also uses a incentive-based model for block creation.

2. Every action in ETH network requires gas. Gas points are used to specify the fees inside of Ether, for ease of computation using standard values.

3. Ether varies in value, gaspoints do now. They allow for the different/independent value of the txn fee and computation fee.

4. ETH has specified gpoints for each type of txn.

5. If fees insufficient, txn is rejected.

Blocks

1. Gas Limit - amount of gaspoints available for a block to spend.

For example, if a block specifies a limit of 1 million 5 hundred thousand units of gas, and a basic Ether transaction fee is 21,000, this particular Ethereum block can fit about 70 plain Ether transactions. If we add smart contract transactions also into this block, that usually requires more gas, and the number of transactions for this block will likely be lower.

If smart contracts added, they require more gas.

2. Gas Spent

<!-- Incentive Model Summarised -->
Gas spent is the actual amount of gas spent at the completion of the block creation.

The proof of work puzzle winner, miner that creates a new block, is incentivized with the base fees of three Ethers, and the transaction fees in Ethereum blockchain.

The winning miner also gets the fees, gas points for execution of a smart contract transactions.

<!-- POW vs POS -->

POW
- Nodes on network do puzzle to verify txn's. The work must be hard but eay to check. 

- Rewards are paid by network.

- Difficulty increases with more miners.

- Competitive system.

- 51% needed to overtake network.

POS

- Similar to POW.

- The creator of a new block is determined from a pool of users with a certain amount of cryptocurrency.

- There is no puzzle and no reward.

- Miners take fees from blocks.

- Pentalty of harming network is possibility of losing money staked.

- Need to own 51% of currency on chain to overtake network (not 51% of computing power).

- POW miners need lots of power to confirm blocks. POS does not.

<!-- WEEK 3 -->
*Algorithms & Techniques*

<!-- Asymmetric key encryption -->

- Peer Participants
- Authenticate Txn's

Do these by using public key cryptography.

Symmetric key encrytpion is easy to hack.

Public Key Cryptography - private key kept safe and locked.

The public-key private key pair has the unique quality that even though a data is encrypted with the private key, it can be decrypted with the corresponding public-key and vice versa. 

A sends tranfer to B, encrypted by A's private key. This is encrypted by B's public key.

B then decrypts using their own private key. Then uses A's public key on the signed txn to decrypt the assigned txn data. 

This ensures B can decrypt & receive and only A could have sent the data.

Elliptic Curve Cryptography - Elliptic Curve Cryptography, ECC family of algorithms is used in the bitcoin as well as an Ethereum block chain for generating the key pair

<!-- Hashing -->
Need to protect private key for security of assets on the BC.

A hash function or hashing transforms and maps an arbitrary length of input data value to a unique fixed length value. 

2 Req's for Hashing:
1. Algo's should be 1-way function. To ensure no one can derive the original items hashed from the hash value.

2. Collision free or low-prob of collision. Ensure the hash value UNIQUELY represents the original item/s hashed. 

Use large # of of bits in the hash value to achieve 1 & 2. 256-bits and common functions - SHA-256 and Keccak.

A simple hash - all the data items are linearly arranged and hashed. Use when we have a fixed number of items to be hashed.

Merle tree hash - the data is at the leaf nodes of the tree, leaves are pairwise hash to arrive at the same hash value as a simple hash. Use when the number of items differ from block to block.

Summarizing, in Ethereum, hashing functions are used for generating account addresses, digital signatures, transaction hash, state hash, receipt hash and block header hash. SHA-3, SHA-256, Keccak-256 are some of the algorithms commonly used by hash generation in blockchains.


<!-- Transaction Integrity -->
1. Secure a unique account address
We need a standard approach to uniquely identify the participants in the decentralized network.

Addresses of accounts are generated using public key, private key pair. 

i. 256-bit random number is generated, and designated as the private key. Kept secure and locked using a passphrase.

ii. ECC algorithm is applied to the private key, to get a unique public key. This is the private public key pair.

iii. Then a hashing function is applied to the public key to obtain account address. The address is shorter in size, only 20 bytes or 160 bits.

2. Auth of the txn by the sender through digital signing.

A transaction for transferring assets will have to be authorized, it has to be non-repudiable, and unmodifiable. 

Data is hashed and encrypted. This is the digital signature. 

The receiver gets the original data, and the secure hash digitally signed.

Receiver can recompute the hash of the original data received, and compare it with the received hash to verify the integrity of the document.

3. Verify the content of the txn is not modified.

i. Find the hash of the data fields of the transaction.

ii. Encrypt that hash using the private key of the participant originating the transaction.

iii. This hash just added to the transaction. It can be verified by others decryiptng it using the public key of the sender of the transaction, and recomputing the hash of the transaction. Then, compare the computed hash, and the hash received at the digital signature. If that is a match, accept the transaction.

<!-- Securing the Blockchain -->

Main components of the ETH block are:
1. Block Header
2. Txn hash
3. Txn root
4. State Hash
5. State Root

In Ethereum, the block hash is the block of all the elements in the block header, including the transaction root and state root hashes.

Computed by using Keccak on all the items within the header.

Smart contract execution in Ethereum results in state transitions. Every state change requires state root hash re-computation. Instead of computing hash for the entire set of states, only the affected path in the Merkle tree needs to be re-computed.

<!-- Block Hash Computation -->
Block hash in Ethereum is computed by first computing the state root hash, transaction root hash and then receipt root hash.

These roots and all the other items in the header are hash together with the variable nonce to solve the proof of work puzzle.

Block hash serves two important purposes; verification of the integrity of the block and the transactions, formation of the chain link by embedding the previous block hash in the current block header.