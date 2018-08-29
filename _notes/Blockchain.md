---
layout: post
title:  Blockchain Notes 
---

Blockchain Advantages
---------------------
Secure
Shared: 
Distributed: many copies of ledger
Ledger: nowhere to hide

Blockchain | Multiple Chain Types
---------------------------------
Blockchains: bitcoin, ethereum, reipple
Alternatives blockchains (altchains): digital asset, hyperledger project corda 

Blockchain | Network Types
--------------------------
Public
Private
Consortium

Database vs Blockchain
----------------------

Evolution of Blockchain
-----------------------
Blockchain 1.0: simple ledger
Blockchain 2.0: + smart contracts and logic tier
Blockchain 3.0: + cloud servicing; multilayer middleware; + cryplets (oracles)


Concepts
--------


consensus algorithm: 

blockchain is slow

5-10 transactions per second: bitcoin
1600 transactions per second: 

Avoids the "double spend" problem

You have to pay to write to the chain

Mining or "proof of work"




No PaaS for Azure Blockchain Service: it uses a template to create the farm of VMs. You have to maintain them. Just like a template can create a farm.

Everything is 

Solidity  

Smart Contract: State and code

BitCoin: 10 minute cycle
Etherium: 10 - 15 second block time


Q: How do you pay for your contract to get executed?
A: Gas.

Reduces DDoS attack. Since they have to pay.

Smart Contracts
Calling a web-service is a no-no

Solidity

Storage vs memory
storage: refers to vars stored permanetly on the blockchain.

memory: vars are temp and are reased between external function calls



DAPP: Decentralized Application Workbench

Transaction costs are based on the cost of sending data to the blockchain. There are 4 items which make up the full transaction cost:
the base cost of a transaction (21000 gas)
the cost of a contract deployment (32000 gas)
the cost for every zero byte of data or code for a transaction. 
the cost of every non-zero byte of data or code for a transaction.
Execution costs are based on the cost of computational operations which are executed as a result of the transaction. 
You can see the breakdown in the yellow paper, Appendix G.
