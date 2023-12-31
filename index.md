---
layout: spec
latex: true
mermaid: true
---

Cantor P3: Blockchain Simultation
======================

## What is a blockchain?
Blockchain refers to the "ledger" that is kept of every crypto transaction. What's interesting about it is that the ledger is formed by all the people who make transactions, and there is no governing system that keeps track of it all. This is why everyone refers to crypto as decentralized, because users themselves create the coins and keep track of sales. If you want to get a better idea of blockchain and how it works, take a look [here](https://medium.com/crypto-currently/lets-build-the-tiniest-blockchain-e70965a248b), it's what a lot of the code is based on. 

## How can we make a decentralized system?
We want our blockchain simulation to behave as if multiple users on different computers are making transactions with eachother, but how can we do so on just one computer? This is where multithreaded programs and TCP sockets come in. When you write code, you can think of it as one thread where the computer reads through each line and carries out the action described in it until it reaches the end of the program. However, if you wanted to have multiple programs running at once, threads are a perfect solution, as they run independently of each other and do not need to wait to carry out their functions. For the sake of this project, we will use different threads to represent different users of our cryptocurrency. For threading syntax and more information, check out the "Threading" section of [this article](https://eecs485staff.github.io/p4-mapreduce/threads-sockets.html)!  

But if they are running completely independently of one another, how can they communicate and make transactions? This is where we will use sockets. Sockets are used to send and listen for signals sent over the internet. There are different types of sockets, but for this project we will be using TCP servers and clients, where a server is used to listen for incoming messages, and a client is used to send them out. The starter files already include the code for running TCP servers and clients, but you can find more information on them in the link above under the "Sockets" section.

## Project overview
Here is a brief rundown of how the project should work. Upon running the code you are prompted with the ability to create a user, make a transaction, or see all the current chains of every user. When a new user is created, two threads should be started, one which runs the mining function, and one which runs the TCP_server function to listen for incoming messages. If you're creating the first user, a genesis block should be created using the create_genesis_block function. Otherwise, the new user should check all of the existing user's blockchains and make the longest one its own blockchain. It will then begin mining coins in the background. 

If a transaction is requested, it will ask for two users and an amount to be given (in this project transactions are just one user awarding coins to another). Then part of the seller's balance will be transferred to the buyer. For any newly mined coin or transaction, the user who mined the coin or the buyer must mint a block using the previous block's (from its own chain) hash, the current timestamp, and the transaction data (for a mined coin it is from "network"). The buyer/miner will then use a TCP client to send all the new block's criteria to every other user in the system, who upon recieving it will run the handle_msg function, which will mine a new block with the new transaction onto their own chains. 

The finished code is contained in the solution folder. If you want to run it , simply type <code>python3 solution/blockchain.py</code> in your terminal to see how the code runs. You can also take a look at the solution if you are really stumped, but I would encourage you to try and figure it out yourself. If you have any questions feel free to reach out!

## Todo list
- [ ] Block class
  - [ ] <code>init</code>
  - [ ] <code>hash_block</code>
- [ ] User class
  - [ ] <code>init</code>
  - [ ] <code>mine</code>
  - [ ] <code>handle_msg</code>
- [ ] <code>transaction</code>
- [ ] <code>main</code>


## More details
### Running
To run the scripts, you need to have python3 installed. You can do so using homebrew and running <code>brew install python3</code>. If you don't have homebrew installed, you can do so [here](https://brew.sh/).

### <code>hash_block</code>
This function is used to create a hash using all the block's information that is passed into the init function, including the previous block's hash. A hash can essentially be thought of as a large string that is used to identify blocks. Look into the python hashlib library to see how to create hashes.

### Global vars
- users: a dictionary with key of user name and value of the user class itself
- signals: a dictionary containing the value of shutdown and genesis. Shutdown becomes true when the program is terminated, and genesis becomes true after the creation of the genesis block

