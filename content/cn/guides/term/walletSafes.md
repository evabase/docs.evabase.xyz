---
title: "私人保险箱"
type: docs
weight: 10
---

Your Wallet Safes:  私人保险箱 。


Evabase 为每个地址创建相互隔离的保险箱，每个地址的所有操作（包括资产转移等）都在独立的保险箱中执行。
因此，每个地址在使用  Evabase 前必须初始化部署私人保险箱合约。

## 功能与用途

私有保险箱功能与用途如下：

1. 代理：创建任务的执行主体。每个地址，在钱包中需将任务信息发送到保险箱，保险箱代理用户执行操作。
2. 黑箱：计划任务是在保险箱中执行，以隔离不同钱包地址创建的任务。
3. 智能钱包：保险箱可充当 EOA 地址的智能钱包，代理 EOA 执行 web3 任意合约交互，可批量执行交易。


{{% alert title="提示" color="primary" %}}
Evabase 尚未开发私人保险箱管理终端，未来会根据使用创建提供。
{{% /alert %}}

## 合约源代码

保险箱合约是固定的，谁都无法变更。一旦创建，只有所属地址才能作为管理员操作，Evabase 只能唤起保险箱执行任务。

保险箱通过工厂合约 [0x4cf397d9EDcFe27A95B7DaD5238f437fe9B5dbB6]( https://etherscan.io/address/0x4cf397d9edcfe27a95b7dad5238f437fe9b5dbb6) 创建。可在浏览器中[查看]( https://etherscan.io/address/0x4cf397d9edcfe27a95b7dad5238f437fe9b5dbb6)所有已经被创建的私人保险箱。
