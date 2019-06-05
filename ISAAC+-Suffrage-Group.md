# Suffrage Group

## Join Suffrage Group

Every node can join *Suffrage Group*, but there are some requirements and steps.

* Node, which want to join the *Suffrage Group* should prove itself
    - required account data; like enough amount of balance
    - state of block
    - validation capability
        - machine power
        - fast-enough network; network should be fast and under stable environment
    - etc : additional conditions could be made by *Suffrage Group*

* Node should vote on the active *Proposal* in each round and can broadcast *SIGNBallot* to the current *Suffrage Group* within the given time(before *ALL-CONFIRM* stage)
* After the given time(at this time, almost 1 month?), node gathers the enough agreement signing from nodes of *Suffrage Group* and proposes the entrance request to the node network.
* The entrance request is validated by *Active Suffrage Group* and if passed, the node can be join *Suffrage Group*
* The newly joined node in *Suffrage Group* can participate after 50 blocks from the block it joins.

## Leaving Suffrage Group

Node can submit the leaving request to *Suffrage Group* and if it correctly signed by node, it will be applied to the block state.

## Exile From Suffrage Group

Node in *Suffrage Group* can be exiled by similar way, voting. If node in *Suffrage Group* is judged to be the fauly node, any node in *Suffrage Group* can propose the exile request for the faulty node. If passed, the node will be out of *Suffrage Group*. If the fauly node want to join again, it should wait for the given time(almost 1 month?).

## Why The Newly Joined Node in Suffrage Group Can Participate After 50 Blocks

Ideally it will be natural that the new node can participate as soon as it joins, but in ISAAC+ it can participate the consensus process after 50 blocks from the block it joins. If `N₀` joined in the *Suffrage Group* at `H33`, `N₀` can participate(it means `N₀` can broadcast `INIT` ballot to the network) after the block, `H88` is stored.

This `50` block interval can make the lagged nodes can catch up easily to the global block state. In distributed environment, there are the lagged nodes, which are failed to sync with the global block state. `50` block interval will help this kind of lagged node can easily check out their block state is far behind from global state.

We can assume this situations,

* `N₀` tries to start new round of `H133` and `R0` for voting of the next block of `H133`.
* But the global state is `H135`.
* `N₀` keeps waiting the incoming ballots for `H133 R0`, but it can not receive because `H133` is already finished.

`N₀` will receive these ballots,

| node | block | round |                |
| ---- | ----- | ----- | -------------- |
| `N₀` | `H133` | `R0` | voted by `N₀`  |
| `N₁` | `H135` | `R0` |                |
| `N₂` | `H135` | `R0` |                |
| `N₃` | `H135` | `R0` |                |

* `N₀` can check that something wrong.
* `N₀` checks, `H135` is over threshold.
* `N₀` can find which nodes are in *Active Suffrage Group* of `H135`.
* `N₀` can check `[N₁ N₂ N₃]` is the valid nodes of *Active Suffrage Group* of `H135`
* Eventually `N₀` can know it's block state is far from the global block state, `H135`.
* `N₀` moves to *sync*.

Without `50` block interval, `N₀` can not check whether `[N₁ N₂ N₃]` are in *Active Suffrage Group* of `H135`. To check which nodes are in `H135`, `N₀` easily check the entire nodes of *Suffrage Group* of `H85`(`135 - 50`).
