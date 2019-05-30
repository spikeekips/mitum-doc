# *ACCEPT* Stage

When node reaches *ACCEPT* stage, it means it's *Proposal* is accepted to the node network and ready to store it's new block. When the enough *ACCEPT* ballots received, node will store the *Proposal* and move to *ALL-CONFIRM* stage. In *ALL-CONFIRM* stage, node will start new round of next block. Like the other stages, same consensus rules will be applied in *ACCEPT* stage. If failed to reach agreement, node will start next round.

In *ACCEPT* stage will collect *ACCEPT* ballot and it has these kind of informations,

* *Proposal*
