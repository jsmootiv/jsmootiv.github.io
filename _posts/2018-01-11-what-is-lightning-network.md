---
layout: post
title: What is the lightning network?
image: /assets/images/flash-logo.png
excerpt: "Put simply, the Lightning Network allows for you to send Bitcoin payments incredibly fast. How fast? Read on to find out."
permalink: /what-is-lightning-network/
tags:
  - bitcoin
  - lightning network
---

Imagine instant transactions with anyone in the world, without the need for a central intermediary. Think this system is Bitcoin?

It's not because Bitcoin is slow.

Let me explain with a few numbers.

Currently VISA processes around 2,000 transactions per second. The Bitcoin network can only handle about 3 per second. This is a big gap to fill if Bitcoin has any chance at becoming a widely used store of value. 

The other major issue with Bitcoin is fees. 

Because of the way the protocol was designed, there is only so many transactions that can be processed every ~10 minutes, which means that as demand for transactions increases, the fees will also increase due to the limited capacity.

But what if something can be built on top of Bitcoin that will allow for a faster throughput and lower fees?

That's the big idea behind the "layer 2" system called the [Lightning Network](https://lightning.network/) that is is currently being tested on the Bitcoin testnet.

Nothing like Lightning Network exists right now so I always tell people the best comparable user experience is Venmo.

You send cash from your bank to Venmo. While your cash is in your Venmo account you can't spend it with your ATM card but you can send it instantly to anyone else who is on Venmo. To make the cash spendable with your ATM card again you send it back to your bank.

All of the technical complexities aside, this is how Lightning Network works from a user standpoint. Put simply, you "send" Bitcoin to the Lightning Network using something called a payment channel. While this channel is open your Bitcoin is spendable on the network, which means you can pay other people on the network instantly. The channel maintains your running balance and once you close it the final balance is cemented on the blockchain.

This means 2 things:
1. You will have 2 slow transactions but most transactions will be fast. One to get the Bitcoin onto Lightning Network, and one to get Bitcoin off of Lightning Network. Every intermediate on network transaction happens instantly.
2. You will only pay transaction fees 2 times. When you put Bitcoin onto Lightning and when you take it off.

So on network transactions will have a very minimal fee and happen instantly.

If Lightning Network can get running and stable on the main Bitcoin network it's going to bring Bitcoin one giant step closer to its potential because transacting will get cheap and fast.

How fast? Let's take a look at the numbers.

- Bitcoin (no Lightning Network): 3 transactions per sec
- VISA: 2,000 transactions per sec
- Bitcoin (with Lightning Network): Millions of transactions per sec

I plan to write some more on Lightning later but first I'm going to work on getting a [Lightning Network Node](https://github.com/lightningnetwork/lnd) up and running.

I'll be sure to report back on how that goes. In the meantime here is a great infographic that explains everything by [Billycoin](https://www.reddit.com/user/billycoin) on Reddit.

![How LN Works, infographic.]({{ "/assets/images/ln-infographic.png" }}){:.center}


