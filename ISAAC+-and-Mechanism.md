# ISAAC+ and Mechanism

## ISAAC+ vs. PBFT

ISAAC+ is based on tranditional *PBFT*. The basic rules of *PBFT* are,

* Consensus can be reached through the majority of voting
* Each round(or view) has leader and it propose the next block
* Each node can validate and vote the next block of leader

ISAAC+ is also based these rules and has some additional rules,

* Consensus can be reached through the majority of voting
* Each round has proposer(leader) and it propose proposal(the transactions for next block)
* Each node can validate the proposal and vote the state result of proposal
* If active round is failed to get agreement, goes to next round
* To start new round, all the nodes in *Validator Group* should agree to INIT ballot
* If failed to agree to INIT ballot, next round will be initialized to 0

Like *PBFT*, the recommended agreement threshold within *Validator Group* is at least 67%.

## Limitations

TODO

## Detailed Consensus Mechanism

In the next, the detailed consensus mechanisms will be explained. For simple explanation, we assume the simple node network,

* 4 nodes: one faulty node can be possible(according to `3f+1` rule)
    - `[N₀ N₁ N₂ N₃]`
* All the nodes is the node of *Consensus Group* and *Validator Group*
    - *Consensus Group*: `[N₀ N₁ N₂ N₃]`
    - *Validator Group*: `[N₀ N₁ N₂ N₃]`
* Every node can receive the transactions from outside of the network
* ~~All the nodes has same block state: `BL0`~~
* Each node is very closely connected with the others: low network latency

<dl>
  <dt>
  
  *Faulty Node*:
  
  </dt>
  <dd>

Faulty node is the failed or non-functioning node to the other nodes. This node,

* Can be crashed,
* Has the different states to other nodes,
* reponses teh different acts to other nodes
  </dd>
</dl>
