---
layout: post
title: "1v1 risk strategy tutorial"
date: 2014-07-19 03:42:40 +0200
author: Horea Christian
googleplus_user: 117525803180879614771
comments: true
categories: [statistics, gameplay, strategy]
published: false
---

[Risk](https://en.wikipedia.org/wiki/Risk_(game) is a board game available in many variations, including free-to-play internet-based versions (as for instance [Dominating12](), [Conquer Club](http://www.conquerclub.com/), or [MajorCommand](http://www.majorcommand.com/)).
Though the gameplay mechanism is consistent, there are many variations between these websites - occasionally extending even to the rule terminology.
As a general reference therefore we would recommend the succinct [Dominating12 terminology glossary](http://www.dominating12.com/?cmd=tutorial&act=glossary).
While we try to accommodate for rule variations in the followinginstructions, please be aware that they are meant specifically for 2-player (1v1) games (optimal gameplay is *very* different for multiplayer).
We also follow the most popular battle mechanism set where the attacker rolls up to 3 and the defender up to 2 dice (with the defender winning ties).

<!-- more -->

##Probability

In Risk, single battle outcomes are decided by random events best thought about in terms of probability.
While as much seems obvious, many Risk players should bear the following concepts in mind:

* *Future odds are not influenced by past outcomes* - bad/good dice just mean that your position has worsened/improved, and should not affect your future roll expectations.
* *The odds (especially for computer-based versions) are unbiased* - you can only become a great player by winning games where your luck was reasonably bad.

Total probabilities for taking over a territory based on the number of attackers and defenders can be calculated with a Markov chain (as for instance in [this paper](http://www4.stat.ncsu.edu/~jaosborn/research/RISK.pdf) or as (not very accurately) implemented in [this simulator](http://riskodds.com/index.php)).
That information, however, is mostly irrelevant in a 1v1 game, since you should never auto-attack.
With every attack the state of the game changes, and you should re-evaluate your next move in light of the new state.

Whilst sounding complicated, this actually makes the mathematics of your gameplay easier, as there are a very limited number of scenarios for every attack (6 scenarios in total - given the aforementioned battle cap of 2 defenders and 3 attackers).
Based on that knowledge you can calculate the odds for each scenario and determine when it is advantageous to attack.

##Opti


