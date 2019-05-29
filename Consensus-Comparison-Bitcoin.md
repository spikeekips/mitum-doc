# Bitcoin

## How does Bitcoin solves byzantine problem?

> The Proof of Work algorithms is a probabilistic solution to the Byzantine General's problem in the case where traitorous generals represent strictly less than 50% of the generals.
>
> To simplify, the main thing a solution to this problem has to guarantee is that all honest generals (honest miners) agree on the same thing.
>
> Let's assume there are 10 miners in the Bitcoin blockchain and a new transaction comes in. This transaction (noted tr1) is broadcasted among all miners. 10 of those miners are traitorous and they broadcast another transaction (noted tr2) where they changed the recipient in tr1. Each miner will starts to solve a puzzle just after he received his first transaction message. Some will receive tr1 first, others will receive tr2 first.
>
> The puzzle is difficult enough that, on average, a solution will be found every 10 minutes. After 10 minutes, miner M solves the proof of work problem. He broadcasts his solution to the 9 other miners and includes in there the transaction he received first. Upon receiving this solution, each miner adjusts his transaction to the new one received. They then all work on the next puzzle. After 1 hour, the chain has 6 blocks (6 puzzles solved). Each general can evaluate how much CPU was necessary to get solve 6 puzzles in 10 minutes. Each general knows then if the majority of the general contributed to building this chain. If the answer is yes, then they agreed on the transaction inside the initial block of this chain.
>
> \- [Does Bitcoin Blockchain solves Byzantine General Problem?](https://bitcoin.stackexchange.com/questions/71547/does-bitcoin-blockchain-solves-byzantine-general-problem)


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


> Byzantine Generals Problem. A commanding general must send an order to his n - 1 lieutenant generals such that
>
> IC1. All loyal lieutenants obey the same order.
>
> IC2. If the commanding general is loyal, then every loyal lieutenant obeys the order he sends.
>
> \- [The Byzantine Generals Problem](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.126.9525&rep=rep1&type=pdf)

## POW: Proof of Work

Blockchains use consensus algorithms to elect a leader who will decide the contents of the next block by POW.

> Proof of Stake takes away the energy and computational power requirement of PoW and replaces it with stake. Stake is referred to as an amount of currency that an actor is willing to lock up for a certain amount of time. In return, they get a chance proportional to their stake to be the next leader and select the next block. There are various existing coins which use pure PoS, such as Nxt and Blackcoin.
> 
> \- [Understanding Blockchain Fundamentals, Part 2: Proof of Work & Proof of Stake](https://medium.com/loom-network/understanding-blockchain-fundamentals-part-2-proof-of-work-proof-of-stake-b6ae907c7edb)

## Nothing At Stake Problem


> If he picks only one chain, he risks losing the transaction fees on the orphaned chain.
>
> However, If he picks both chains, he simply has to wait for one of the chains to be picked as a winner – and he gets his rewards either way.
>
> \- [Nothing At Stake Problem – A Forkin’ Mess!](https://www.mangoresearch.co/casper-nothing-at-stake-problem/)

