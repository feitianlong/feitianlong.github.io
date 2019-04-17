---
layout:     post
title:      Dos和Sybil分析
subtitle:   几篇Mixer论文中的Dos和Sybil
date:       2019-04-17
author:     FTL
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Paper
---

###  Sybil 和 Dos 抵抗

____

#### CoinSwap 2013

CoinSwap的中间人设定必须是可信的，因此可以通过支付混币费来抵抗dos，sybil(具体数额未分析)。
 
____
#### Mixcoin 2014

##### （原文）未分析

Mixcoin的mixing server也是需要一个可信的第三方（类似于淘宝卖家，基于信誉度的方式），但是每次混币需要支付混币费的方式来抵抗dos和sybil。
  
（CoinShuffle原文）the use of a central mix introduces a single point of failure, where the mix becomes a suitable target for DoS attacks from competing mixes as well as governmental agencies.这个混币的中间商还是会收到dos攻击，

____

#### CoinShuffle 2014

##### (原文)CoinShuffle is inspired by CoinJoin to ensure security against theft and by the accountable anonymous group communication protocol Dissent to ensure anonymity as well as robustness against Dos attacks
 
使用Dissent来抵抗dos，其中Dissent(Dining-cryptographers Shuffled-Send Network)可以accountable，但是无法让其付出代价。

(原文)The shuffling provides robustness in the sense that attacks that aim to disrupt the protocol can be detected by honest users and at least one misbehaving participant can be identified and excluded.  

对于破坏协议的成员会被诚实的节点发现，并将其排除。  

在创建交易之前，会计算交易费，然后通过均摊的方式来支付交易费。这里的交易费不是混币费。因此通常认为Coinshuffle无法抵抗Dos和Sybil。

____

#### Xim 2014(实质是一个匿名寻找伙伴协议)

##### (原文)We show that because of Xim's participation fees, launch-ing inference or DoS attacks based on Sybil identities are costly. For a given success rate, ((a Sybil attacker's costs grow linearly with the number of mix participants)), while honest participants' costs remain small,fixed, and constant.

假设针对Xim的advertiser进行dos攻击，那么attacker需要使用多个respondent向目标location发送加密消息；且advertiser不一定会选择attacker的消息进行回应，即使attacker的消息被选中，如果攻击者不再规定时间内对advertiser消息进行ad回应，那么advertiser会重新选择respondent的消息，

因此对于sybil攻击，攻击者的代价与参与者的数量呈线性增长。
对于该混币机制的用户收取费用的方式来抵抗dos和sybil，但是Xim中恶意节点的损失会根据混币参与者的数量呈线性增长。之前的混币协议的混币费用对于恶意节点和友好节点是一样的。

____

#### BindlCoin 2015

##### （原文）each user interacts only with the mixing server(谁充当),and refusing to comply with the protocol does not affect any other users or slow down the mixing process.

用户只和mixing server进行混币，所以即使进行进行dos攻击也不会影响到其它用户进行混币。（这个dos抵抗是不是太片面？？？dos也会耽误mixing server的时间）

____

#### Blindly Signed Contrasts 2016

##### 同TumbleBit

In a sybil attack, the adversary creates many sybil identities secretly under her control, and deanonymizes a target user by forcing the target to mix only with sybils [3, 22]. To launch this attack on our protocol, the attacker could create m runs of our protocol (i.e., m payers and payees) that occupy most of the intermediary T’s resources, leaving only a single slot available for the targeted payer and payee. Again, we use fees to raise the cost of this attack, by requiring each of the m Sybil runs to pay a fee voucher of value f. If T performs a sybil attack, T avoids paying f but must pay all four transaction fees.
  
在sybil攻击中，对手在她的控制下秘密地创建了许多sybil身份，并通过强制目标仅与sybils混合来对目标用户进行去匿名[3,22]。 为了对我们的协议发起这种攻击，攻击者可以创建m个我们的协议（即m个付款人和收款人），占用大部分中间T的资源，只留下一个可用于目标付款人和收款人的插槽。 同样，我们通过要求每个m Sybil运行支付价值f的费用凭证来使用费用来提高此攻击的成本。 如果T执行sybil攻击，T避免支付f但必须支付所有四笔交易费用。  

This is because must forward an anonymous fee voucher V` from A to I every time B wishes to initiate our protocol.  

这里万一 I(发行Voucher的人) 跑路了怎么办。。。。

____

#### TumbleBit  2017

##### （原文）TumbleBit uses transaction fees to resist Dos and Sybil attacks.使用交易费的方式抵抗DoS和Sybil攻击.
  
Alice 同Tumbler建立支付通道时，除了支付一笔费用用于托管，还需要给Tumbler支付一笔混币费。Bob同Tumbler建立支付通道也需要支付混币费。  （此处使用Voucher，交易费很低） 


##### （原文关于TumbleBit Dos）Recall from the previous section that TumbleBit relies on escrow transactions to prevent double spending. In both the payment hub mode and the traditional mixing mode, escrow setups have to be completed before the payment phase. There is no requirement on the order of the escrow transactions’ creation. In fact, it is impossible to enforce such restrictions without protocol modification, since the Tumbler cannot link the Alices’ payments to their respective Bobs’ outputs. Thus, the Tumbler has to accept escrow requests from people claiming to be Bob, even if they are not accepting any payment. Malicious attackers may exploit this weakness by forcing the Tumbler to escrow bitcoins to them and wasting the Tumbler’s capital when it could be servicing other customers. These attacks make it very inefficient for the Tumbler’s business, where it prepares a large reserve but is only capable of servicing a fraction of their estimated users. Each unsuccessful escrow would also cost the Tumbler some bitcoins to pay for the fees associated with the escrow and refund transactions.  


恶意攻击者可能通过迫使Tumbler将比特币托管给他们并在可能为其他客户提供服务时浪费Tumbler的资本来利用这一弱点。这些攻击使得Tumbler的业务效率非常低，它可以准备大量的储备，但只能为其估计用户的一小部分提供服务。每次不成功的托管也会使Tumbler花费一些比特币来支付与托管和退款交易相关的费用。虽然原文中说，需要提供混币费进行交易，但是并没有具体说明支付方式。

____

即使用混币费来抵抗dos攻击，但是无法避免dos


去中心化，带来通信代价
  
Decentralization also requires mix users to interact via a peer-to-peer network in order to identify each other and mix payments.This coordination between users causes communication to grow quadratically [13], [14], limiting scalability。

