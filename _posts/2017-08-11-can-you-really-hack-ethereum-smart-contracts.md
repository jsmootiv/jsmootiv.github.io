---
layout: post
title: Can you really hack Ethereum smart contracts?
image: /assets/images/gavel.png
image_alt: The blockchain does'nt neeed a judge
excerpt: You can't "hack" an Ethereum smart contract. In fact, this incident disproves the viability of Ethereum in general.
permalink: /can-you-really-hack-ethereum-smart-contracts/
tags:
  - ethereum
  - cryptocurrency
--- 

A couple of weeks back, there was an incident where a "hacker" was able to take advantage of an issue in an Ethereum smart contract to "take" 30MM worth of Ethereum (ETH).

[You can see the transactions on Etherscan here](https://etherscan.io/address/0xb3764761e297d6f121e79c32a65829cd1ddb4d32) 

But I'm not sure that "theft" is the appropriate term to use in this situation. In fact, this incident disproves the viability of Ethereum smart contracts in general.

To understand why I've come to believe this, first, lets talk about what it means to own a cryptocurrency.

### You don't actually possess cryptocurrency unless you run a node

When you own a cryptocurrency, you can't really "hold it in your wallet" like you could have a $100 bill in your physical wallet. In crypto, your wallet is actually a key which is used to control the associated account number on the Blockchain.

This isn't all that different than how banks work.

Your bank debit card allows you to make charges or deposits against a digital representation of the amount of money that is held by the bank. The history of past bank transactions (the ledger) is maintained on bank computers within private networks.

With cryptocurrencies, however, the ledger is stored on a network of computers all around the world. All of these computers "vote" (gain consensus) on a group of transactions to determine which are valid and which are not.

How exactly the consensus system works is outside of the scope of this post, but what you really need to know is that because of the way Ethereum works, anyone who is running an Ethereum node has access to everything. Every Ether ever created every balance on every account and, most importantly, every smart contract that was ever written.

So the alleged hacker didn't need to break into a computer --[which is what the US government considers hacking](https://www.law.cornell.edu/uscode/text/18/1030). The alleged hacker just needed to run an Ethereum node, at which point the ETH she "took" and the contract that she "exploited" was actually already on her computer. 

### Can you take something that has been given to you?

If you give your money to a bank, and they keep it, we don't call that a hack. 

Believe it or not, this happens all of the time. 

When you do something like send a wire from your bank account, the bank ~~keeps~~ charges you a fee. If the bank charges you more than they are supposed to you would need to convince a judge that the bank violated the terms of the agreement that you had setup with the bank. If the judge agrees with you the judge forces the bank to suffer consequences.

The whole idea behind the blockchain is to remove the need to trust a judge or any other singular 3rd party to maintain the history of transactions or resolve disputes. This is done via the consensus process I mentioned above. 

This is easy on Bitcoin because when you send a Bitcoin to someone, there isn't much to dispute. You sent the coin, or you didn't.

With Ethereum, this is a little different.

Ethereum allows people to setup more complex agreements between parties. These agreements are called smart contracts.

I like to think of a smart contract like an on blockchain vending machine. It sits there, and when you deposit a token, it does some work and outputs something else. Behind the scenes, a smart contract is really just a computer program that executes on blockchain nodes. The big problem is that, like all computer programs, it's nearly impossible to build something without bugs.

### The alleged hacker violated no agreement

In this case, the bug in the contract clearly allowed for an owner to be changed after the contract was initialized. The alleged hacker didn't do anything that the contract didn't allow, they merely sent a message which executed the contract as it was written.

So moving forward we should all refer to the alleged hacker as the "contract executor" which is more accurate.

You may think the intent behind the contract was to keep the Ether safe. And you are probably right.  Computers don't understand intent though. Computers blindly execute instructions that they are given so to have the intent argument mean anything you would need to argue it in front of a judge. One of the core ideas behind the blockchain is to remove the need for any type of argument like this. The balances (state) on the chain is the state that is agreed upon by the network, not a group of judges. 

If we are arguing about intent the requirement to have a 3rd party decide on the intent negates the whole idea behind a contract on the blockchain in the first place.

### The smart contract is the authority

Recently I also found out that æternity (one of the "victims" of the contact execution) is working with the authorities to track down the contract executor.

> ["Together with æternity’s lawyer, we have contacted the Liechtenstein police authorities and filed charges. The police will forward the matter to Interpol."](https://blog.aeternity.com/parity-multisig-wallet-hack-47cc507d964d)

As I said above, what makes the Blockchain worth using is its decentralization. If we need the courts to enforce transactions on the blockchain, how is that any better than the current non-blockchain method of transacting with people?

By going to the authorities æternity is admitting that the Blockchain isn't an improvement at all. Which means that the old school method writing a "real world" contract between partners would have worked just fine.

In æternity's case, they could have done a partnership agreement and sent the cash to a bank account that requires multiple signatures for withdrawing funds. In this case, they would have been admitting that the contract language may be flawed and that you may need a 3rd party to decide what it really meant.

"But what about their ICO" you may be thinking, "they needed the blockchain to raise money". Well, there are still ways of funding projects off chain that have proven themselves over history to be secure and stable. Living by the ICO sword, also means that you should be willing to die by it.

Especially if you are a blockchain company.

So there you have it, a hack wasn't a hack. It's just an execution of a contract with a bug. To argue about the intent of the contract would need someone to decide on what the correct state should be which negates the whole purpose of a smart contract to begin with.

Since the decentralized consensus process is really the only thing that is valuable about the blockchain, the above means that smart contracts, on chain, are useless.