---
layout: post
title: "1v1 risk strategy tutorial"
date: 2014-07-19 03:42:40 +0200
author: <a rel="author" href="https://plus.google.com/117525803180879614771/about">Horea Christian</a>
comments: true
categories: [statistics, gameplay, strategy]
published: false
---

[Risk](https://en.wikipedia.org/wiki/Risk_(game) is a board game from the mid 20th century which has sprouted several variations, including free-to-play internet-based versions (as for instance [Dominating12](), [Conquer Club](http://www.conquerclub.com/), or [MajorCommand](http://www.majorcommand.com/)).
The games offer a wide range of rule variations, including the number of players, the value of bonus cards, the range for end-of-turn reinforcements, and many more.
As the terminology may likewise be inconsistent on occasion, we recommend [this succinct glossary](http://www.dominating12.com/?cmd=tutorial&act=glossary) for general reference. 
While we try to accommodate for rule variations in these instructions, please be aware that they are meant specifically for 2-player (1v1) games (optimal gameplay is *very* different for multiplayer), following the most popular rule set where the attacker may roll up to 3 and the defender up to 2 dice (with the defender winning ties).

<!-- more -->

##Probability

In Risk, single battle outcomes are decided by throwing dice.
This gives the game a higher outcome uncertainty and poses some difficulties for players who do not really understand probability.
You should bear the following concepts in mind:

* *Future odds are not influenced by past outcomes* - bad/good dice just mean that your position has worsened/improved, and should not affect your future roll expectations.
* *The odds (especially for computer-based versions) are unbiased* - you can only become a great player by winning games where your luck was reasonably bad.

Total probabilities for taking over a territory based on the number of attackers and defenders can be calculated with a Markov chain (as for instance in [this paper](http://www4.stat.ncsu.edu/~jaosborn/research/RISK.pdf) or as implemented in [this simulator](http://riskodds.com/index.php)).
That information, however, is mostly irrelevant to a 1v1 game, since you should never auto-attack.
With every attack the state of the game changes, and you should re-evaluate your next move in light of the new state.

Whilst sounding complicated, this actually makes the mathematics of your gameplay easier, as there are a very limited number of scenarios for every attack (6, given a cap of 2 defenders and 3 attackers).
Based on that knowledge you can calculate the odds for each scenario and determine when it is advantageous to attack.

###Dice Odds per Attack 

We use the following notation to represent the probability of the *attacker* obtaining a specific outcome given $a$ attacking troops (ergo $\geq a+1$ troops on the attacking territory) and $d$ defenders:

* Victory: $P(V|(a,d))$
* Tie: $P(T|(a,d))$
* Defeat: $P(D|(a,d))$

#### $(a,d) = (1,1)$

Here calculations become easier since:
$$
P(T|(a,d)) = 0
$$
Further: 
$$
P(V|(a,d)) = \sum\limits_{n=1}^6 \frac{n-1}{6^{2}} = 0.41(6)
$$
Thus:
$$
P(D|(a,d)) = 1 - P(T|(a,d)) - P(V|(a,d)) = 0.58(3)
$$

#### $(a,d) = (2,1)$

$$
\sum\limits_{n=1}^6 \frac{n-1}{6} + \frac{n(6-n)}{6^{2}}
$$

The above calculations are loosely based on [this discussion thread](http://math.stackexchange.com/a/874291/109086). 
