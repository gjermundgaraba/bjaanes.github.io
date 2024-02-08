---
title: 'The Blockchain Innovation Part 1: What is Blockchain'
date: 2017-04-27T10:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /the-blockchain-innovation-part-1-what-is-blockchain/
categories:
  - Uncategorized
redirect_from:
  - /the-blockchain-innovation/
header-img: "img/blockchain_smart_contract_bg.png"
image: "img/blockchain_smart_contract_bg.png"
---

You might not be aware, but there is an innovation revolution happening right now. It's changing the economy, business, the Internet, and could soon also change the entire world. This innovation is called blockchain.

<!--more-->

This is the first post of this series, where I will cover some of the key concepts behind the technology of blockchain and try to make it clear what it actually is and what it enables.

All three parts of this series: 

[Part 1: What is Blockchain (this post)]({{ site.baseurl }}/the-blockchain-innovation-part-1-what-is-blockchain/){:target="_blank"}  
[Part 2: What can Blockchain solve?]({{ site.baseurl }}/the-blockchain-innovation-part-2-what-can-blockchain-solve/){:target="_blank"}  
[Part 3: Exciting Blockchain Projects]({{ site.baseurl }}/the-blockchain-innovation-part-3-exciting-blockchain-projects/){:target="_blank"}  

Blockchain originated as the technology behind Bitcoin, but it is so much more. It's a ledger of information that enables trust, transparency, and decentralization of transactions and data. 
It might sound boring, but this tech might just be one of the big innovations in our time (I'm talking on the level of the Internet!).

The tricky part is understanding it.

[![Blockchain Dilbert Comic]({{ site.baseurl}}/img/posts/blockchain/blockchaindilbert.jpg)]({{ site.baseurl }}/img/posts/blockchain/blockchaindilbert.jpg)

Before starting, if you want a quick intro to Bitcoin and Blockchain (which might help), I can recommend this video by SciShow:

<iframe width="560" height="315" src="https://www.youtube.com/embed/kubGCSj5y3k" frameborder="0" allowfullscreen></iframe>

&nbsp;

# What is blockchain?

In its most abstract form, a blockchain is a distributed database or ledger. 
In simple terms, it means there is a network of people that has a full copy of the blockchain database, and everyone helps decide what goes into it, and what is the correct state of the database. 
This makes it hard to hack or take down, because it's in so many places, and there are a bunch of people controlling and making sure everybody plays nice. 
It's not just a single person or company controlling it all.

You can also use this centralized principle to store and execute code on the blockchain. The code is run by ever<yone, and the result is therefore very deterministic and safe (different results would make the network discard the transaction). 
Also, you can't take down such code, because everybody has it. These pieces of code are named smart contract and can do many many interesting things, which I will get back to later.

&nbsp;

## The Trust Protocol

The thing that makes blockchain technology so cool is the fact that it eliminates a lot of need for trust.

> “Distributed ledgers – or decentralised databases – are systems that enable parties who don’t fully trust each other to form and maintain consensus about the existence, status and evolution of a set of shared facts”
>> Richard Gendal Brown

Let me explain why that is a good thing. In business and transactions in general, there has always been the need to trust the ones you are interacting with, to know that you are not being deceived. 
This is why we have a lot of big third parties involved with things today. PayPal, Uber, Airbnb, etc. Most middlemen are there to reduce the need for trust between actors.

The interesting thing is that blockchain removes a lot of that need because trust is implicit in the platform. You can't cheat the platform. 
You can't cheat a smart contract. Code is law! This has some negative consequences as well, which I will get back to later.

[![Trust drawing]({{ site.baseurl}}/img/posts/blockchain/trust.png)]({{ site.baseurl }}/img/posts/blockchain/trust.png) 

If you want to read an article about blockchain and trust, take a look at this one from CoinDesk: [Blockchain's Big Innovation is Trust, Not Money](http://www.coindesk.com/blockchain-innovation-trust-money/){:target="_blank"}

&nbsp;

## A Chain of Blocks

As the name implies, a blockchain is a chain of blocks. Each block contains some transactions or pieces of data. Each block also includes a reference to its previous block, making it a sort of a reverse linked list. This keeps the order of the blocks in check, which is important to keep the data correct. 

[![Blockchain drawing]({{ site.baseurl}}/img/posts/blockchain/blockchain.png)]({{ site.baseurl }}/img/posts/blockchain/blockchain.png) 

Each block is encrypted with a particular algorithm, giving it a unique hash. The hash also has to follow some rules, which makes it take a long time to find a correct one. This hash is part of the security. If you try to change a block, the hash changes. And if the hash changes, then anyone linking to that block will need to change - and then you have to change every block after that. So changing data in the middle of a blockchain is a big hassle as it requires you to re-apply your cryptographic magic on each changed block (each block coming after the first changed block).
 
All of this also makes it virtually impossible to change the history of the blockchain. Nobody will accept those changes. They will not be valid, and they chain will be old and outdated before you even find the first hash.
An old chain will not be accepted by the network either; the longest chain always wins.

There is more going on with the cryptography part of blockchain and how it is secured. If you are interested, I suggest reading this excellent article: [How Does the Blockchain Work](https://medium.com/@micheledaliessi/how-does-the-blockchain-work-98c8cd01d2ae){:target="_blank"}

[![Blockchain drawing]({{ site.baseurl}}/img/posts/blockchain/block.png)]({{ site.baseurl }}/img/posts/blockchain/block.png) 

To better wrap your head around how these blocks work, I suggest this video to help visualize and understand:

<iframe width="560" height="315" src="https://www.youtube.com/embed/_160oMzblY8" frameborder="0" allowfullscreen></iframe>

&nbsp;

## A Distributed Ledger

[![Network drawing]({{ site.baseurl}}/img/posts/blockchain/network.png)]({{ site.baseurl }}/img/posts/blockchain/network.png) 

What makes blockchain shine is the fact that it's distributed. Without that, it's just a fancy technique for storing stuff and keeping track of transactions.

In this system, there are a few key players you need to know about:

1. Miners
2. Full Nodes

*Miners* are the ones that spend data power on trying to figure out the correct hash for a given new block. Once one of them find the correct hash, they give the block to the nodes.
When the block is accepted into the blockchain, the miner who got the correct hash is given a set amount of Bitcoins for their work (this happens automatically, and is the incentive created to make anybody want to mine).

*The nodes* are basically just the maintainers of the network. They keep a full copy of the blockchain, accept blocks and verify them, and passes information on to other nodes in the network.

A blockchain is said to be distributed because it's not stored in one single place. It's saved many places! A lot of people have full copies of blockchains. 
And a lot of individuals are running full blockchain nodes to verify and secure the network. All the data is in the network, not some data center controlled by a single company. 
Blockchains are owned by no one and everyone.

The fact that it's distributed is actually what makes it a trust protocol. The trust lies in the network, not just the technology. 
I mean, let's face it, nobody trust technology or people in general too much. But a network of people that are economically incentivised to enforce the truth can be trusted.
If you try to create an untruth on the blockchain, your contribution will be discarded and your chance to make any money on a block is gone.
 
You cannot simply take down a blockchain, as long as it is in use. You can't shut it down, nor control it. 
The only way to partially control a blockchain is by doing what is called a "51% attack" (by controlling more than 51% of the network) and removing already processed transactions, which is bad, but not catastrophic. Also, it's not feasible to change things too far back in the future either. It's actually pretty safe.

Learn about 51% attacks: [https://learncryptography.com/cryptocurrency/51-attack](https://learncryptography.com/cryptocurrency/51-attack){:target="_blank"}

&nbsp;

# What can blockchain do?

In the next part of this series, I explore what kind of problems you can solve with this super interesting technology:

[Part 2: What can Blockchain solve?]({{ site.baseurl }}/the-blockchain-innovation-part-2-what-can-blockchain-solve/){:target="_blank"}  
