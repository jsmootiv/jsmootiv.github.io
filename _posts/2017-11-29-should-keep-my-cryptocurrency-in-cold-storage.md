---
layout: post
title: Should I keep my cryptocurrency in cold storage?
image: /assets/images/keys.jpeg
image_alt: 
excerpt: "Whats the difference between having assets on the exchange, in a wallet, and in a hardware wallet?"
permalink: /should-keep-my-cryptocurrency-in-cold-storage/
tags:
  - cryptocurrency
  - bitcoin
  - storage
  - questions
  - cryptography
--- 

Today I got a question from a friend about the various ways to store crypto assets. I started to respond but decided the response would be a great blog post instead so read along.

Here is my friend’s question:

> “Regarding wallets, using Coinbase as an example, whats the difference between having assets on the exchange, in a wallet, and in a hardware wallet?”

The answer to the question really comes down to who controls the assets. But before you can understand that you need to have a high-level understanding of cryptography.

Say you want to send an email that only you and I can read. How would you do it?

One way is for us to create and share a passphrase that can be used to encrypt the message. This works because since only you and I have the passphrase, anyone who intercepts the encrypted message won't be able to read it. This is very much like one of those decoder rings that you use to be able to get in a cereal box.

The big problem is obvious. If someone gets ahold of the passphrase, they can now decrypt and read any previous or future message sent between you and I.

One way to safeguard against this is to change our encryption method so that the passphrase can be used to encrypt the message but *not* decrypt it. That way, even if someone got ahold of the passphrase it wouldn’t matter.

Sounds impossible right?

Well thanks to some really fancy math, it's not.

I have a fairly vague understanding of the math so I won't attempt to explain it but the method of encryption is known as “asymmetrical cryptography”. Although the term is a bit of a mouthful, the intuition is very simple. We create a passphrase (in the crypto world this is called a key) which has 2 parts. One part is considered “public” and the other part of the key is “private”.

The public key is a “one way”, which means nobody but I would be able to read a message encrypted with the key —not even the sender. Because of the public key’s “one way” nature, it can be publicly shared with everyone. For instance, you can find [my PGP public key here.]({% link public-key.md %})

To decrypt a message encrypted with my public key, I use my private key which is kept secret.

One other important thing about public/private is that I can use the private key to “sign” a message so that anyone with my public key can verify the message came from me.

I may cover how signing works in detail in another post but within this context, the signature is similar to a handwritten signature. Its small, its unique, and it can be easily verified. Where a private key signature diverges from a handwritten signature is in that, as far as we know, its impossible to forge.

## What does encryption have to do with crypto asset wallets?

When it comes to the blockchain, anyone can write a transaction and sent it to the network. Public/private key pairs are used by the computers to determine if the person who sent the transaction should be able to spend the funds sent the transaction.

For example, If you were to create a transaction that sends 0.001 Bitcoin to my address `3LDhDoKVRzfHFpJsCJ3nDgrswxbygghUjT` you would need to also sign the transaction with your private key. Once the transaction is broadcasted, the Bitcoin nodes can verify the signature included with the transaction to make sure that you are the owner of the 0.001 BTC you are sending to my address.

As I said at the beginning of this post, the main difference between keeping your crypto on an exchange and keeping it in wallet has to do with who controls the assets. Well, for the reason outlined above, controlling assets on the blockchain is the same thing as controlling the private key. So let's take a look at private key control in the various wallet scenarios.

If you create a software wallet using something like [Electrum](https://electrum.org/) you will generate a private key during the setup process. Since this is private, nobody knows it but you. Which means that you have total control over the assets. You can send however much you want to whatever address you want. If this sounds scary don’t fret because the wallet developers have done a good job at making it easy to create and sign transactions using the private key. Also, I know Electrum's website looks shady but is a legit option for a software wallets.

If you own a hardware wallet like a [Trezor](https://trezor.io/) or [KeepKey](https://www.keepkey.com/), during the setup process you create a private key which is stored on the device. This has the same benefits as a software wallet with some added security since the key is stored on a hardware chip. Having the key separate from your computer makes it resistant to hackers.

> Pro tip: if you are setting up a hardware wallet for the first time, it will give you a 24 word “seed phrase” which can be used to recover your device. *WRITE THIS PHRASE DOWN* on a piece of paper. Then before you send any crypto assets to the device, go through the recovery process so that you a) understand it and b) can confirm you wrote the phrase down correctly.

The above 2 options are like being your own bank which is awesome but this power comes with with a big responsibility. If you lose your private key (by deleting your wallet, forgetting the Electrum password, losing your device/recovery phrase, etc) you won't be able to sign transactions with it. This means that the blockchain cant verify you are the owner of the assets making them non-spendable.

Exchange wallets are like bank accounts. The exchange themselves generate and control the private key. They don’t share it with you or anyone else. This means that they ultimately are in control of your assets. If they [get hacked](https://en.wikipedia.org/wiki/Mt._Gox), [the founder goes to jail](https://www.theverge.com/2017/7/26/16035702/btce-arrest-bitcoin-alexander-vinnik-mt-gox-theft-suspect), or the exchange collapses you probably won't get your assets back. Also, most of the exchanges have limits on the number of assets you can send from the exchange in a 24 hour period.

So to wrap things up there are benefits and drawbacks to each storage option. Ultimately it will be up to you to decide whats best for you given your situation. Below is a quick overview.

### Hardware/Software wallet:

Benefits:
- If there is a fork, you control the key on both blockchains so you can spend the assets on both blockchains —basically, this means if a fork happens you get the forked currency guaranteed
- You control your assets which means no limits
- Privacy since you created your key in isolation
- The private key is on the device and signing takes place on the device. So someone cant hacks you and get access to your private key —on hardware wallets
- More flexibility for setting up things like multi-signature wallets

Drawbacks:
- Harder to setup
- Nobody to call if something goes wrong
- If you lose your key, there isn’t a way to recover it
- Moving to an exchange if Bitcoin is crashing can be nerve-racking 

### Exchange wallet:

Benefits:
- Easy to setup
- If something weird happens you contact (or sue) someone
- Some places like Coinbase have insurance

Drawbacks:
- Daily transfer limits —though you have the Bitcoin, you may not be able to send it anywhere
- Privacy: The exchange knows exactly who you are
- If a fork happens, it's up to the exchange to give you the forked currency

If there are any questions ask them in the comments below.

*Btw if you find this encryption stuff interesting and want to learn more, there is a great (and very accessible) book called [“The Code Book” written by Simon Singh](https://www.amazon.com/Code-Book-Science-Secrecy-Cryptography/dp/0385495323/ref=sr_1_1?ie=UTF8&qid=1511925030&sr=8-1&keywords=the+code+book) that I strongly recommend you read.*
