---
title: 'The Blockchain Innovation Part 2: What can Blockchain solve'
date: 2017-04-27T10:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /the-blockchain-innovation-part-2-what-can-blockchain-solve/
categories:
  - Uncategorized
header-img: "img/blockchain_smart_contract_bg.png"
image: "img/blockchain_smart_contract_bg.png"
---

You might not be aware, but there is an innovation revolution happening right now. It's changing the economy, business, the Internet, and could soon also change the entire world. This innovation is called blockchain.

This post is all about what kind of problems that Blockchain can solve.

<!--more-->

All three parts of this series: 

[Part 1: What is Blockchain]({{ site.baseurl }}/the-blockchain-innovation-part-1-what-is-blockchain/){:target="_blank"}  
[Part 2: What can Blockchain solve? (this post)]({{ site.baseurl }}/the-blockchain-innovation-part-2-what-can-blockchain-solve/){:target="_blank"}  
[Part 3: Exciting Blockchain Projects]({{ site.baseurl }}/the-blockchain-innovation-part-3-exciting-blockchain-projects/){:target="_blank"}  

# What can blockchain do?

The most important aspects of blockchain is the fact that it is decentralized secure, and how it negates the need for a lot of trust. Today we often use third parties to solve the problem of trust.

Blockchain can help remove uncertainty in all kinds of dealings. You can bring forth a new form of transparency and traceability that would otherwise be impossible. Blockchain can guarantee these things. If you are interested in a short video on how you can envision the new economy with blockchain, take a look here:
 
<iframe src="https://embed.ted.com/talks/bettina_warburg_how_the_blockchain_will_radically_transform_the_economy" width="640" height="360" frameborder="0" scrolling="no" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
 
&nbsp;

## Currency

The most common use case for blockchain right now is currency. Bitcoin was the one who introduced blockchain after all. 
 
But, why would you want something different than today's currencies? Today, currencies are centralized and controlled. You need to work with, trust and pay centralized banks to handle your money. Some of the problems with this is:


1. It's expensive. There are a lot of fees
    - International money transfer can be expensive and slow
2. Trust
    - You have no choice but to trust your banks. They could, in theory, misplace all your money. You don't have any control.
    - You have to trust a middleman when wiring your money around, instead of sending it directly to the receiver.
3. Not everyone can/want to work with a bank
    - Some people can't afford to use banks because they make too little money and the banks are too expensive (quite common in developing countries)
    - Some people don't have access to banks because the banks just don't bother to establish themselves there, or people are unable to get themselves to where the banks are.
    - Some people aren't trusted by banks (refugees without ID might have a problem for instance)

[![Money Transfer drawing]({{ site.baseurl}}/img/posts/blockchain/transfer.png)]({{ site.baseurl }}/img/posts/blockchain/transfer.png) 

Cryptography solves these problems really well. With for example Bitcoin, anyone can create a wallet on their smartphone for free and start receiving and spending money, with low transaction costs (a few cents today). Nobody needs to trust you, nobody overcharges you, and nobody cares how much money you have. Everybody can join.

There is also the possibility of real transparency to consider. If the money (Bitcoins) you donate to some organization to help out somewhere in the world were traceable, it would be much harder to cheat the people in need. If any money went missing, everyone would know, and the organization could be held accountable. Another example could be if you are part of a microfinancing institution. It would be good to know that the money you lend out is going to the people they are supposed to. A lot of corruption and cheating could be made a lot harder to do with blockchain. 

&nbsp;

## Decentralized Apps

Decentralized Apps, or "Dapps", is where things start to get interesting for me. Imagine if your back-end was on the blockchain. Imagine if all your back-end logic was verified and run by a world computer. Imagine if you could just upload some piece of code to the blockchain, and nobody could ever take it down.

[![Dapps drawing]({{ site.baseurl}}/img/posts/blockchain/dapps.png)]({{ site.baseurl }}/img/posts/blockchain/dapps.png) 

The idea that you can run code on the blockchain is incredibly cool. But it's hard to wrap your head around. It's not like you can write a traditional REST API server and just put it on the blockchain. Not quite at least. It doesn't work exactly like a regular server. It's more like a decentralized location for your code. The execution of that code can happen locally on your user's computer (because they have downloaded the blockchain), or in the blockchain network (if you need to change state or create a transaction of some kind).

Take for instance my Extreme Results web app, which runs on a cloud server somewhere. If that server goes down, XR goes down. If that code was in a blockchain instead, it could never go down. 

I want to use the most popular blockchain app platform as the example here: Ethereum. The way Ethereum works is that as a developer you create something called a "Smart Contract." A smart contract is a lot like a class. It can contain some functions with logic, some state, and it has a balance of Ether (Ether is the value token on Ethereum, just like Bitcoins). Once you have your smart contract on the blockchain, the code (functions) on it can be triggered and executed.
 
The code can be triggered by either a user or another contract (which allows smart contracts to interact with each other). If the code triggered is transactional (i.e. it changes state or sends Ether), it needs to be run on the blockchain and verified by the network. If not, it could run locally (because it just fetches you some data, no new transaction is required).

To make sure people are not doing things like infinite loops and other computational expensive things, you have to pay for your execution. If you as a user calls the execution, you are paying for it. If another contract is triggering it, then IT pays for the execution (remember how I told you that smart contract has an ether balance?).

The big idea here is that the code cannot go down, and it cannot run any other way than the way it was programmed. If it for some reason ran differently on the nodes in the network, the transactions it created would be rejected (because it would not be consensus on the blockchain on the new transactions).

To illustrate, I have created and uploaded a stupid little hello world contract. All it does is count how many times it has been called. It has two functions, one transactional, and one read only.

The contract is written in Ethereum's programming language called Solidity.

{% highlight javascript %}
pragma solidity ^0.4.6;
contract HelloCounter {

    uint counter;

    function HelloCounter() public
    {
        counter = 0;
    }

    function helloWorld() returns (string) {
        counter = counter + 1;
        return "Hello World!";
    }

    function numberOfTimesCalled() constant returns (uint) {
        return counter;
    }
}
{% endhighlight %}

When you call the helloWorld() function, the counter state is updated. This call will be a transaction that needs to go on the Ethereum blockchain (because the state is changed). You as the caller will need to pay for that (won't cost much). Whenever someone with an updated blockchain calls the numberOfTimesCalled() function, they will get back the number of times the helloWorld() function has been called. And this is a truth on the blockchain.

This example code is very simple, and might not show the true power of Ethereum, but the concept is solid. Since this is programming, you as a developer will be able to think of what kind of things you can do with such power.

You can image that you create a smart contract for some object (perhaps a digital one) you are buying together with your spouse. The contract could work this way:

The object ownership is transferred (as a token of ownership on the blockchain for instance), and payment is paid to the seller as soon as:

1. All required participants have paid their share.
2. Each user has signed some document that is signed digitally on the blockchain. 


You could create contracts for goods and services too. They could make sure the correct parties get paid when they are supposed to because nobody would want to deliver until all money is in "escrow" by the contract. With these kinds of contracts, you wouldn't have to put your trust in anything else than the network. And the network is not owned by one company; it's owned by everyone involved. Everyone who runs it. Everyone who uses it.

If you are a web developer and still struggling to wrap you head around Dapps, take a look at this great post: [Ethereum for web developers](https://medium.com/@mvmurthy/ethereum-for-web-developers-890be23d1d0c){:target="_blank"}

If you want to know where you can get started with Ethereum coding, take a look at this great article by the same guy: [Full Stack Hello World Voting Ethereum Dapp Tutorial](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2){:target="_blank"}


&nbsp;

## Decentralized Cloud Computing

The cloud right now is just a few mega providers like Amazon, Google, Microsoft and a few others which mean that a few companies have all our data and all of our processing power. There is a lot of computing power out there which is not being utilized, so why not use some of that instead? How about renting out some of the power that is currently not being used in your gaming PC?

You can imagine that you need to run some heavy computations like:

- Render graphics
- Big data analysis 
- Machine Learning algorithms
- Run simulations (for instance science tasks like folding proteins)

Today, you could do all of the above in Amazon's cloud. But it's relatively expensive, especially if you need to run a bunch of tasks in parallel. A ton of small tasks is ideal for a network like this. It can also help with lag from your service providers because you might be able to get processing power that is near you (instead of some fixed data center).

Golem and iEx.ec are two projects that are starting up with this kind of technology, and I think it's something to look out for. I for one plan to rent out my computing power! 

[iEx.ec](http://iex.ec/){:target="_blank"}

[Golem](https://blog.golemproject.net/){:target="_blank"}

&nbsp;

## IoT

If the Internet of Things is going to be as huge as everyone keeps saying, then we need another solution for all that communication that it will generate. Should all that data go into centralized data centers for processing and storage? And what about sensitive data? How can you know for sure that the data collected is correct and hasn't been tampered with? And what if IoT devices need to communicate with each other, or buy services or data from each other?

There are many potential issues with IoT, and the blockchain can help out. Using a blockchain, your IoT devices can store its data on a blockchain and sell that data (using some cryptocurrency perhaps?) automatically (using smart contracts). And best of all, it doesn't run on any centralized servers.

A big problem with today's IoT devices is that they tend to do all their work on some cloud services, which is OK as long as you can access the service you need. But what happens when the company that owns that cloud services goes under? That has happened already, and it's going to happen again.

Just to go a bit further, let's imagine a scenario where all the IoT devices are running on a fast, cheap and secure blockchain. Imagine that your devices can barter for services like processing power, storage and data using its own cryptocurrency automatically using smart contracts. Or perhaps your house has some extra electricity from your solar panels that you sell directly to your neighbor (again, automatically using smart contracts) while you are on vacation and don't need it.

Another possibility is that you have a lot of IoT devices running at home (inside and out) that collect data from your environment. Perhaps some company currently need data from an enormous amount of people to power their new machine learning algorithm. Since all your data is on the blockchain, you can sell any data you want to that company. It's your data after all! This is better than a company selling your data for you, without you getting anything for it. And in that scenario, you couldn't choose which data to sell either.

There is just so much possibility here that I think we would be stupid not to try to utilize it.

&nbsp;

## Supply chains and goods history

We are back to transparency and traceability, but this time it's a more physical aspect. Blockchain can help trace history in a reliable way, which can contribute to knowing for sure where everything comes from. If you wanted to know that a piece of meat was produced in such a way that it didn't impact the environment, there could be a history attached to the animal from which the meat came from. 

Right now supply chains are incredibly complex, and it's hard to trace anything related to it. Forced labor, counterfeiting, and environmental impact are only a few of the things both consumers and regulators need to be able to track.  

Provenance is a company that is trying to do just that. In their own words: "Products are more than meets the eye. They are the sum of their creators’ work, history, and ownership. What if there were a new digital dimension to products that gave verified information about their producers, origins, and ingredients? We created Provenance to do just that."

[Provenance](https://www.provenance.org/){:target="_blank"}

&nbsp;

## Voting

Blockchain lends itself to voting scenarios very easily, because you could verify that nothing funky has been done. You could truly count every vote, and it would be guaranteed to be correct. You could actually prove it.

You could create safe and secure voting for anything that requires it.

I guess such a system might make any voting process feel a lot safer than today. Today there are so many parties we have to trust in our voting systems. I for one would feel better if we could prove the votes are correct instead. 

&nbsp;

## Governments

Transparency and keeping our politician's honest sounds like a very important usage for blockchain. We can imagine that you could monitor and make sure the politicians act with integrity and hold their promises. We could force a lot of it through smart contracts.

If all decisions made were on the blockchain, then it would be easier to make sure no "off the book" transactions and shady deals went down. We want to make sure everybody behaves with integrity and honesty, right?

This is probably far off, but if the benefits are needed, we could push for it sooner. We need government officals to act with integrity not just because they feel like it, but because it is required! There should be no way around it.

&nbsp;

## Decentralized and Autonomous Organizations

Decentralized Autonomous Organizations is relatively new and unexplored concept, but the idea is to use smart contracts to run and organize a business. It could be an organization with no conventional management or employees. Everything is automated. You have stakeholders in the form of digital tokens on the blockchain, and they can vote and make money off their organization.

An interesting aspect of such an organization is that it can be run entirely by anonymous people. As long as you can buy the digital tokens, you can be part of the business.

There was such a project called the DAO, which launched on the Etherum blockchain with a ton of success. People poured money into it. The DAO was supposed to let it shareholders vote on investment opportunities, and the profits from said investments would get back to the investors - automatically. All code.

The DAO was a fascinating and potentially amazing opportunity, but it was also a flawed one. Since such an organization is only code, it can have security flaws that hackers can exploit. And someone did. The hack managed to get Ether valued $50M. Because of the hack, Ethereum was hard-forked to make sure everyone got their money back. The hard-fork was not popular with everyone (someone felt that this was cheating or something I guess), and the old branch is still running under the name of Ethereum Classic. So the community is essentially split in half because of this.

If you want to read all about the DAO and what happened there, take a look at this in-depth article: [Understanding The DAO Attack](http://www.coindesk.com/understanding-dao-hack-journalists/){:target="_blank"}

The cryptocurrency Dash actually already has a DAO type governance working for them. And it seems to be working! If you are interested in exactly how they do it, take a look at this video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/b_hVTRoUrjw" frameborder="0" allowfullscreen></iframe>

&nbsp;

## Ownership

In many poor countries, the process for registering ownership of land is a long and tedious process, often drenched in corruption and less-than-ideal integrity. After the Haiti earthquake in 2010, Red Cross had serious problems trying to figure out land ownership in order to rebuilding things.

Having ownership recorded on the blockchain would allow people to prove they own something, and transfer of ownership would be transparent, fast and secure.

&nbsp;

## Cloud storage

Several projects are trying to use blockchain to enable decentralized cloud storage. The prospect of having all of your files on others people's computers might sound a bit weird, but it's better than having all your files at for instance Dropbox or Google Drive. The big difference is that with decentralized cloud storage, nobody has an entire file of yours (they get split up) and most importantly they are all encrypted on your computers, so only YOU can unlock them.

Ditching the current cloud storage concepts shouldn't be too hard to sell. After all, there have been many security breaches for the big cloud storage providers in the past years. I would guess that the market is ready for a change. Perhaps a secure, cheap and decentralized one?

A couple of the players in this field today is Sia and Storj.

Here is a video on how Storj works:

<iframe src="https://player.vimeo.com/video/102119715?color=ffffff&title=0&byline=0&portrait=0" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<p><a href="https://vimeo.com/102119715">Storj: Decentralizing Cloud Storage</a> from <a href="https://vimeo.com/user30243596">Storj</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

&nbsp;

## Gathering Big Data

Getting hold of Big Data of any type can be a challenge for anyone who wants to do machine learning.

Blockchain can help incentivize people with data to give it up (sold for tokens) and make it available for people who need it (purchased with tokens).

A great example of this is the Lampix token PIX project. They need a billion {image, description} data sets to train their machine learning algorithms. 
They have created a blockchain system with allows people to sell such sets to the chain (sold for PIX tokens) and allow anyone to purchase data sets of any size they need (purchased with PIX tokens).

This could be used for any kind of data sets that someone might need. In the future, there might be marketplaces where you can purchase real data on the blockchain!

&nbsp;

# Blockchain challenges

While there are a lot of great things that blockchain technology can be utilized for, there are also a lot of challenges it needs to overcome going forward.

All of these challenges are something I see not as reasons to discard blockchain, but reasons to get together and work to solve them. The potential for greatness is too big to ignore.

&nbsp;

## Scaling

The Bitcoin blockchain is currently limited regarding how many transactions it can fit in a single block. And a new block is mined every 10 minutes. So if the number of transactions went up by a lot, then transactions would begin to queue up, slowing the network down.

The reason we can't just increase the size of a block is that that doesn't scale over time either. No amount of block size would be enough if everyone started using Bitcoin. There are also several other technical and social reasons why it's not entirely straightforward, but I won't go into details here.

Other blockchains have solved this in different ways, but each has issues to deal with when it comes to big time scaling. 

&nbsp;

## User friendliness

Using Bitcoin and most other blockchain technologies today is not especially user-friendly. People don't understand why they have to do all this complicated stuff with public and private keys and shady clients with poor UI's and all that stuff. 

Right now, most of the people using Bitcoin are geeks. They want to learn how to do this sort of thing. But for my parents to be able to use blockchain technology on a daily basis (not just Bitcoin), it needs to get a lot simpler.

People are working on that, however. For instance, the cryptocurrency called Dash is trying to be the cryptocurrency even your grandmother can use... Let's hope they can do it!

&nbsp;

## Speed

Bitcoin uses by average 10 minutes to create a new block. This is significant because a transaction is not done before it's included in a block. This is a lot faster than bank transactions today; we just aren't aware of it. 

Instant transactions are needed for many use cases by blockchain. Dash has this already. Many other blockchains are also a lot faster than the 10 minute limit for Bitcoin.

There are a lot of technical discussions going on right now on how to best solve these kinds of things, and it's going to be interesting to see how it plays out. But it needs to play out faster than today, that's for sure!

&nbsp;

## Code is law. Never forget

Previously, I mentioned while talking about trust that code which never wavers has some negative sides. Well, imagine the world with no second chances. Everything you ever do is on record. There is no escaping your mistakes.

If a law is stupid and makes no sense, there is no way to just look through the fingers in specific cases. Sure, this would help out in corruption and lot of other cases, but when the code is unjust, there is no way out either.

This is partly the problem that the Ethereum fork is based upon. The fork was created because most people wanted to revert a wrong-doing, but not all agreed that bending the rules was OK (even though it seemed morally just).

&nbsp;

## Energy consumed by proof-of-work

I haven't talked too much about consensus algorithms in this post because it's such a technical topic. What I wanted to point out, however, is that the mostly used algorithm today (the one in Bitcoin) uses a lot of energy.

In fact, it uses hundreds of megawatts. That's enough to power several hundred thousand houses. Just to keep the Bitcoin network secure. It seems incredibly wasteful, especially when we think about the time we live in. Bitcoin is not good for the planet right now - that's for sure. 

There are other ways to solve the census algorithm problem for blockchain, and many are already doing just that. We just need to make sure everyone finds a good and secure way to do it. Security AND keeping the planet cool - that should be attainable. 

&nbsp;

## Governments trying to control things

This is mostly only applicable for Bitcoin and other cryptocurrencies (at least for now) because they seek to disrupt what the governments today are managing. Money. The big banks might not be pleased with their systems getting overthrown either...

If people want this change, it will happen at some point. Exactly how it will play out is going to be very interesting.

&nbsp;

## Governing protocols

When nobody and everybody owns something, it becomes kind of an issue to regulate it properly. Today there is a lot of yelling and screaming and then somehow agreeing on things after a while. 

I hope organizations like the Internet Engineering Task Force and W3C will form at some point for blockchain technologies. It would be a lot more focused than it is right now. I believe this will happen once things get enough traction. It's just a matter of time.

&nbsp;

# The future of Blockchain

The future of blockchain is super exciting. I can't wait to see what people will come up with!

There is so much going on in this space that I can't possibly keep up with all of it. If you want to learn more, try to follow a few Reddit boards on different kinds of blockchain technology.

&nbsp;

# Exciting Blockchain Projects

In the next part of this series, I explore some of the most innovative and exciting projects right now in the blockchain space:

[Part 3: Exciting Blockchain Projects]({{ site.baseurl }}/the-blockchain-innovation-part-3-exciting-blockchain-projects/){:target="_blank"}  
