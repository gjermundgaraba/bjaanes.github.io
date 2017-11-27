---
title: 'Understanding Ethereum Smart Contracts'
date: 2017-11-27T08:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /understanding-ethereum-smart-contracts/
categories:
  - Uncategorized
---

You might have heard the term "smart contract," and you might even know that they are "code" you can run on a blockchain.

But how can you run *code* on a blockchain? It's not the easiest concept to wrap your head around.

This post explains how smart contracts work on the Ethereum Blockchain.

Basic understanding of programming will help as this post contains some code - although the examples a simple.

<!--more-->

&nbsp;

*Some technical details in this post are slightly simplified for the sake of clarity, but the concepts are valid.*

&nbsp;

# Blockchain - Quick & Dirty

Without going into too much detail, the central concept of Blockchain technology is a distributed ledger.
It's a particular type of database that is shared among many participants.

This special database is just a list of transactions. Every transaction that has ever happened in the network. 
Everybody can have their own copy. This distribution coupled with strong monetary incentives removes the need for trust between parties.

Traditionally, trust between parties has been solved using middlemen, third parties. Paypal. Your bank. 
A transact with someone you don't trust would go through an intermediary both parties trust. 

With blockchain, this need is eliminated because you can instead put your trust in a network where the want to cheat is removed by strong incentives (in short: it's much more profitable to stay within the rules).

[![Distributed Ledger]({{ site.baseurl}}/img/posts/distributed_ledger.png)]({{ site.baseurl }}/img/posts/distributed_ledger.png)

To become a bit more concrete: A blockchain network is a bunch of machines which all have the same copy of the list of transactions (e.g., money sent from person A to person B). 

Since everybody has the same list, it is hard to fool the network into accepting false transactions. 
Combine this with some cryptographic algorithms and monetary incentives to follow the rules, and you get a pretty secure network.

All of this also makes blockchains pretty much immutable. The only way to change the history is for most of the network to agree to do it.

If you want a bit more in-depth introduction to blockchain (which is more accurate too) you can take a look at this post:
[The Blockchain Innovation Part 1: What is Blockchain]({{ site.baseurl }}/the-blockchain-innovation-part-1-what-is-blockchain/){:target="_blank"}

&nbsp;

# What is a smart contract?

The main thing that makes Ethereum different than Bitcoin is that Ethereum has the concept of smart contracts.
Bitcoin is digital money; store of value. Ethereum is also digital money, but so much more.

The name "Smart Contract" is a bit misleading. They are not really contracts, and they are not particularly smart either. 
They are just pieces of code - or computer logic - that can run on the blockchain… 

The first thing I will introduce about smart contracts is that they are a special kind of account on the Ethereum Network. 
You have user accounts, and you have smart contract accounts.

A user account is just
* An address (sort of like your bank account number - this also exists on Bitcoin)
* A balance (how much money do I have)

A smart contract account has:
* An address
* A balance (of Ether)
* A state
* Code

**The address** is the same thing as any regular account. It’s just the unique identifier for the account.

**The balance** is also the same thing as any regular account. The only exciting thing is that a balance on a smart contract means that code can own money. It can handle money. And it can mishandle it if incorrectly coded.

**The state** of a smart contract account is the current state of all fields and variables declared in the smart contract. It works the same way as field variables in a class in most programming languages. In fact, an instantiated object from a class is probably the easiest way to think about smart contracts. The only difference is that the object lives forever (unless programmed to self-destruct).

**The code** of the smart contract is compiled byte-code that Ethereum clients and nodes can run. It is the code that is executed on the creation of the smart contract, and it contains functions that you can call. Just like any object in an object-oriented programming language.

*Side note:* Fun thing about smart contracts: they can call other smart contracts. This opens up the ability to create autonomous agents that can spend money and do transactions by themselves.  


```
contract Counter {
    uint counter;

    function Counter() public {
        counter = 0;
    }
    function count() public {
        counter = counter + 1;
    }
}
```

Let’s say I create a smart contract with the above code.
The code has a single field called “counter” of type uint (an integer). The content of the counter variable is the state of this contract. Whenever I call the count() function, the state on the blockchain for this smart contract will be increased by 1 - for anyone to see.

[![Smart Contract Infographic]({{ site.baseurl}}/img/posts/smart_contract_infographic.png)]({{ site.baseurl }}/img/posts/smart_contract_infographic.png) 

We’ll get back to how this works with more examples, but first I want to go back to the transactions on Ethereum and Bitcoin to explain a few things.

&nbsp;

# Ethereum vs. Bitcoin on the Transaction-Level

Bitcoin transactions are pretty simple in what they do. You can do one single thing. One type of transaction. 
Skipping some details, it all boils down to **TO** (who is receiving money), **FROM** (who is sending money) and **AMOUNT** (how much money). 
This let’s bitcoin be a store of value with the capability to transfer the value between participants in the network.

What makes Ethereum different is that the transaction also has a **DATA** field. This **DATA** field enables *three* types of transactions:

* Transfer of value (same as Bitcoin)
    * **TO** recipient address
    * **DATA** field empty or containing any message you want to attach
    * **FROM** you
    * **AMOUNT** of Ether you want to send
* Create smart contract
    * **TO** field is empty (this is what triggers the creation of a smart contract)
    * **DATA** field contains smart contract code compiled to byte-code
    * **FROM** you
    * **AMOUNT** can be zero or any number of Ether you might want to give to your contract
* Call smart contract
    * **TO** field is the address of the smart contract account
    * **DATA** field contains function name and parameters - how to call the smart contract
    * **FROM** you
    * **AMOUNT** can be zero or any number of Ether if for instance, you need to pay the contract for a service

There are more fields and complexity that goes into these transactions, but these explain the central concept well.

Let’s see some more concrete examples of how those transactions might look like.


## Ethereum Transactions

### Transfer of value

```
{
    to: '0x687422eEA2cB73B5d3e242bA5456b782919AFc85',
    value: 0.0005
    data: ‘0x’ // Could also send a message here if we want to
}
```
Very simple. To an address with some amount of Ether. 

You can also add a message to the transaction if you'd like.


### Create smart contract

```
{
    to: '',
    value: 0.0
    data: ‘0x6060604052341561000c57fe5b60405160c0806……………’
}
```
Like mentioned, an empty **TO** field signifies the creation of a smart contract. 

The **DATA** field contains the smart contract code compiled to byte-code.

### Call contract

```
{
    to: '0x687422eEA2cB73B5d3e242bA5456b782919AFc85’, // Contract
    value: 0.0
    data: ‘0x6060604052341561000c57fe5b60405160c0806……………’
}
```
We'll get back to this one momentarily, but the main concept is that you send the transaction to the address of the smart contract you want to call and you put the function call in the **DATA** field. 

&nbsp;

# Note about cost and execution

As you might imagine, you can't just go ahead and run computationally heavy programs on the blockchain for free.

The execution of code is being paid by the caller in something called *gas*. Gas is the fuel that runs the Ethereum Virtual Machine. 
You can think of it as payment per execution of instruction (almost like a line of code).

You have to set the max amount of gas you want to spend on a particular call. 
If for instance, the code you called went into a forever loop you would spend no more than your max gas on the execution.

The cost of gas (execution) is decided by the miners of the network - the nodes that are running the code.

There is a lot more to gas and execution, but it is worth keeping in mind.

If you want to take a deep dive into this part of Ethereum, take a look at this great article: 
[Ethereum, Gas, Fuel & Fees](https://media.consensys.net/ethereum-gas-fuel-and-fees-3333e17fe1dc){:target="_blank"}


&nbsp;

# How do smart contracts work?

When a smart contract has been deployed to the Ethereum network, anyone can call the functions of the smart contract. The function may have security features that block people from using it, but you are free to try.

Calling a function on a smart contract is in many ways similar to "normal" programming - with some differences in executing of course.

Let’s say you have an object of type *"MyObject"*. That object has a function called *“myFunction”*. 
To call it, you simple reference the instance of the object, which function to call and which parameters to call it with. Like this:

```
myObjectReference.myFunction(parameters);
```

If the function returns any value, you can save it in a variable:
```
myVariable = myObject.myFunction(parameters);
```

Calling a smart contract is conceptually the same thing. 
The only difference is that you have to put all the information about the call into a transaction, sign it and send it to the network to execute.

Let’s say you want to call function “myFunction” with some parameters on smart contract “0x0123456"

Calling the smart contract consists of four steps:

[![Calling a Smart Contract Infographic]({{ site.baseurl}}/img/posts/calling_a_smart_contract_infographic.png)]({{ site.baseurl }}/img/posts/calling_a_smart_contract_infographic.png)

Now, when the transaction is put into a block in the blockchain the change of state will be reflected in the entire network.

&nbsp;

# The World Computer

Ethereum is being called by many for the World Computer. And it's not a bad analogy. It's like a virtual machine that is being maintained by the whole world!

One thing to keep in mind though: while smart contracts are Turing complete and can, in theory, do anything, they are not well suited to heavy computational work.

The Ethereum World Computer is like an old slow computer that can run simple programs. And it is vital to keep Ethereum Smart Contracts small and simple because of cost and security.

The more computation a contract demands, the more it costs to run it. The more complex a contract is, the more likely it is to have security holes. 
And a security breach in your smart contract is very hard to do anything about - the blockchain is immutable after all. 

[![World Computer]({{ site.baseurl}}/img/posts/world_computer.png)]({{ site.baseurl }}/img/posts/world_computer.png) 

&nbsp;

# Example: Token

Just to drive the point home, I want to explain how tokens work. 
You know, those tokens that everyone raves about in their ICO’s? If you are not familiar, the concept is that you can create your own token, or "coin," on top of Ethereum. 

Most of those tokens are created on Ethereum, and the concept is alarmingly simple (it works fine, but it is so simple that it’s almost stupid).

How would you program a simple monetary system using Javascript or any other programming language? Well, you could do it all in a single file. All you really need to keep track of is:
1. Total supply
2. Accounts
3. Amounts of money in accounts
4. Movements of money

With a simple mapping between users and amounts you get number 1, 2 and 3:
```
Map<Account, Double> usersAndTheirMoney;
```

This map just maps an account to an amount of money.

With a constructor function you can set up the initial supply in your own account (or spread among any number of accounts):
```
public Token(Account initialAccount, double initialSupply) {
  usersAndTheirMoney.put(initialAccount, initialSupply);
}
```

Movements of money are done with simple functions that just subtract from one account and add to another:
```
public transfer(Account from, Account to, double amount) {
  verifySenderOfMoneyIsCaller(from);
  verifySenderOfMoneyHasEnoughMoney(from, account);
  usersAndTheirMoney.put(from, usersAndTheirMoney.get(from)-amount);
  usersAndTheirMoney.put(to, usersAndTheirMoney.get(to)+amount);
}
```

This is the exact same concept we use in Ethereum to create tokens. Granted, there is some more complexities and extra functionality, but the basic concept is very simple.

This is what a basic Token contract could look like (again, simplified for clarity) in Ethereum’s own programming language (Solidity):
```
contract MyToken {
    mapping (address => uint256) public balances;
    function MyToken(uint256 initialSupply) {
        balances[msg.sender] = initialSupply;
    }   
   
    function transfer(address to, uint256 amount) public {
        balances[msg.sender] -= amount;
        balances[to] += amount;
    }
}
```

This is the general programming concepts that lie beneath the ICO craze that is going on. I think that says something about the power of Ethereum as a platform. With some simple code, you can generate a token out of thin air that is essentially just some variables being kept track of by the world computer. Welcome to the new internet. 