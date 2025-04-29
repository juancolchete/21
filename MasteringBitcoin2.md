# Chapter 3
## Why is Bitcoin Core called a "Reference Implementation"? What other implementations of Bitcoin are out there? Over 95% of Bitcoin nodes run Bitcoin Core, what's the problem of running a different implementation?
Network effect, some different implementation Libbitcoin, btcd, BitcoinJ, Bitcoin Knots, Bcoin. The pratical problem is the maintenability, troubles on implementation and bugs.  
## What are BIPs (Bitcoin Improvement Proposals)? What are their role in the Bitcoin development process?
BIPs are protocol changes to change the Bitcoin current implementation, their role is to update, do security changes and all bitcoin core changes.  
## What are some common reasons you would run your own full node?
Soberany, no need to trust anyone, be part of consensus.  
## What is the difference between a pruned node and a full (AKA archival) node?
Pruned do not store all the consensus, and full node store all blockchain data, and be able to retrive old data
# Chapter 4
## What is the relationship between private keys, public keys, and signatures?
**private key**: the only key that can validate your spenses  
**public key**: the key that can validate the signature  
**signatures**: message signed by privatekey  
## What is a Bitcoin address, and why are addresses used instead of raw public keys?
To protect privacy.
## How do we know that the discrete log problem is hard to break?

## What are output and input scripts? How do they relate to receiving and spending Bitcoins?
## What are the differences between P2PKH and P2SH?
## What are Bech32 and Base58 addresses? What issues are associated with each?
