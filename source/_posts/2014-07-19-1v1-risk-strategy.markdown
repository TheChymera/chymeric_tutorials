---
layout: post
title: "1v1 risk strategy"
date: 2014-09-18 03:42:40 +0200
author: Horea Christian
googleplus_user: 117525803180879614771
comments: true
categories: [statistics, gameplay, strategy]
published: true
---

[Risk](https://en.wikipedia.org/wiki/Risk_(game)) is a board game, variations of which can also be played online, as for instance on [Dominating12](www.dominating12.com), [Conquer Club](http://www.conquerclub.com/), or [MajorCommand](http://www.majorcommand.com/).
Though the gameplay mechanism is consistent, there are many variations between these websites - occasionally extending even to the rule terminology.
As a general reference therefor we would recommend the succinct [Dominating12 terminology glossary](http://www.dominating12.com/?cmd=tutorial&act=glossary).

While we try to accommodate for rule variations in the following instructions, please be aware that they are meant specifically for 2-player (1v1) games (optimal gameplay is *very* different for multiplayer games).
We follow the most popular battle mechanism, where the attacker rolls up to 3 and the defender up to 2 dice (with the defender winning ties).
Our notation for attack configurations is **AvD**, with **A** being the number of attackers (troops on the attacking territory minus one) and **D** being the number of defenders (total troops on the defending territory).

<!-- more -->

##Probability

In Risk, single battle outcomes are decided by random events (roll of the dice) best thought of in terms of probability.
While as much seems obvious, players should make sure to understand that:

* *Future odds are not influenced by past outcomes* - bad/good dice just mean that your position has worsened/improved, and should not affect your future roll expectations.
* *The odds (especially for computer-based versions) are unbiased* - you can only become a great player by winning games where your luck was reasonably bad.

Total probabilities for taking over a territory - based on the total number of attacking and defending troops - can be determined via a Markov chain (as for instance in [this paper](http://www4.stat.ncsu.edu/~jaosborn/research/RISK.pdf)) or via a Monte Carlo simulation.
That information, however, is mostly irrelevant in a 1v1 game, since you should never auto-attack.
With every attack the state of the game changes, and you should always re-evaluate your next move in light of the new state.

Whilst sounding complicated, this actually makes the mathematics of your gameplay easier, as there are a very limited number of scenarios for every attack (6 scenarios in total - given the aforementioned battle cap of 2 defenders and 3 attackers).
Based on that knowledge you can calculate the odds for each scenario and determine when it is advantageous to attack.[This article](http://chymeric.eu/blog/2014/07/23/per-attack-risk-dice-odds/) demonstratively calculates the odds for all single-attack configurations and and presents a summary table. 

##Troop Placement
The [single-battle odds table](http://chymeric.eu/blog/2014/07/23/per-attack-risk-dice-odds/) shows that the optimal attack configurations are those with the maximum number (3) of attacking units.
The [compound odds table](http://www4.stat.ncsu.edu/~jaosborn/research/RISK.pdf) allows us to compare the victory odds for alternative troop placements.
Based on this information, you should:

####PR1 - Avoid reinforcing territories containing less than 3 troops
Unless otherwise strategically mandated, reinforcing territories that contain only 1 or 2 troops is a poor move - as you will thus deprive yourself of using 1 or even 2 of your troops in an optimal attack configuration.

####PR2 - Split troops between territories
This might indeed sound counterintuitive, but based on data from the aforementioned compound odds table, two attack scenarios starting with **3v3** each are more advantageous than one attack scenario starting with **4v3**.
Keep in mind that as per our notation e.g. **3v3** means 4 troops on the attacking territory and 3 on the defending territory.
Regarding this demonstrative calculation's probability notation refer to [this page](http://chymeric.eu/blog/2014/07/23/per-attack-risk-dice-odds/):

$$
\Pr(V\vert(3,3),(3,3)) \approx 0.47+0.47(1-0.47) \approx 0.719
$$

$$
\Pr(V\vert(4,3)) \approx 0.642
$$

Also, keep in mind that the added benefit of splitting troops instead of placing them on the same territory decreases as the number of placeable troops goes up.

####PR3 - Reinforce regions connected to multiple enemy territories
Since you will want to attack in all cases where you have 3 available attackers (see next section), place your troops in a way that allows you to make optimal use of favorable outcomes -
as for instance by allowing you to attack a further territory if you have enough troops left after conquering your initial target.
Probability tells us that you can and will get "lucky" - it is important to put yourself in a position where you can make best use of good fortune.

##Attack

The [single-battle odds table](http://chymeric.eu/blog/2014/07/23/per-attack-risk-dice-odds/) shows that it is always advantageous to attack in **3v1**, **2v1**, and **3v2** configurations. 
It follows that you should:

####AR1 - Attack if you have 4 or more troops on a territory
Even if the adversary has more defenders than you have attackers, it is still beneficial to attack until your troop count in the attacking territory is close to 3.
This is not necessarily in the hope of conquering his territory (though for troop counts exceeding **15v16**, this might actually be the case - as shown [here](http://www4.stat.ncsu.edu/~jaosborn/research/RISK.pdf)).
It might *seem* like you are weakening your defense, but in fact your troops are more efficient at causing attrition in your opponent's ranks ranks if used for an attack rather than kept for "defense".

####AR2 - Attack exposed 1-troop territories
The most favorable attack scenarios are **3v1** and **2v1**.
If you find yourself presented with such an attack opportunity, do not miss it!
This is an excellent opportunity to erode you adversary's total troop and territory count.
An exception to this rule may be made for AR3:

####AR3 - Avoid attacking territories next to large stacks
Optimizing your attack opportunities is on par with containing the opponent's opportunities.
If for some reason your opponent has large troop stacks (more than 4) in a territory not adjacent to any of yours (e.g. to protect a bottleneck), avoid attacking the adjacent territories if you cannot reasonably expect to also neutralize the threat of the stack.
By doing this you will deprive him of the use of a large number of troops come next round.
Otherwise the next round will find you faced with an attack force you may not be apt to defend yourself from.

##Reinforcements

As previously discussed, **3v1** and **2v1** attack configurations are very favorable to the attacker.
So is, in fact, **3v2** - but **3v2** battle events can, however, not be averted in the reinforcement phase (they can be averted in the attack phase, as seen in AR1).
Key concepts for reinforcement include:

####RR1 - Do not leave exposed 1-troop territories
Troops left alone on a territory get high attrition during the adversary's attacks - meaning that you not only cannot hold the respective territory, you are also wasting the unit.

####RR2 - Reinforce bottlenecks
Bottlenecks (territories which control access into regions otherwise inaccessible) provide an excellent means to make sure as many as your troops as possible will be attacked in a **3v2** scenario -
which is the most advantageous configuration you can have against an informed attacker.
The advantages of reinforcing a bottleneck can outweigh RR1, though it is best to keep both these rules in mind during the attack phase - so that you will not be forced to chose.

####RR3 - Keep large armies close to the enemy
Since you do not want to start the next round with unusable troops, it is advisable to place your troops where they will be able to attack from.
This includes not only the enemy lines, but also territories next to other territories the enemy is likely to attack - for example a neutral territory which he needs to get a bonus.

##Bonuses
Some regions, as well as a certain number (commonly 3) of controlled territories give troop bonuses.
We shall be referring to these as regional and territorial bonuses respectively.

####BR1 - Always try to break bonuses
In a sense, a unit lost for the enemy is a unit gained for you.
Breaking bonuses is the best way to weaken your enemy's position, and you should let that high payoff come into play when deciding whether an attack is desirable.
In general you should go beyond your usual attack configuration comfort zone when trying to break a bonus. 
However, breaking a bonus is not worth losing more troops than the value of the bonus.

####BR2 - do not be over-zealous in getting bonuses
You should definitely try to get bonuses, but always ask yourself whether you can afford them.
Regional bonuses in particular introduce a potential (and obvious) weakness in your position.
You should also only attack neutrals to get a bonus, if you are sure you can hold it enough rounds to account for *both* the troops you lost attacking them *and* the troops the enemy did not lose while he was not being attacked.

##Cards
Some Risk variations allow you to turn in cards (received for every taken turn where you conquered a territory) to get a fixed or incremental number of units.
Cards can be of any of 3 different types (e.g. "colors") or they can be "wildcard" (usable as any type) - and you need 3 cards of the same type or 1 of each type to turn them in.

####CR1 - In incremental turn-in games, turn in as late as possible
This rationale also means that if you get the first turn in an incremental turn-in game, you can comfortably afford to fail conquering a territory during one round.
Pretty obvious, you want as many troops as you can get. 
However, an exception should be made for cases where the damage you cause to the enemy by an immediate turn in (e.g. breaking a 5-unit bonus) outweighs the number of additional units (e.g. 2) you would have received turning in later.

####CR2 - In fixed turn-in games, turn in as early as possible
In fixed turn-in scenarios, there is no cost associated with turning in earlier, you do, however, still get the benefit of breaking territorial or regional bonuses.
Additionally, you can take advantage of the adversary not (yet) having cards to turn in, and thus no means to undo the damage you have done. 




