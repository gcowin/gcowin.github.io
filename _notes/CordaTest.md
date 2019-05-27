

Question
Given Answer
Correct Answer


What does a State in Corda represent?
A fact known by one or more parties
A fact known by one or more parties


States must be shared between at least two participants.
True
* False


Fields of any ContractState are stored in separate database columns when persisted. It is possible to run any kind of SQL-like queries against these states.
False
False


From the above code block: which participants will store the state after it gets committed to the ledger?
partyA and partyB
* partyA


What type of on-ledger facts should be represented using OwnableState?
Fungible asset, owned by a single party, which can be split and merged with other states of the same type.
Fungible asset, owned by a single party, which can be split and merged with other states of the same type.


What interface allows states to start a flow at a certain future point in time?
SchedulableState
SchedulableState


What field(s) does the LinearState interface define?
linearId
linearId


Where does each node store their states?
Vault
Vault


What does a Contract in Corda represent?
The sets of constraints that govern the evolution of state objects.
The sets of constraints that govern the evolution of state objects.


How does a transaction uniquely identify the contracts to use to verify a transaction?
Hash of the JAR file containing the contract and the fully qualified contract class name.
Hash of the JAR file containing the contract and the fully qualified contract class name.


It is possible to allow non-deterministic Java libraries, such as DateTime, to be used in Contracts if to fulfill business logic.
False
False


Contracts are included in attachments in Corda.
True
True


What does a Contract.verify method return?
Void/Unit
Void/Unit


What does a Transaction in Corda represent?
A proposal for a number of participants to update their ledgers.
A proposal for a number of participants to update their ledgers.


How are transactions consuming or creating multiple state objects processed?
All state changes must be valid. Any invalid state transition will result in a failed transaction.
All state changes must be valid. Any invalid state transition will result in a failed transaction.


For performance reasons, the number of participants in a transaction is limited to:
not limited
not limited


A transaction accepts ______ input states.
0 or more
0 or more


What is the purpose of filtering a transaction?
Finding the outputs of a transaction that are relevant to my node
Hiding certain components of the transaction from users who do not need to see them


A transaction cannot be distributed to all participants of a Corda Network.
False
False


Contract verify is the only code run when verifying a transaction.
False
True


A notary is optional within a TransactionBuilder prior to signing the TransactionBuilder.
False
False


At which point(s) is a Transaction verifiable?
All the above.
All the above.


In what form does a TransactionBuilder hold inputs and outputs?
StateRef/TransactionState
StateRef/TransactionState


What class does a transaction become after it has been signed?
SignedTransaction
SignedTransaction


Why does a transaction have to be resolved to a LedgerTransaction before being verified?
The inputs must be converted from state references into state objects, the attachments must be converted from hashes into actual attachments, and the TimeWindow must be converted into the node's local time
The inputs must be converted from state references into state objects and the attachments must be converted from hashes into actual attachments


How is the hash of a transaction calculated?
It is the root hash of the transaction's Merkle tree
It is the root hash of the transaction's Merkle tree


What is included in a StateRef to uniquely pinpoint which input state(s) a transaction is spending?
The hash of the transaction that created the state and the state's index in the outputs of that transaction
The hash of the transaction that created the state and the state's index in the outputs of that transaction


Why can't a transaction's signatures be checked for validity from within a contract's verify method?
One or more signatures may not yet have been added to the transaction
The signatures are not included in the transaction being verified


What role does a command play inside a Transaction?
A hint on the intent of a Transaction and public keys required to sign the transaction.
A hint on the intent of a Transaction and public keys required to sign the transaction.


Commands are optional in Corda transactions. 
False
False


How are the required signers of a transaction decided?
Based on the signers listed on the commands
Based on the signers listed on the commands


Which guarantees are provided by Flow framework in Corda?
Flows are abstractions over messaging operations only. Developers need to checkpoint and restore flows by themselves.
Flows guarantee eventual finality.


How long can flows remain in a suspended state?
Indefinitely
Indefinitely


sendAndReceive() method takes a timeout as one of its optional arguments.
False
False


The Party which initiates a Flow is responsible for creating the output States that are the proposed changes to the ledger.
True
False


Which of the following about anonymous-to-wellknown party mappings is true?
Anonymous-to-wellknown party mappings are resolved as a part of IdentitySyncFlow 
Anonymous-to-wellknown party mappings are resolved as a part of IdentitySyncFlow 


Which Corda key concept should the TransactionBuilder used in?
Flow
Flow


What pre-defined flow is used to notarise a transaction and record it in every participant/owner's vault?
FinalityFlow
FinalityFlow


What annotation is used to specify which initiator flow a response flow responds to?
InitiatingFlow
InitiatedBy


What happens if your node receives a message from a flow for which it has not registered a response flow?
It ignores the message
It ignores the message


When would you wrap an exception in a flow within a FlowException instance?
When you want the exception to be propagated back to the node that is suspended and waiting for your flow to respond because of a send or receive call
When you want the exception to be propagated back to the node that is suspended and waiting for your flow to respond because of a send or receive call


How is a state's notary changed once the state has been issued?
The node can change a states's notary using the NotaryChangeFlow
The node can change a states's notary using the NotaryChangeFlow


Time may be specified for which of the following ranges:
All of the above
All of the above


How can a contract ensure that a transaction is only valid if it is fully signed before time X?
By adding a TimeWindow to the Transaction and getting the Notary to sign the Transaction within that TimeWindow.
By adding a TimeWindow to the Transaction and getting the Notary to sign the Transaction within that TimeWindow.


Attachments are intended to be reused across transactions
True
True


What format are attachments stored in?
JAR files
JAR files


By default, when a node records a transaction, which objects does it store in its vault.When a node sees an attachment how does it resolve the attachment?
By downloading the attachment from the network map.
By retrieving the attachment from its own storage or requests it from the counterparty.


How is information shared in Corda?
On a peer-to-peer basis
On a peer-to-peer basis


Any participant can join Corda network as long as they get accepted by the majority of the members.
False
False


Corda nodes communicate via:
AMQP 
AMQP 


What requirements for connectivity are needed for node connectivity?
None of the above.
If a node goes offline messages will be retried until the remote node has acknowledged the message.


How do nodes look up information about other nodes on the network?
The network map
The network map


The name and certificate of a "Confidential identity" is never revealed to any other nodes in the network.
False
False


What is the name of the certificate with which a node is able to verify the identity of the owner of a public key?
X509
X509


Corda Nodes run in a JVM.
True
True


Where does each node store their states?
Vault
Vault


Which of the following statements about Corda data backup is true?
Data does need to be backed up: each participant must back up their own data. 
Data does need to be backed up: each participant must back up their own data. 


How is a CorDapp installed on a node?
By placing it in the node's CorDapps folder
By placing it in the node's CorDapps folder


Each node receives a full copy of the Transaction history during verification.
False
True


How does Corda ensure each output state is only consumed once?
Each Notary maintains a list of state refs that have already been consumed.
Each Notary maintains a list of state refs that have already been consumed.


Which of the following types of verification must go in the flow?
Checking that the signatures on the Transaction are valid.
Checking that the signatures on the Transaction are valid.


Transactions can have inputs assigned to different Notaries.
True
False


The entire historical chain must be walked backward for any kind of transaction verification.
False
False


How many notaries can co-exist on the same network?
Many
Many


When is a notary NOT required to notarize a transaction?
All transactions are notarised
When the transaction has no input states and no timewindow


Which parts of a transaction does a non-validating notary see when signing a transaction?
The input state references
The input state references, the TimeWindow, and the transaction's notary


What service does an Oracle provide to a Corda Network?
Signs Transactions which include data external to the ledger.
Provides data external to the ledger into a Transaction and signs the Transaction.


What type of information might an oracle provide to a transaction?
All of the above.
All of the above.


Oracle services can be used both when building and when verifying transactions.
True
True


What is used to encrypt communications between nodes?
TLS
TLS


It's a good practice to bundle all flows, contracts and states into the same CorDapp, as it makes it easier to distribute the CorDapp to other parties.
False
False


Which of the following about serialization in Corda is true?
Third party classes have to be explicitly added to the serialization whitelist in order to be sent over the network
Third party classes have to be explicitly added to the serialization whitelist in order to be sent over the network


What annotation marks a class as being eligible to be sent and received between nodes as part of a flow?
CordaSerializable
CordaSerializable


How would you rate your overall experience with Corda Developer Certification?
6
N/A


If you didn't pass the exam at this time do you plan on taking it again?
Yes
N/A


What was the most challenging aspect(s) of the certification exam?
No answer was given
N/A


What aspect(s) of certification were not clear?
No answer was given
N/A


Any other feedback that you'd like to give the R3 team?
No answer was given
N/A