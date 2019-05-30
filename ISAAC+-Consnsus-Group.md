# *Consensus Group*

## Join *Consensus Group*

Every node can join *Consensus Group*, but there are some requirements and steps.

* Node, which want to join the *Consensus Group* should prove itself
    - required account data; like enough amount of balance
    - state of block
    - validation capability
        - machine power
        - fast-enough network; network should be fast and under stable environment
    - etc : additional conditions could be made by *Consensus Group*

* Node should vote on the active *Proposal* in each round and can broadcast *SIGN* ballot to the current *Consensus Group* within the given time(before *ALL-CONFIRM* stage)
* After the given time(at this time, almost 1 month?), node gathers the enough agreement signing from nodes of *Consensus Group* and proposes the entrance request to the node network.
* The entrance request is validated by *Validator Group* and if passed, the node can be join *Consensus Group*

## Leaving *Consensus Group*

Node can submit the leaving request to *Consensus Group* and if it correctly signed by node, it will be applied to the block state.

## Exile From *Consensus Group*

Node in *Consensus Group* can be exiled by similar way, voting. If node in *Consensus Group* is judged to be the fauly node, any node in *Consensus Group* can propose the exile request for the faulty node. If passed, the node will be out of *Consensus Group*. If the fauly node want to join again, it should wait for the given time(almost 1 month?).
