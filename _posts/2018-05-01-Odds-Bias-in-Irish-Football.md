---
layout: post
title: Soccermatics odds-bias strategy in Irish league football
---

In his book Soccermatics: Mathematical Adventures in the Beautiful Game, David Sumpter trials a number of gambling strategies on English Premier League football.

Of these, success was found using what was termed as the 'odds-bias' strategy. 

In his book, Prof. Sumpter fits a logistic regression model to estimate the 'true' odds, based on the odds offered by bookmakers. Prior to this he identifies some biases in the probabilities implied by bookies' odds, and the frequency with which these events occur. In doing this, an opportunity to make value bets was identified.

The overall strategy was as follows:

For games where the win probablitlies based on bookmakers' odds was greater than 40% in favour of the home side, a bet was placed on a home win.

For games where this differential was less than 15%, a bet was placed on a draw.

First, let's apply this strategy to League of Ireland football. I'll create a logistic regression for home wins and draws, using the 2012 - 2016 seasons as training data. This wil form the basis for a strategy applied to games from 2017 to date.

Below is a graph of the Soccermatics odds-bias strategy returns over time, with a starting bankroll of $1000.

![alt text][br]


[br]: https://github.com/andrewwoods1/andrewwoods1/images/Bank_GameNo.png "Bank roll over time"
