============================================================
Designing Network
============================================================

Mitum is designed for general purpose blockchain. To fill this requirement, policy and data of mitum can be configurable and manageable by practical way. The network designer will design his/her network in 2 parts:

* Data
* Policy

Data
------------------------------------------------------------

Simply to say, data is the contents of block. In block any kind of arbitrary contents can be stored. There are several built-in data types in mitum, and new types of data can be defined by the network designer.

Roughly data can be categorized by 2 kinds:

* Defined data
* Anonymous data

Every data belongs to the pre-defined type and has the unique id within globally.

*Defined data*

    is the data, which is statically defined outside block. It is managed in each node and shared thru network. It is under control of it's type.

*Anonymous data*

    represents any kind of undefined data.

The size of data is limited up to certain amount by network policy. Basically data can be created, updated and removed.

Policy
------------------------------------------------------------

Most of distributed system should share the basic principles to the siblings. These principles can be shared and should be synced. For example, how many node should be selected as acting suffrage group and the way to select proposer from acting suffrage group.

In mitum these kind of principles, most of policies are managed in block like data. This means that:

* Policy can be shared to the entire network without additional mechanism.
* Policy can be updated by consensus like data.

.. note::

    The initial policy is set by the network designer.

Model
------------------------------------------------------------

By designing data and policy, the designer can build and launch his/her own model of network.

For example, the designer want to build currency model in mitum. He/Her can define several currency and it's related data and add additional policy.

Data types:

    * Account
    * Balance

Policy:

    * Total amount
    * Minimum amount of new balance
    * Multisig
    * Inflation
    * etc

