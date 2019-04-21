---
layout:     post
title:      Unlinkable Coin Mixing Scheme for Transaction Based on Ringsignature
subtitle:   The Mixing Protocol
date:       2019-04-21
author:     FTL
header-img: img/post-bg-paper-unlinkableCoinBasedRingSignture.jpg
catalog: true
tags:
    - Paper
---

# Unlinkable Coin Mixing Scheme for Transaction

[Paper链接][1]

## The Mixing Protocol

 1. requesting phase

	coustomer发送(request message)mr(包含接收地址的数量(注意是地址数量，不是地址)addrcount)给Mixer。Mixer在收到请求之后会给costumer发回一个任务开始消息。如果costumer收到了确认消息，那么costumer生成公钥pkc，然后将pki和txid(需要混淆的UTXO)发给Mixer。Mixer在收集完pk后，将list1={pk1, pk2,...pkn}发给每个Costumer。

 2. generation phase：

	costumer收到list1，然后生成list2（{address1, address2, ... adresssm}. Costumer根据收到的list1对每个地址进行环签名，然后更换Ip地址将各地址连接环签名一个接一个发给Mixer(不是一起发给Mixer)。Mixer构建mixing交易Tranraw。

 3. confirmation phase

	costumer对Tranraw(合并交易)进行确认，并对其进行签名。

**匿名性怎么保证???**

    因为Costumers每次将接收地址addressi发给Mixer的时候会更改IP，然后使用相对应的群签名对addressi进行群签名，便于认证是否为合法成员，这样Mixer就收到相关地址，但是无法辨别地址的归属，但是能够确定这些地址是群用户的。


  [1]: https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8338002