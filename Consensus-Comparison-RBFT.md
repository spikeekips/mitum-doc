# RBFT: Redundant Byzantine Faulty Tolerance

> Hi veterans,
> 
> This is GDOC’s new creative Consensus Mechanism we called it as Random Byzantine Fault Tolerance (RBFT). 
> 
> It is well known to public that using BFT consensus system to finish the block producing and validation is popular. 
> 
> But for more security and decentralization, one process of Random Selection will be integrated. The following is the detail process: 
> 
> F(Credential)=Hash(〖SIG〗_i,r,1,Q^(r-1) )
> 
>    First, GDOC network will continuously update to produce a "seed parameter".
> 
>    Secondly, all nodes generate a credential according to the "seed parameter" based on their own private key and a random hash function.
> 
>    Credential value within some range are selected as Validation Nodes (selection blind to public).
> 
>    One of selected nodes is responsible for producing the current block. At the same time, one of the verification nodes will be selected as Leader Node(selection blind to public).
> 
>    The Leader Node cooperate with other nodes to complete the consensus process according to BFT consensus verification logic.
> 
>    Then above verification nodes and Leader Node are invalidated and there will be a new round of random election.
> 
> The strength of the creative process as following:
> 
> First, avoid attacks and fork. Nodes are selected secretly and randomly. And even the producing node is exposed when the BFT consensus started, but the attacker can’t change the block (block producing has been completed).
> 
> Secondly, the BFT consensus mechanism is completed in a very short time, the attacker can’t effectively attack it since it can’t predict the nodes selected and “seed parameter” in advance.
> 
> Thirdly, because of the high efficiency of BFT, the TPS of GDOC network will be greatly improved. We predict that it will be 1000 times more to Ethereum.
> 
> Because BFT has no incentive system, GDOC integrated an incentive system into it with a called DCMM process which will reward all nodes selected by Random Selection. 
> 
> The incentive process to nodes as following:
> 
> First, GDOC will record all nodes selected including block-producing node and validation node randomly secretly.
> 
> Secondly, GDOC will reward all nodes based on a function as bellowing (in name of transaction fee like Ethereum’s GAS):
> 
> T=∑(X_i*a_i+PN*b+VN*r)
> 
> GDOC hope to create a new high TPS and more security network under completely decentralized conditions. It will entirely help GDOC to build up a high efficient data-assets market to support kinds of Dapp. 
> 
> Please leave your comments and we will reward the top 3 hot repliers with one million each.  
> 
> GDOC will publish the whitepaper, website and all social media next week that hope could bring a chance of creative investment.
>
> \- [RBFT: A Creative Consensus Mechanism of Breaking Through to Ternary Paradox](https://bitcointalk.org/index.php?topic=5035362.0)
