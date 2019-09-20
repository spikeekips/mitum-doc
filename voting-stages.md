# Voting Stages

The voting stages was already explained briefly. At this section, more details will be described.

In mitum, there are 3 voting stages, *INIT*, *SIGN* and *ACCEPT*. These have very similar role with classic PBFT. The voting flows thru stages:

```
INIT -> SIGN -> ACCEPT
```

Strictly to say, there is one more important step between *INIT* and *SIGN*, that is *Proposal*.

```
INIT -> Proposal -> SIGN -> ACCEPT
```

Except proposal, voting occurs and then consensus process moves to next stage when the voting result reaches to majority(over voting *threshold*).

## INIT Stage For Suffrage Group

The first step of consensus starts at *INIT* voting. Unlike the other stages all the suffrage group members(`m0`, ... , `m9`) votes at this stage. *INIT* stage has important features:

* Finally establishing the next block of the previously proposed proposal.
* Making agreement for next block
* Making agreement for new round

The ballot for *INIT* stage has several informations:

* New block
* Round of new block(previous voting)
* Next round

*INIT* voting is finished, this means, network gets agreement on the next block and new round. Node can select acting suffrage group members for next block and new round.

When *INIT* voting is finished, the new proposer of newly selected acting suffrage group should propose new proposal for next block to the entire network.

{% hint style="info" %}
Node is booted and previous block is already established. Does *INIT* ballot should contain new block and previous round information?

TL;DR Yes. Basically *INIT* stage works for verifying the previous voting result and finally establishing it. If previous voting is already established, the new block and it's round information will be used the new starting round is based on the valid block or not.
{% endhint %}

## Proposal

Proposal is proposed by proposer, which is selected node from acting suffrage group. Proposal has these information:

* Next block
* Next round
* Messages for next block

Block is the result of validating proposal, so suffrage group members will validate proposal.

If proposal is not received:

* Node in the suffrage group waits the proposal from the proposer for the given time.
* Node does not receive the expected proposal.
* Node will start new round.
* In the new round, the another acting suffrage group and another proposer will be selected.

If proposal is received, but invalid:

* Node in the suffrage group receives the expected proposal.
* But it has some problems:
    * Proposal message is not well-formatted, or
    * The informations of proposal is not correct, or
    * Messages in the proposal is not valid, etc.
* Node will start new round.

Non-intact proposer will be evaluated also as faulty node by the suffrage group.

## Stages For Acting Suffrage Group

*SIGN* and *ACCEPT* stage is done by acting suffrage group, not by suffrage group.

Even if acting suffrage group fails to get agreement at *SIGN* or *ACCEPT*, the consensus process keeps going. The agreement of suffrage group decides the next block, not by one of acting suffrage group.

For example,

* acting suffrage group members: `m0`, `m1`, `m2`, `m3`
* proposer: `m0`
* threshold for majority: 3 of 4
* proposal: `P0`

Voting for the round, `R0`

| node | stage | block |
| ---- | ---- | ---- |
| `m0` | *SIGN* | `H0` |
| `m1` | *SIGN* | `H0` |
| `m2` | *SIGN* | `H1` |
| `m3` | *SIGN* | `H1` |

This *SIGN* voting fails to get agreement,
* `H0`: `m0`, `m1`; under threshold 3
* `H1`: `m2`, `m3`; also under threshold 3

No hash failed to be over threshold(3). With this voting result, they moves to the next stage, *ACCEPT*:

| node | stage | block |
| ---- | ---- | ---- |
| `m0` | *ACCEPT* | `H0` |
| `m1` | *ACCEPT* | `H0` |
| `m2` | *ACCEPT* | `H1` |
| `m3` | *ACCEPT* | `H1` |

Even if getting agreement failed. Why acting suffrage members moves to *ACCEPT*?	In ISAAC+, the agreement failure inside acting suffrage group does not mean the agreement failure of entire network. As described earlier, acting suffrage group exists for proposing proposal and verifying the ability and health of node continuously. The voting of acting suffrage group will be evaluated by all the suffrage group members and if some node be thought as faulty node, it will be handled by network policy and rule.

After *ACCEPT* stage is finished, the next *INIT* stage will be like this;

| node | stage | block |
| ---- | ---- | ---- |
| `m0` | *INIT* | `H0` |
| `m1` | *INIT* | `H0` |
| `m2` | *INIT* | *`H1`* |
| `m3` | *INIT* | *`H1`* |
| `m4` | *INIT* | `H0` |
| `m5` | *INIT* | `H0` |
| `m6` | *INIT* | `H0` |
| `m7` | *INIT* | `H0` |
| `m8` | *INIT* | `H0` |
| `m9` | *INIT* | *`H1`* |

The result of voting:

* `H0`: `m0`, `m1`, `m4`, `m5`, `m6`, `m7`, `m8`
* `H1`: `m2`, `m3`, `m9`

`H0` gets votes over threshold, 7 in the suffrage group

{% hint style="info" %}
The threshold, 7 is different from 3, threshold of acting suffrage group, why?

The default threshold percent is 67%, this means at least 2/3 nodes should agree on the same result. The 7 is 67% of the number of all the suffrage group members.
{% endhint %}


The suffrage group agreed on `H0` and `H0` will be established as the new block, and then newly selected acting suffrage group will start new round for next block.

### SIGN

After agreement of *INIT* stage, consensus process moves to *SIGN* stage. The voting at this stage is on the proposal for the next block. Basically proposal has the contents of the next block, so node checks and validates the content of proposal. Each node can produce the next block from proposal and vote by the produced next block.

The ballot for *SIGN* stage has these informations:

* Latest block
* Round
* Proposal
* Next block

When same next blocks from *SIGN* ballots reaches majority(over threshold), the consensus process moves to *ACCEPT* stage.

### ACCEPT

*ACCEPT* stage is the final stage of acting suffrage group. The consensus process will work if *INIT* stage be started after *SIGN* without *ACCEPT* stage. This stage maybe looks redundant, but there are some reasons:

* During 2 stage, *SIGN* and *ACCEPT* by the acting suffrage group, the suffrage group will have enough time to share result rather than with only *SIGN* stage.
* The minority node at *SIGN* stage can have chance to correct it's decision. With node maybe estimated as none-intact node by only *SIGN* voting.

The ballot for *ACCEPT* stage has these informations:

* Latest block
* Round
* Proposal
* Next block

