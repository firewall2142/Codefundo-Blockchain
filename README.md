Complete guide to Conducting Elections using Azure Blockchain
=============================================================

Our model of a blockchain election satisfies the following:

* Its easy to check if particular person has voted
* Impossible to say that a person voted for a particular candidate
* Only Election Commissioner can tell which person voted for which candidate

Voter's Perspective
-------------------

1. Voter has to apply online for voterID with aadhaar card and specify the polling booth for casting vote.
2. Voter will receive a mnemonic of 10 words.
3. On the day of election, voters will have to go to their polling booth, get fingerprint/iris scan verified and enter the mnemonic to vote.

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


In our idea for election, every vote is a transaction from the ethereum wallet of the voter (created automatically after applying for voter ID) to the election wallet (election wallet is same for every transaction). Every wallet will have sufficient funds for fast transaction. The transaction's data field specifies the candidate voted for, this is salted and encrypted using RSA and the key(1)(private key used to decrypt RSA)  is with EC. The transaction is signed by both the voter and the EVM using their private keys (ECDSA algorithm).

The mnemonic+hash(voter's name) is used as a seed to generate a private key of the voter.

The EVM's code is permanently "burned" into the EVM.

EVM's private keys are encrypted using RSA and the "password" is communicated just before the opening of booth.

The EC, will run a program which reads the database and the transactions with the election wallet, and will monitor the election for activities like double voting, people voting from the wrong booth etc. in real-time.

When the voting process is over, the EC will run another program to count the votes which uses key(1) for decryption.

Pros of our idea
----------------

* In regions without internet, the voter will get an app(which simulates a EVM) during voterID registration. The decryption key is sent in a letter to the voter. Then the voter will enter decryption key, his mnemonic, name, candidate in the app. The app generates a transaction which is copied to a postcard & mailed back to EC. 
* Real-time monitoring of election
* High Security: Creating a fake vote requires access to many levels
* You have the freedom to choose any booth

![Flow Diagram](codefundo-min.png)
