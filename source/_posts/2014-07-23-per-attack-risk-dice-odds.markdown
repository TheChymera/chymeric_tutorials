---
layout: post
title: "per-attack risk dice odds"
date: 2014-07-23 02:22:35 +0200
author: <a rel="author" href="https://plus.google.com/117525803180879614771/about">Horea Christian</a>
comments: true
categories: [statistics, gameplay, strategy]
published: true
---

In [Risk](https://en.wikipedia.org/wiki/Risk_(game))-like games, players face off against each other on maps divided into territories.
One player may conquer the territories of another by eliminating all of the other's units from a said territory.
Units can be eliminated with the throwing of the dice, and a unit is lost for every instance where the opposing player has a higher score on one cast die.
The throwing of the die is governed by the following rules:

* Defenders throw up to 2 dice, they have $\geq 2$ units on the attacked territory.
* Attackers throw up to 3 dice, if they have $\geq 3+1$ units on the attacking territory.
* Only the top dice are considered if a player throws more dice than his opponent.
* Dice are paired with each other in an ordinal fashion.

There are already texts providing more wide-ranging whole-battle predictions (as for instance [here](http://www4.stat.ncsu.edu/~jaosborn/research/RISK.pdf)), and closed-source [battle simulators](http://riskodds.com/).
Here we try to offer a transparent formulaic reference and odds table for all single-attack scenarios. 

<!-- more -->

##Notation

We use the following notation to represent the probability of the *attacker* obtaining a specific outcome given $a$ attacking units (ergo $\geq a+1$ troops on the attacking territory) and $d$ defending units:

* Victory: $\Pr(V\vert(a,d)) $
* Tie: $\Pr(T\vert(a,d))$
* Defeat: $\Pr(D\vert(a,d))$

##Scenarios

Given a cap of 2 defenders and 3 attackers we can expect $2 \times 3$ attack scenarios, which we shall be listing according to the value of $(a,d)$:

### (1,1)

Here calculations become easier since there is no possibility of a tie:
$$
\Pr(T|(a,d)) = 0
$$
Further we sum the probabilities of the attacker winning contingent on the 6 possible and equally probable defender die outcomes:
$$
\Pr(V|(a,d)) = \frac{1}{6}\sum_{n=1}^6 \frac{6-n}{6} = 0.41(6)
$$
Thus:
$$
\Pr(D|(a,d)) = 1 - \Pr(T|(a,d)) - \Pr(V|(a,d)) = 0.58(3)
$$

### (2,1)

As before, there is no possibility of a tie, and we account for the $\left(1-\frac{6-n}{6}\right)\frac{6-n}{6}$ probability that one die loses but the second one wins.

$$
\Pr(V|(a,d)) = \frac{1}{6}\sum_{n=1}^6 \left( \frac{6-n}{6} + \frac{n}{6} \cdot \frac{6-n}{6} \right) = \frac{1}{6}\sum_{n=1}^{6} \frac{6^2-n^2}{6^2} = 0.578(703)
$$

Thus:
$$
\Pr(D|(a,d)) = 1 - \Pr(T|(a,d)) - \Pr(V|(a,d)) = 0.421(296)
$$

### (3,1)

Similarly we solve for $(a,d)=(3,1)$, where a tie is again impossible and there is an added probability that two dice lose but the third one wins.

$$
\Pr(V|(a,d)) = \frac{1}{6}\sum_{n=1}^6 \left( \frac{6^2-n^2}{6^2} + \left(\frac{n}{6}\right)^2 \cdot \frac{6-n}{6} \right) = \frac{1}{6}\sum_{n=1}^{6} \frac{6^3-n^3}{6^3} = 0.6597(2)
$$

Thus:
$$
\Pr(D|(a,d)) = 1 - \Pr(T|(a,d)) - \Pr(V|(a,d)) = 0.3402(7)
$$

### (2,1)

Here we take one dice of the defender (of value $n$) as the minimum a requirement for a victorious attacker and adjust the probability for the cases where a second die (value $m$) receives a higher value.
Again, there can be no tie.

$$
\Pr(V|(a,d)) = \frac{1}{6^2}\sum_{n=1}^6 \left( (n-1)\frac{6-n}{6} + \sum_{m=n}^6 \frac{6-m}{6} \right) = 0.25462(962)
$$  

Thus:
$$
\Pr(D|(a,d)) = 1 - \Pr(T|(a,d)) - \Pr(V|(a,d)) = 0.7453(703)
$$

### (2,2); (2,3)

For more complex cases determining the odds becomes a far more non-uniform probability problem.
While we are still looking out for a formulaic solution, we currently solve these cases via a (significantly slower) exhaustive lookup of all possible combinations.

## Script

Based on the above we have written [a Python script (named **Risky**)](https://github.com/TheChymera/Risky) that can be used to calculate the voctory, tie, and defeat odds given $a$ attackers, $d$ defenders, and $s$ sides of the dice.
For a more exghaustive documentation of how to *use* the script from the command line please consult [its README document](https://github.com/TheChymera/Risky/blob/master/README.md).
The calculations are done preferentially based on the general formulas for the respective aforementioned cases:

### General Formulae 

For $ a \in \mathbb{N}$ and $b=1$:

$$
\Pr(V|(a,d)) = \sum_{n=1}^{s} \frac{s^a-n^a}{s^{(a+1)}}
$$

For $a=1$ and $b=2$:

$$
\Pr(V|(a,d)) = \frac{1}{6^2}\sum_{n=1}^6 \left( (n-1)\frac{6-n}{6} + \sum_{m=n}^6 \frac{6-m}{6} \right)
$$

###Exhaustive Lookup

In case no formula is defined for the specified number of attackers and defenders, the script defaults to a subroutine which populates an array with all the possible dice outcome combinations and looks up combinations meeting the respective (victory, defeat, and tie) criteria.
One should note that this method can also be used as a validation tool for formulaic calculations, but is significantly slower. 

##Odds Table

For ease of overview we have compiled a table with all the odds (victory, tie. defeat) of a single attack in the common Risk set-up (6-sided dice and a cap of 3 attackers and 2 defenders). 

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;border:none;margin:0px auto;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:0px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:0px;overflow:hidden;word-break:normal;}
.tg .tg-2thk{background-color:#c0c0c0;text-align:center}
.tg .tg-skfc{background-color:#dedede;color:#000000;text-align:center}
.tg .tg-3ka8{background-color:#fbc6ea;color:#000000;text-align:center}
.tg .tg-be7o{font-weight:bold;background-color:#efefef;color:#656565}
.tg .tg-v8r2{background-color:#cfcfcf;color:#000000;text-align:center}
.tg .tg-cqq2{font-weight:bold;background-color:#656565;color:#efefef;text-align:center}
.tg .tg-f1qn{font-weight:bold;background-color:#efefef;color:#656565;text-align:right}
.tg .tg-c8xk{background-color:#f9a4de;text-align:center}
.tg .tg-g7zu{background-color:#f788d4;color:#000000;text-align:center}
.tg .tg-qems{background-color:#c0c0c0;color:#000000;text-align:center}
.tg .tg-a3ry{background-color:#f788d4;text-align:center}
.tg .tg-m5ue{background-color:#cfcfcf;text-align:center}
.tg .tg-gf1w{background-color:#fbc6ea;text-align:center}
.tg .tg-j518{background-color:#dedede;text-align:center}
</style>
<table class="tg">
  <tr>
    <th class="tg-cqq2">a</th>
    <th class="tg-cqq2" colspan="2">1</th>
    <th class="tg-cqq2" colspan="2">2</th>
    <th class="tg-cqq2" colspan="2">3</th>
  </tr>
  <tr>
    <td class="tg-cqq2">d</td>
    <td class="tg-cqq2">1</td>
    <td class="tg-cqq2">2</td>
    <td class="tg-cqq2">1</td>
    <td class="tg-cqq2">2</td>
    <td class="tg-cqq2">1</td>
    <td class="tg-cqq2">2</td>
  </tr>
  <tr>
    <td class="tg-f1qn">V</td>
    <td class="tg-c8xk">41.67%</td>
    <td class="tg-g7zu">25.46%</td>
    <td class="tg-v8r2">57.87%</td>
    <td class="tg-3ka8">22.76%</td>
    <td class="tg-qems">65.97%</td>
    <td class="tg-skfc">37.17%</td>
  </tr>
  <tr>
    <td class="tg-f1qn">T</td>
    <td class="tg-c8xk">0%</td>
    <td class="tg-g7zu">0%</td>
    <td class="tg-v8r2">0%</td>
    <td class="tg-3ka8">44.83%</td>
    <td class="tg-qems">0%</td>
    <td class="tg-skfc">29.26%</td>
  </tr>
  <tr>
    <td class="tg-f1qn">D</td>
    <td class="tg-c8xk">58.33%</td>
    <td class="tg-g7zu">74.54%</td>
    <td class="tg-v8r2">42.13%</td>
    <td class="tg-3ka8">32.41%</td>
    <td class="tg-qems">34.03%</td>
    <td class="tg-skfc">33.58%</td>
  </tr>
  <tr>
    <td class="tg-be7o">V-D</td>
    <td class="tg-c8xk">-16.66%</td>
    <td class="tg-a3ry">-49.08%</td>
    <td class="tg-m5ue">15.74%</td>
    <td class="tg-gf1w">-9.65%</td>
    <td class="tg-2thk">31.94%</td>
    <td class="tg-j518">3.59%</td>
  </tr>
</table>
<br>


"V" stands for victory odds, "T" for tie odds, "D" for defeat odds, "a" for attacking units, and "d" for defending units.
We have also added "V-D" as an indicator of attack configuration desirability from the point of view of the attacker (though attack desirability is also contingent on strategical context, which is not accounted for here).
Undesirable attack configurations are highlighted in pink.

---
<sup>Browse the history of this file *or* find static versions to cite via [its GitHub page](https://github.com/TheChymera/chymeric_tutorials/blob/master/source/_posts/2014-07-23-per-attack-risk-dice-odds.markdown)!</sup>
