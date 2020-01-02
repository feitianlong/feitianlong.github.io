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

 1. Requesting phase

	​		Costumer<sub>i</sub> 发送请求消息 ( 简称： mr ，request message ) ( 包含接收地址的数量addrcount ) 给 Mixer。Mixer 在收到请求之后会给 Costumer<sub>i</sub> 发回一个任务开始消息。如果 Costumer<sub>i</sub> 收到了确认消息，那么 Costumer 生成公钥pkc，然后将 pk<sub>i</sub> 和 tx<sub>id</sub> (需要混淆的 UTXO )发给 Mixer。Mixer 在收集完 pk 后，将 list<sub>1</sub> = { pk<sub>1</sub> , pk<sub>2</sub> , ...， pk<sub>n</sub> } 发给每个 Costumer<sub>i</sub> 。

 2. Generation phase：

	​		Costumer<sub>i</sub> 收到 list<sub>1</sub>，然后生成 list<sub>2</sub>（{ address<sub>1</sub> , address<sub>2</sub> , ... adresss<sub>m</sub> } 。Costumer<sub>i</sub> 根据收到的 list<sub>1</sub> 对每个地址执行环签名，然后更换 IP 地址将各个地址以及环签名依次发给 Mixer (不是一起发给 Mixer )。Mixer 构建混淆交易 Tranraw。

 3. Confirmation phase：

	​		Costumer对 Tranraw ( 指 Coinjoin 式交易 )进行确认，并对其进行签名。

**匿名性怎么保证 ? **

​		因为 Costumer<sub>i</sub>  每次将接收地址 address<sub>i</sub> 发给 Mixer 的时候会更改 IP，然后使用相对应的群签名对 addresslist<sub>i</sub> 执行群签名，便于认证是否为合法成员，这样 Mixer 就收到相关地址，但是无法辨别地址的归属，但是能够确定这些地址是群用户的。


[1]: https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8338002