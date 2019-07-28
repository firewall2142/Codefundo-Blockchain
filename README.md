Complete guide to Conducting Elections using Ethereum
=====================================================

Our model of a blockchain election satifies the following:

* Its easy to check that a particular person has voted
* Impossible to say that a person voted for a particular candidate
* Only the Election Commisioner can tell which person voted for which candidate
* Each EVM has a unique encrpyted key, which will be decrypted with a password. The password is communicated at the time of opening of polling booth. The EVMs are useless without the password and the password is usless without the EVM

Voter's Perspective
--------------------

1. The voter has to apply for a voterID online with aadhar card and specify the polling booth to cast the vote.
2. The voter will receive a mnemonic of 10 words.
3. On the day of election, the voter will have to go to his/her polling booth, get their fingerprint/iris scan verified and use mnemonic to cast their vote.

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

3. The password to activate the EVM is communicated (via Phone, email etc...) to the polling booth head half to one hour before the election begins.
4. During voting the EC can check for double voting, voter going to a poll booth other than the alloted one etc..
5. After the voting process is over. The EC counts the number of votes by checking transactions on Ethereum network.


Technical Perspective
---------------------
