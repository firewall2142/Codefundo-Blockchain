Complete guide to Conducting Elections using Azure Blockchain
=============================================================

Our model of a blockchain election satisfies the following:

* Its easy to check that a particular person has voted
* Impossible to say that a person voted for a particular candidate
* Only the Election Commissioner can tell which person voted for which candidate

Voter's Perspective
-------------------

1. The voter has to apply for a voterID online with aadhaar card and specify the polling booth to cast the vote.
2. The voter will receive a mnemonic of 10 words.
3. On the day of election, the voter will have to go to his/her polling booth, get their fingerprint/iris scan verified (to get permission to use EVM) and enter their mnemonic to cast their vote.

Election Commision's Perspective
--------------------------------

1. EC has to produce EVMs. Every EVM has a different encrypted private keys.
EC stores the following things about EVMs in a secure database:
    * Public Key
    * EVM's polling booth
    * EVM's private key decryption password

2. During online registration of voters. The EC stores the following in a secure database:
    * voter's name 
    * voter's public key
    * voter's polling booth/alloted EVM
    * Aadhar link/ biometric data

3. The password to activate the EVM is communicated (via Phone, email etc...) to the polling booth in-charge before the voting begins.
4. During voting the EC can check for double voting, voter going to a poll booth other than the allotted one etc..
5. After the voting process is over. The EC counts the number of votes by checking transactions on Ethereum network.


Technical Details
-----------------


In our idea for election, every vote is a transaction from the ethereum wallet of the voter (created automatically when applying for voter ID) to the election contract. The transaction's data field specifies the candidate voted for, this is salted and encrypted using RSA and the key(1)(private key used to decrypt RSA)  is with EC. The transaction is signed by both the voter and the EVM using their private keys (ECDSA algorithm).

The mnemonic+hash(voter's name) is used as a seed to generate a private key of the voter.

The EVM's code is permanently "burned" into the EVM so that it cannot be changed.

EVM's private keys are encrypted using RSA and the "password" is communicated just before the opening of the polling booth.

The EC, will run a program which reads the database and the transactions with the contract, and will monitor the election for things like double voting, people voting from the wrong booth etc. in real-time.

When the voting process is over, the EC will run another program to count the votes which uses key(1) for decryption

Pros of our idea
----------------

* EVMs are flexible. For extremely remote regions, the person can register for voter ID online. EVM can be a mobile app, whose private key is communicated, instead of taking the whole EVM to the remote place.
* Real-time monitoring of election
* High Security: Creating a fake vote requires access to many levels
* You have the freedom to choose any polling booth
