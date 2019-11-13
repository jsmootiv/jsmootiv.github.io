---
layout: post
title: Cryptocurrency Sentiment Analysis On Reddit
excerpt: A few weekends ago, I wrote a Reddit sentiment analysis program and applied it to the crypto markets. Lets take a look how it panned out.
permalink: /assets/images/cryptocurrency-sentiment-reddit/
image: /assets/images/disentinel-r-btc.png
tags:
    - cryptocurrency
    - crypto
    - nlp
    - sentiment
    - reddit
---

A few weekends ago, I wrote a Reddit sentiment analysis program and applied it to the crypto markets. This analysis scores only the titles of Reddit posts by users to the following subreddits:

- r/bitcoin
- r/ethereum
- r/bitcoincash
- r/btc
- r/BitMEX
- r/cryptocurrency
- r/litecoin
- r/neo

My goal here was to try to figure out if there is a way to do a fairly simple sentiment analysis that could gauge how people "feel" about various cryptocurrency on Reddit.

#### Tools used

- Python 3.7
- sPacy
- [Liu and Hu opinion lexicon](https://www.cs.uic.edu/~liub/FBS/sentiment-analysis.html)

#### Methodology

It tests the words in the last 100 reddit titles against words in a known corpus of negative or positive sentiment word. I use the Liu and Hu opinion lexicon.

The scoring algo is fairly naive right now. I create a score for each title (the score is initially 0). Then I walk word by word through each title and add 1 the score for the presence of positive word or subtract 1 for score for negative words.

To expand the potential list of dictionary words I compare the word vectors in the title and in the opinion lexicon and if the words have a similarity score of above 75 I consider it positive or negative depending on the word in the dictionary I’m comparing.

### Results

The below are the results from this experiment. If, however, you want to interact with the data you can do so on via built Disentinel. Disentinel is a [cryptocurrency sentiment analysis tool](https://app.disentinel.com?utm_source=jsfour_blog&utm_medium=disentinel_app&utm_campaign=disentinel).

~ 10:00a 9/23

- r/bitcoin POSITIVE score 4.0000
- r/ethereum NEGATIVE sentiment score -6.0000
- r/bitcoincash POSITIVE sentiment score 20.0000
- r/btc NEGATIVE sentiment score -14.0000
- r/BitMEXNEGATIVE sentiment score -37.0000

~ 9:00p 9/23

- r/bitcoin: NEGATIVE sentiment score -18.0
- r/ethereum: NEGATIVE sentiment score -2.0
- r/bitcoincash: NEGATIVE sentiment score -3.0
- r/btc: NEGATIVE sentiment score -39.0
- r/cryptocurrency: NEGATIVE sentiment score -6.0
- r/litecoin: NEGATIVE sentiment score -28.0

~ 10:00a 9/24

- r/bitcoin NEGATIVE score -56.00
- r/ethereum POSITIVE score 1.00
- r/bitcoincash NEGATIVE score -3.00
- r/btc NEGATIVE score -19.00
- r/BitMEX NEGATIVE score -343.00
- r/cryptocurrency NEGATIVE score -73.00
- r/litecoin NEGATIVE score -29.00
- r/neo NEGATIVE score -24.00

~ 3:53 9/25

- r/bitcoin NEGATIVE sentiment score -91.00
- r/ethereum NEGATIVE sentiment score -61.00
- r/bitcoincash NEGATIVE sentiment score -11.00
- r/btc POSITIVE sentiment score 7.00
- r/BitMEX NEGATIVE sentiment score -343.00
- r/cryptocurrency NEGATIVE sentiment score -91.00
- r/litecoin NEGATIVE sentiment score -34.00
- r/neo NEGATIVE sentiment score -26.00
- r/bitcoin titles POSITIVE sentiment score 4.0000

#### Future work

Given the “weekend project” nature of this project, it was a bit of a hack job. Here are some notes on how I would do to improve it.

- It would be nice to see how this sentiment changes over frequent time intervals (and how the changes correlate to the market), so I should start storing data and/or collecting old data
- Ideally the negative/positive sentiment words I test against would be specific to the domain (in this case crypto). So I should compile a domain specific dictionary and rerun it.
- I could do some more pre-processing on data
- Deep learning models could yield interesting results as well. I would need labeled training data for this though which could be hard to collect.
- I would be interested to see how the method could be applied to tweets
- Once I collect more data, it would be interesting to see if this is a leading or lagging indicator

**Disclaimer: I don’t claim that this is a trading signal, this project is just something interesting that I was thinking about and I wanted to share the results. If you do use this to trade trade at your own risk. The above references an opinion and is for information purposes only. It is not intended to be investment advice Seek a duly licensed professional for investment advice.**
