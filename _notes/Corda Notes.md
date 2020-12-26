Corda Key Concepts on Lessonly: https://r3.lessonly.com/path/5150-corda-key-concepts/login?view=signu
Corda Developer Training:  https://www.udemy.com/corda-development/ 
Corda Documentation:  https://docs.corda.net/ 
Corda Certification: https://corda-certification.myshopify.com/products/corda-standard-certification-test

Network
-------
The Corda network is best represented as a fully-connected graph containing nodes.
There is no global broadcast or gossip network on Corda.
Corda nodes discover each other via a network map service. 
Each Corda node includes a vault, and every vault contains facts.
These facts can be shared with other nodes on the network.
The Corda Ledger is subjective from each peer's perspective.

Transactions
------------
Key takeaway:
Transactions are an atomic set of changes to update the ledger.
Transactions are committed and update the ledger only when signed by all required peers.
Uncommitted transactions are proposals to update the ledger.
Committed transactions enforce output state immutability because they are digitally signed.
Once a transaction is committed, it marks the input state references as historic and creates new output states reflecting an updated ledger.
Transactions are not instructions which require action. 

Transaction proposals require verification which is performed separately to transaction creation.

Differences Between Ethereum and Fabric
+ Ethereum (smart contract) and Fabric (chaincode) all execute same contract code and compare results
+ Corda has one party propose (transaction proposer) new state and rest; it is distributed to peers and they perform verfication using the contract code; so two parts: proposal and verfication

Transaction components
A transaction consists of six types of components:
1+ states:
0+ input states
0+ output states
0+ reference input states
1+ commands
0+ attachments
0 or 1 time-window
A transaction with a time-window must also have a notary

Contracts
---------
Key takeaways:
Each state must reference a contract.
A contract contains contract code and legal prose. 
Contract code is used to verify transactions.
Contract code is a "pure" function executed in a deterministic environment on a need-to-know basis.

Legal Prose
-----------
Whilst the contract code is a powerful means to verify transactions, it cannot handle all real-world events like complex disputes, fraud and arbitration. In such events, we need to defer to existing judicial system to resolve them. 

Key takeaways:
Legal prose is referenced within contracts.
Legal prose can be relied upon when the contract code alone is insufficient.

Commands
--------
What are commands?
Commands are verbs. They parameterise transactions, providing more information than is obtainable from only the states. Commands also hint to the intention of a transaction. Commands may also contain arbitrary data signed over by an Oracle service.

More examples of commands:
Issue a new state on the ledger
Transfer the asset to another peer on the ledger
Pay some cash to another peer on the ledger
Redeem an asset and extinguish the state representing it
Exercise an option
Settle an obligation to deliver an asset
Net a set of fungible obligations

Key takeaway:
Commands parameterize transactions.
Commands hint the intent of the transaction.
Commands specify the required signers via a list of public keys.

Time Windows
------------
Before a specific time
After a specific time
Between specific points of time

Time tolerance - e.g. 30 seconds window. Allows for network latency and how long you think it will take to get signed

Key takeaways:
Time windows assert that a transaction happened before, after, or within a specified time range.
Time windows can be used to enforce contractual logic.
The notary acts as a time window authority.

Attachments
-----------
Are zip files and identified by the hash in bytes. Transactions can also contain a number of transactions.

Attachments may contain:
Data files which support the contract code e.g. currency definitions, public holiday calendars or financial data
Contract code and associated state definitions (.class files)*
Legal prose template and parameters*

States can place restrictions on what attachments are willing to accept. signed or hashed.

Attachments provide data but do not authenticate it. It's done by contract code verifying certs or hashes. Imposes size limits.

Key takeaways:
Attachments are zip files.
Attachments are referenced in a transaction by hash value.
Attachments are not included in the transaction itself.

Flows
-----
Flows are designed to facilitate multi-party and multi-step coordination to reach consensus on a shared fact. To do so, flows control:
When to communicate
What to communicate
With whom to communicate

Most DLT (Distributed Ledger Technology) platforms use forecasting and gossip networks, in which data is simply messaged to other nodes. The disadvantage of this approach, however, is that peers cannot control who receives their data. This component is largely inconsistent with the needs of most financial institutions.

Fully autonomous: require no human interaction; may only take seconds

In-progress flows must also be able to survive node reboots, when nodes undergo node maintenance.

Activity vs. Sleep
-----------------
Flows sleep most of the time
Awaken by IO or a message on the network

Then, the flow might wait a long period of time for a response. 

Flows
Paired or one sided
Paired: initiator and receiver

check-points
while waiting for responses from peers (the flows are "asleep"). State is suspended and serialized to storage.

Code never blocks

How?
Fx called Quasar rewrites code behind scenes, transforming a asynchronous state machine into asynchronous state machine so developer doesn't have to
+ Since not in memory, can have millions of flows in progress

Sub-flows
---------
Commonly/reused flows; packaged as sub-flows. How? flow library

Some examples of sub-flows:
Atomic asset swaps
Broadcasting data to multiple peers
Sending cash
Agreeing on multi-lateral deals

APIs
----
Send and receive data to and from other peers on the network
Create transactions
Verify and sign transactions
Embed subflows
Report progress information to observers
Interact with the node, its services, and its users


 
Concensus
---------
Types of Consensus
Corda supports two types of consensus: 
1. verification consensus, which determines whether an update to the ledger is valid 
2. uniqueness consensus, which determines if a ledger update is unique, or if it has been used before (e.g. has the update attempted to double spend another state on the ledger?)

Understanding Verification Consensus
* has been signed by all of the peers listed in the commands
* satisfies the constraints defined by the contracts pointed to by the input / output states

Lazy Propagation
If you are a party on a Corda network, and you are presented with transactions containing input states that are fungible issued assets-on-ledger, you need to verify all previous transactions concerning those states.
Bob Owes Alice £10 - A Lazy Propagation Example

Understanding Uniqueness Consensus
How is uniqueness consensus implemented?
Uniqueness consensus requires peers to agree that the output states created in a transaction are the unique successors to the input states referenced by that transaction

Consensus Summary

Why is uniqueness consensus used?
To ensure that an input state has not been previously used and marked as historic (i.e. prevent a "double spend").

Notaries
--------
In addition, we need a signature from the notary service. 
Notaries are typically specified for each input state, and are required for the transaction to be considered committed. This is known as notarization. 
In short, the point of finality is reached once the notary service signs the transaction. 

However, there are exceptions...

If a transaction has:
no input states, or
no timestamps
then the "uniqueness" of those properties cannot clearly be confirmed nor denied. 
So, we only need a notary signature when there are input states and/or timestamps.

To reiterate, finality only occurs for transactions where the output states are the unique successors for all referenced input states. 
If any of the input states are already historic states, the notary will refuse to sign the transaction, and the transaction will not be completed.

Non-verifying notaries...
Only check to see if the input state references are already historic or not
Do not perform verification over transactions
Therefore, they do not need to see the contents of state objects

Oracles
-------
You can communicate with an Oracle:
To attest over a fact you have already inserted into the transaction
Request that the Oracle provide the fact and attest to it as well

Note: There can be many external facts required in a transaction and you CAN use Multiple Oracles per transaction.

Oracles will likely provide the facts when creating transaction proposals, whilst also attesting to those facts during verification.

How it works
When you need to include an off-ledger fact in the verification of a transaction, you can provide a command where:
That fact is incorporated into that command inside the transaction itself
The fact can be established independently or by querying an Oracle service that provides facts
At this point, the Oracle's public key is added to the command's signers list and the Oracle becomes a co-signer to the transaction.

Now that you know two ways to implement Oracles, let's compare them.
Commands
Use for small or regularly changing data
Suitable where there is commercial sensitivity due to licensing
Attachments
Use for large data, particularly if it does not change regularly
Not suitable for licensed facts

Nodes
-----
Break Down of Corda Nodes
Corda nodes run within a Java virtual machine. In brief, processing involves: 
Storage services and vaults backed by a SQL DB 
Attachments stored separately in a dedicated folder 
RPC client framework and server shell for communication amongst network nodes
Built-in extensions or custom functionality called CorDapps

Defined Services
Notice the ServiceHub internal contains references to the following service features: 
Vault: stores output states relevant to a particular node  
Transaction storage: key value store for attachments, transactions, and serialized state machines (SSM) 
Flow State Machine Manager: manages operation of flow state machines 
Identity/Key Management: manages various supported identities and generated keys used to sign transactions
Scheduler: schedules operations for future points in time
Network Map:  searchable phone book of nodes on network 
Notary: obtains authorized signatures 
Messaging: interface with other nodes for communication 

Custom Functionality
The PlugIn Registries keeps track of custom functionality. 

Component Interactions
Remember that flow contains all the business logic required to access nodes services and create/verify transactions so anything in Corda must pass through. 
We typically build transaction via first steps of the flow after receiving signature of the counterpart. Once all required steps are performed such as checking the signature, the transaction is sent to notary services for signing to achieve finality. 
After the signature is attached to the transaction, record is placed in TX storage to indicate shared consensus. Both parties participating in this flow will have an identical copy of the output states in their vaults. 
Once in a vault, a state can be extracted via query and displaced in a user interface. 

Summary

Network
-------
Break Down of Corda Nodes
The Corda Network consists of the following elements: 
Nodes that communicate using AMQP/1.0 over Transport Layer Security 
A permissioning service or "doorman" that automates the process of provisioning TLS certificates 
Communication with other nodes requires certificate placement in nodes folder
A network map service that publishes information about nodes on the network 
If the map goes down, new nodes are prevented from joining the network BUT all nodes maintain a local cache of other known nodes that can be relied upon
One or more notary services
Zero or more oracle services 

A Compatibility Zone (CZ) is a private network of nodes that is able to transact using the Corda platform.

Permissioning Service
This permissioning service is required on Corda because Corda is designed for semi-private networks.
As such, it is expected that for an entity to participate, that entity would sign a network agreement and obtain a certificate from a root authority: the permissioning service.
Certificate signing requests are reviewed by an R3 team.
R3 acts as the root certificate authority (CA) for the "testnet."
Once a node has a certificate, it can then communicate with other nodes on the network. Without certification, communication is impossible.

Network Map Service
Essentially, the network map service is a list of all the nodes on the network.
As nodes join or leave the network, the service publishes their data: IP addresses through which every peer can be reached, as well as the identity.
The network map is distributed to all peers on the network.
If the network map services goes down, the only thing that this prevents is other nodes joining the network. (This is because all nodes maintain a cache of all other nodes that they know about on the network.) 

Summary