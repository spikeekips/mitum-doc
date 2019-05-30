# BFT: Byzantine Faulty Tolerance


## The Two generals Problem


> This problem (first published in 1975 and given its name in 1978, [SOME CONSTRAINTS AND TRADEOFFS IN THE DESIGN OF NETWORK COMMUNICATIONS](http://hydra.infosys.tuwien.ac.at/teaching/courses/AdvancedDistributedSystems/download/1975_Akkoyunlu,%20Ekanadham,%20Huber_Some%20constraints%20and%20tradeoffs%20in%20the%20design%20of%20network%20communications.pdf)) describes a scenario where two generals are attacking a common enemy.
>
> There is no way to guarantee the second requirement that each general be sure the other has agreed to the attack plan. Both generals will always be left wondering whether their last messenger got through.
>
> \- [Understanding Blockchain Fundamentals, Part 1: Byzantine Fault Tolerance](https://medium.com/loom-network/understanding-blockchain-fundamentals-part-1-byzantine-fault-tolerance-245f46fe8419)


## The Byzantine Generals Problem

> Famously described in [1982 by Lamport, Shostak and Pease](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.126.9525&rep=rep1&type=pdf), it is a generalized version of the Two Generals Problem with a twist. It describes the same scenario, where instead more than two generals need to agree on a time to attack their common enemy. The added complication here is that one or more of the generals can be a traitor, meaning that they can lie about their choice (e.g. they say that they agree to attack at 0900 but instead they do not).
>
> \- [Understanding Blockchain Fundamentals, Part 1: Byzantine Fault Tolerance](https://medium.com/loom-network/understanding-blockchain-fundamentals-part-1-byzantine-fault-tolerance-245f46fe8419)


## Byzantine Generals Problem.

> A commanding general must send an order to his n - 1 lieutenant generals such that
>
> IC1. All loyal lieutenants obey the same order.
>
> IC2. If the commanding general is loyal, then every loyal lieutenant obeys the order he sends.
>
> \- [The Byzantine Generals Problem](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.126.9525&rep=rep1&type=pdf)

## Phases

* (*REQUEST*)
* *PRE-PREPARE*
* *PREPARE*
* *COMMIT*
* (*REPLY*)
