---
layout: post
title: Soccermatics odds-bias strategy in Irish league football
---

In his book Soccermatics: Mathematical Adventures in the Beautiful Game, David Sumpter trials a number of gambling strategies on English Premier League football.

Of these, success was found using what was termed as the 'odds-bias' strategy. 

Prof. Sumpter fits a logistic regression model to estimate the 'true' odds, based on the odds offered by bookmakers. Prior to this he identifies some biases in the probabilities implied by bookies' odds, and the frequency with which these events occur. In doing this, an opportunity to make value bets was identified.

The overall strategy was as follows:

For games where the win probablitlies based on bookmakers' odds was greater than 40% in favour of the home side, a bet was placed on a home win.

For games where this differential was less than 15%, a bet was placed on a draw.

First, let's apply this strategy to League of Ireland football. I'll create a logistic regression for home wins and draws, using the 2012 - 2016 seasons as training data. 
![Img1](/images/Odds_Prob_Soccermatics.png "Logistic model fit")

This will form the basis for a Kelly strategy applied to games from 2017 to date. 

Below is a graph of the Soccermatics odds-bias strategy returns over time, with a starting bankroll of $1000.

![Img2](/images/Bank_GameNo.png "Bank roll over time")

At game 141 our bank roll takes a major hit. Here we placed a bet on Cork City to win at home versus Bohemians, who despite being priced on average at 12.19 came away with a win. The strategy performs moderately well over the course of two seasons, however can this be improved, looking at the data at hand?

On closer inspection of the strategy, not once was a draw bet placed over the two seasons. The plots below show that as in the Premier League, biases can be found in the prices given for home favourites, but this bias is not present for draws. As mentioned in the original book, punters usually prefer to side with one team over the other rather than back a draw, possibly because they support one the teams.
A possible explanation for this bias not being present in our data is that this is a minor league and thus the biases fans have when betting on their teams is not present.  Draw bets were removed from our strategy. Biases can be seen in the home win odds, from 80% likelihood and up.

![Img3](/images/HomeWinsLOI.png "HW")
![Img4](/images/DrawsLOI.png "D")

The refined strategy was then applied, placing bets using our logistic model, from roughly 2013 to present. This turned a profit, as seen below.

To further test the startegy, it was run again and again on different parts of the data. 75% was selected randomly to be used as training data, using the other 25% for testing. Of course, we're making a key assumption here, that the order in which results came in does not matter in the context of the apparent bises in the odds, and that these biases are the same throughout our dataset.

Having run the strategy 5000 times, the distribution of returns was found, and as below shows, the strategy almost always made a profit.
