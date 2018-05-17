---
layout: post
title: Soccermatics odds-bias strategy in Irish league football
---

In his book, Soccermatics, Prof. David Sumpter uses a betting strategy which he calls his 'odds-bias' strategy. This involves looking at the implied probability of bookmakers' odds, relative to the observed frequency with which these events occur. In the book, biases in the odds of strong home favourites and well matched draws are identified in the English Premier League, and a profit is made. The question is, can this be applied to other leagues, and can it be refined?

A logistic regression model is used to map the odds we have found to be biased onto, hopefully, more accurate ones. A dataset from League of Ireland football was used. The graphs below show similar biases to those presented in the book, although none are found in the odds of a draw.

![Img3](/images/HomeWinsLOI.png "HW")
![Img4](/images/DrawsLOI.png "D")

The above shows that from 2012 to present, home favourites with odds of less that 1.25 have won more often than the odds suggest. This forms the basis of the below strategy.

A logistic regression model was used as described above, to come up with more accurate likelihoods, along with the Kelly staking strategy. The model and strategy were then applied to the past two seasons worth of data.

![Img2](/images/Bank_GameNo1.png "Bank roll over time")

If it's assumed that the bias found in the odds does not change over the time the dataset covers, the strategy can be simulated on multiple test portions of the data. This was done 5,000 times, to get an accurate picture of the distribution of returns. The histogram below gives just a 6% chance of the strategy's return being below zero, with an average return of 55%.

![Img2](/images/ReturnsDist.png "Returns")

