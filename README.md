# blockchain
Learn about blockchain, distributed systems, and multithreaded programming through this blockchain simulation project.

<h2>What is a blockchain?</h2>
Blockchain refers to the "ledger" that is kept of every crypto transaction. What's interesting about it is that the ledger is formed by all the people who make transactions, and there is no governing system that keeps track of it all. This is why everyone refers to crypto as decentralized, because users themselves create the coins and keep track of sales. If you want to get a better idea of blockchain and how it works, I suggest taking a look at this link (https://medium.com/crypto-currently/lets-build-the-tiniest-blockchain-e70965a248b), it's what I base a lot of the code on and helped me to come up with this project. 

<h2>How can we make a decentralized system?</h2>
We want our blockchain simulation to behave as if multiple users on different computers are making transactions with eachother, but how can we do so on just one computer? This is where multithreaded programs and TCP sockets come in. When you write code, you can think of it as one thread where the computer reads through each line and carries out the action described in it until it reaches the end of the program. However, if you wanted to have multiple programs running at once, threads are a perfect solution, as they run independently of each other and do not need to wait to carry out their functions. For the sake of this project, we will use different threads to represent different users of our coin. For threading syntax and more information, check out the "Threading" section of this article! https://eecs485staff.github.io/p4-mapreduce/threads-sockets.html 

But if they are running completely independently of one another, how can they communicate and make transactions? This is where we will use sockets. Sockets are used to send and listen for signals sent over the internet. There are different types of sockets, but for this project we will be using TCP servers and clients, where a server is used to listen for incoming messages, and a client is used to send them out. The starter files already include the code for running TCP servers and clients, but you can find more information on how them in the link above under the "Sockets" section.



