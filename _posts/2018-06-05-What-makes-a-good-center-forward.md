---
layout: post
title: What makes a good goal scorer?
---

The summer transfer window is underway, with the usual glut of clubs looking to improve on the forward options already in their squad. 
This includes my own Leeds, who are involved in a quite public pursuit of Abel Hernandez. formerly of Hull City. Searching  through fan
forums, the inevitable comparisons to Chris Wood are there to be seen, as well as the usual discussion of whether the considerable outlay on Hernandez will be worth it.

Questions such as the rather vague '*is he any good?'*, to the somewhat more analytical '*how clinical is he?*' are posed, however how do we measure these qualities?

In essence, what makes a goal scorer *good*?

If we pose this question with the more traditional view of a center forward in mind (i.e. a player who's primary focus is simply to score) then the answer could be given as a combination of **chance getting**  and **chance taking** ability. Of course, this ignores the offensive contribution of the player outside of goal scoring, but for this analysis, we'll look solely at this quality.

**How can a player's 'chance getting' ability be measured?**

Let's first look at each player's *chance getting* ability, that is to say, their ability to get into goal scoring positions. To measure this we can simply look at each player's expected goals (xG) per game. To do this an expected goals model needs to be constructed, to rate the quality of each chance the players get, i.e. the probability of scoring a goal. The model used is relatively simple and is based on the football events dataset on Kaggle, found [here](https://www.kaggle.com/secareanualin/football-events).

**How can a player's 'chance taking' ability be measured?**

To assess a player's finishing ability, we can look at how their actions influence the probability of a chance being converted to a goal. Given that we know where the player places their shot, how does this differ from the baseline probability calculated by our expected goals model above? A good finisher will aim for parts of the goal which generally increase the probability of a chance being converted. Likewise, a poor finisher will make poor choices, and their likelihood of scoring will be diminished.


Taking all of this into account, the performance of Europe's top goal-getters can be analysed in more detail than looking at simple goal counts. The data shows that between 2011 and 2017, the top performers in terms of xG per game and post shot xG differential are who we would expect them to be, however with noticebale differences between the two top performers. Even the most casual of football fan would know Cristiano Ronaldo to be volume heavy shooter, and this is shown to be the case. He led La Liga in the 15/16 season with 6.3 shots per game, for instance.

![Img1](/images/xg_finishers.png "graph")

Lionel Messi is shown to be a less volumous shooter, with greater finishing ability. Messi is then followed closely in both respects by his Barcelona team-mate Luis Suarez.

Interestingly, Daniel Sturridge is included among the top performers in terms of finishing ability. Given that the data includes the 13/14 season, this is not a surprise and it is interesting to see how his career has diverged from that of Luis Suarez, his strike partner in that period.

Looking at the other end of the scale there are a number of familiar names showing an average reduction in chance conversion likelihood, due to the player's shot placement. Graziano Pelle is by far the worst finisher of those players with xG per game of 0.3 or more. Pierre-Michel Lasogga will be a familiar name to Leeds supporters, and did not live up to the bill of replacing Chris Wood. Personally speaking, an average post shot xG differential of approximately -0.025 for Lasogga is not surprising. 

![Img2](/images/xg_poor_finishers.png "graph")

Coming full circle, at this point, we should be in a position to return to the fan's forum, and answer questions over Abel Hernandez. 

**Is he any good?**

With a post shot xG differential average of 0.001, he is a superior finisher to Lasogga. A comparable xG per game of 0.27 across 60 games means it is easy to make the case that Hernandez would be, at the very least, a significant upgrade on Lasogga. Leeds will be getting a similar player stats-wise, but with far better recent showings. However, whether Leeds can keep him fit remains to be seen.
