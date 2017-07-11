---
title: 'Private Blockchains And How to Make Them Work'
date: 2017-07-11T20:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /private-blockchains-and-how-to-make-them-work/
categories:
  - Uncategorized
---

Many people are getting excited about blockchain technology, and for good reasons. Immutability, trustless sharing of data, secure transactions and much more can truly change the way we do business.

However, not everybody wants to put their data on a publicly accessible data store.
How can you have a private blockchain that is still secure and has all the great functionality of a public blockchain?

<!--more-->

If you are not too familiar with blockchain and want to learn more about the basics you can check out several articles about blockchain that I have written:

[Part 1: What is Blockchain]({{ site.baseurl }}/the-blockchain-innovation-part-1-what-is-blockchain/){:target="_blank"}  
[Part 2: What can Blockchain solve?]({{ site.baseurl }}/the-blockchain-innovation-part-2-what-can-blockchain-solve/){:target="_blank"}  
[Part 3: Exciting Blockchain Projects]({{ site.baseurl }}/the-blockchain-innovation-part-3-exciting-blockchain-projects/){:target="_blank"}  

&nbsp;

# Why private blockchains?

Why would anyone **not** want all their data open to the public and have no ability to change the data once it's out there?

That might be a slightly leading question to get my point across... Anyway, the point is that many people want the benefits of blockchain, but need to keep their data private or more tightly controlled for some reason.

Let's study a couple of use cases to understand the reasoning behind these needs better.

Property ownership is a great example.
It would be less than ideal if the government or legal system was not able to enforce changes of ownership in for instance a legal dispute. 
If the ONLY person able to change ownership is the current owner himself, even if that ownership was acquired fraudulently, then you have big problem. 
Forcing changes that override some of the current restrictions of a public blockchain are needed for use cases like this.
Perhaps we will figure out a good way to solve these issues at some point, and that is great, but for right now, a controlled blockchain is the best solution.

Another (slightly generic) use case that you might imagine is that you might want to have data that are heavily regulated regarding privacy and security on a blockchain.
You can't just slap that kind of that on a public blockchain. To share those kinds of data, a private blockchain is the only real solution right now.

&nbsp;

# Public vs. Private

When choosing between a public and private blockchain, I believe you can summarize the reasons down to this:

*Reasons for using public blockchains*
- When you need **complete** decentralization and trust
- When you need a **hack-proof** blockchain
- When you need a **censorship resistant** blockchain


*Reasons for using private blockchains*
- When you need the ability to **change or revert transactions**
- When you need to **comply with privacy regulations**
- When you have **specific requirements for speed, consensus or architecture** that doesn't play well with open blockchains

While it seems like private blockchains might be the best bet for most businesses, let's also look at some of the trade-offs you need to make.

&nbsp;

# Why a private blockchain sounds stupid

Blockchains, which are secured by openness and crowds, just private and controlled. At first glance, this seems like a tall order. 
And, to be fair, to some extent it is. BUT, it's not entirely impossible. There are however a few trade-offs and things to keep in mind.

To understand why private blockchains are not ideal let's go over some key reasons why public blockchains work so well:

- You don't have to trust anybody because the network as a whole is economically incentivised to keep all the rules
- Data can't change because the network at large, again, is economically incentivised to keep all the rules
- Because anybody can participate, anybody can contribute to the health of the network (and keep an eye on it if they want to)

Initially, it seems these reasons don't really play too well with the concept of a private blockchain. 

It is possible, however, to maintain these effects to some extent as long as there are at least a few key players in the network. 
That means that entirely private blockchains controlled by ONE single entity are not going to work. Instead, we need to aim for a middle ground here.
 
A blockchain with one single entity calling the shots is by basically just a centralized database. There is very little reason to use blockchain for this in my opinion.
As long as only one entity is in control, immutability is out of the window, as is any other extra sense of security. All you really end up with is control (which you already can get with any traditional database solution).

To reiterate one more time: If you just want a database that you can say is immutable and unhackable: private blockchains might not be the right thing for you.
You can, however, partly achieve some of these benefits with a network of trusted players, but it's not going to be a case of you swapping out your centralized Oracle or MySQL database for a blockchain.
Instead, it's going to be a case of carefully designing your system.
 
To continue this discussion, we need to define how a private blockchain needs to actually work. And to do that, we need to look take a close look a public blockchains.

&nbsp;

# Private vs. Public Blockchains

Let's define what a private and public blockchain is.

There are three primary levels of how private a blockchain is:

- Fully Public
- Consortium
- Fully Private

For a *fully public blockchain*, there is no access control built into the protocol itself; anyone can contribute as a user or as a working part of the network (e.g. validating transactions or mining).

A *consortium blockchain* has some access control that at least controls who own the consensus of the network. That means that a set of specific nodes controls the entire network and all transactions happening on it (validating transactions).
The level of access to read and write can by any level from no access outside the network to read-only or even open to read/write (but still having the owner nodes clearing all transactions).
This level of privacy is where we can design ourselfs a network that reaps the most benefits. 

A *fully private blockchain* is the one that I would call a fully centralized database. There is one entity controlling the entire network. 
This might seem like it's pretty far from the original Bitcoin vision - and that's because it is. 
Essentially, you are using the ledger technology from blockchain, but not much else. I don't see any reason for doing this. Just use a simple database technology. It's going to be much cheaper.

In other words, a private blockchain (vs. a public one) is just a blockchain that has some level of access control on it. It can still be distributed and even open to the public.

The kind of blockchain we need to get any value from a private blockchain then is a *consortium blockchain*. We need a blockchain that is **at least** distributed to more than one player.
It all depends on the use case, but the more players you have in your network, the more benefits you will get.

&nbsp;

# How to secure a private blockchain

One of the biggest reasons I wanted to learn about private blockchains in the first place was because I was curios how it could ever be secured. 
I mean, the biggest reason public blockchains are safe is that they are distributed, open and economically incentivised to be kept safe. If anyone tries to do something "bad," it will just be rejected by the network.
It's just the consensus part of the protocol.

It turns out, this consensus part of blockchains is also what is securing private blockchains, although on a slightly different level. 
They not secured because you have an enormous amount of people validating some mathematical piece of work (and being paid to do so). 
Instead, it's secured by the fact that the players that are allowed on the network are trusted by those that "matter." 
What I mean by that is that to be allowed the privilege to verify the blockchain, you have to be trusted in the first place, or you would not be handed the privileges. 
The only thing you need to be able to validate and contribute is to prove that you are who you say you are and that you have access to do so. 
Compared to an open blockchain where anyone has the privilege to participate, it works out quite nicely.

In other words, the security of a private blockchain is provided by the network it is in. Just like a public blockchain.
You just have to keep in mind that you need to design your network carefully. 

An excellent article from Harvard Business Review on this subject talks a lot about the design of private blockchains:
[https://hbr.org/2017/03/how-safe-are-blockchains-it-depends](https://hbr.org/2017/03/how-safe-are-blockchains-it-depends){:target="_blank"}

I will say, however, that this security is still slightly flawed compared to that of a big public open blockchain. 
If a sufficient amount of players in the private blockchain turn bad, they could easily corrupt the network. 

And, again, as I mentioned at the beginning, this is mainly looking at consortium blockchains (partially private blockchains). 
Fully private blockchains which are controlled by a single entity has only the security of that single entity. 
In other words, no better security than any other centralized service.

&nbsp;

# The counter-point from the idealists

So, it seems like private blockchains (or at least partially private permissioned ones) have some uses. 
I would, however, like to invite the idealists into the discussion on this, because I think they have some good points.

Andreas M. Antonopoulos, also called Mr. Bitcoin, recently (at Oslo Blockchain Day 2017) said that he views public vs. private blockchains as the same thing as internet vs. intranet. 
He said something along the lines of (not a direct quote): "When was the last time you saw something interesting on an intranet? Compared to the internet, intranets are not very interesting".

The following is, however, a quote I found in [bitcoinmagazine](https://hbr.org/2017/03/how-safe-are-blockchains-it-depends){:target="_blank"} that summarizes his viewpoint:

> “Not only is decentralization, open protocols, open source, collaborative development and living in the wild a feature of Bitcoin, that’s the whole point. And if you take a permissioned ledger and say, that’s all nice, we like the database part of it, can we have it without the open decentralized P2P [peer-to-peer] open source non-controlled distributed nature of it, well you just threw out the baby with the bathwater.”

&nbsp;

# The reason private blockchains are useful (right now)

While Andreas brings up some excellent reasons for blockchains to be open and public, I think the need for private blockchains are real. At least right now.

We have gone over the need for private blockchains. We need the benefits of blockchains, but we can't turn all data public, and not all data can be 100% immutable.

Vitalik Buterin, co-founder/creator of Ethereum said on the [Ethereum Blog](https://blog.ethereum.org/2015/08/07/on-public-and-private-blockchains/){:target="_blank"}

> “The consortium or company running a private blockchain can easily, if desired, change the rules of a blockchain, revert transactions, modify balances, etc. In some cases, e.g. national land registries, this functionality is necessary; there is no way a system would be allowed to exist where Dread Pirate Roberts can have legal ownership rights over a plainly visible piece of land, and so an attempt to create a government-uncontrollable land registry would in practice quickly devolve into one that is not recognized by the government itself….
“Given all of this, it may seem like private blockchains are unquestionably a better choice for institutions. However, even in an institutional context, public blockchains still have a lot of value, and, in fact, this value lies to a substantial degree in the philosophical virtues that advocates of public blockchains have been promoting all along, among the chief of which are freedom, neutrality and openness.”

&nbsp;

# The future of private blockchains

We have established in this post (if you agree me) that private blockchains are useful and could bring some real benefits to many use cases today.
We have also looked at how public blockchains are superior in many aspects and have some real benefits that private blockchains can never obtain.

I believe that in the future, most blockchains will, in fact, be public. The reason I believe this is because private blockchains are useful, *but they are not revolutionary. Public blockchains ARE!*

For now, please use private blockchains, but don't forget about the open public and revolutionary blockchains - or you might get left behind.