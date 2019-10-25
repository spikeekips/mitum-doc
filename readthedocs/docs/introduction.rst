============================================================
Introduction
============================================================

Mitum is a general privacy blockchain with flexible and resilient way. Mitum can be used for various kind of purposes, public and private blockchain like cryptocurrency network, data-centric blockchain for arbitrary data, or secure anonymity voting system, etc.

Basically mitum can provide these main features.

* **SECURITY**: All the in-coming and out-coming messages is signed by signature of sender, so there will be no chance some damaged or malicious messages to be infiltrated. 

* **DESIGNING NETWORK**: mitum network is designed at bootstrap with various policies, network own data types and its native features. These designed factors can be updated without downtime or termination of node and the entire network. 

* **APPLIANCE**: Data in mitum can be defined and designed. Any arbitrary type of data can be supported in mitum. Inside mitum there is a plugin system, so new type of data can be added thru plugin. If you want to launch cryptocurrency network, you can design currency model, define your own currency unit and even inflation rate, etc.

* **CONSENSUS**: mitum guarantees finality. Once the block and it's data are established, it will not be changed or revoked.

* **CONSENSUS**: mitum verifies and establishes data by the consensus protocol. We created the consensus protocol, called ISAAC+, which is newly devised and based on the manner of PBFT. ISAAC+ focuses on finality of block. It guarantees liveness, security and limited fault tolerance. ISAAC+ can be extended for the open and public environment, so new nodes can join the network without the external allowance.

* **CONSENSUS**: ISAAC+ works like well-hardened axe, it is hard to break and resilient from external impact. When some nodes are not intact, it tries to continue agreement. When some blocks are lost in nodes, these data are restored without breaking consensus, the missed consensus messages also be delivered to the edge of network. 

* **CONSENSUS**: Due to ISAAC+, mitum can process huge amounts of messages, like currency transactions, consensus ballots, or any kind of messages for agreement. 

* **DATA PRIVACY**: For privacy of user, mitum supports untraceable account. Basically thanks to the consensus process, accounts can be easily traced by anyone, who did fund it, who sent to it, whom it sent, and it's related data too. But unlike zcash, or hyperledge, mitum tries to support the privacy by transparent account. Transparent account can be created by the legitimate account, but hides which source account makes it. It breaks the link from the originated source account. 

* **DATA**: All the data is stored by hierarchical tree structure(AVL tree). It makes to store and search data efficiently.

* **DATA**: mitum does only rely on the data in the established data in block. The volatile data in node will not be used for consensus process and most of important data will be saved in block, so it can be updated by agreement by consensus protocol.

* **NETWORK**: the basic networking protocol is UDP for consensus process. By the nature of UDP, there is no need to keep or check the connection between consensus nodes.

* **DATA**: mitum supports various kind of storage database: LevelDB, MongoDB, MySQL, PostgreSQL, etc. By the purpose and scale of mitum network, you can choose the best storage database.

* **MANAGEMENT**: For handling the expected or unexpected situation, mitum will provide the management console to the node operator. By this management console, node operator will control his/her node manually.

* **NETWORK VOTING**: All consensus node has the special right to vote for the important decision of network, e.g. allowance or exile of newbie consensus node, updating network policies, etc.

This document will introduce mitum and will describe the working mechanism of mitum.
