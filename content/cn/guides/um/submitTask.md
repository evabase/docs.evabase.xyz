---
title: "提交任务"
type: docs
weight: 40
---

在 Evabase 中任意类型[任务]({{<ref "../term/task.md">}})的提交都将按三个步骤处理:

1. 初始化[私人保险箱]({{<ref "../term/walletSafes.md">}})
2. 请求授权
3. 提交订单

![提交任务三个步骤](/img/submitOrder.png)

## 初始化私人保险箱 {#initWallet}

Evabase 为每个钱包创建相互隔离的[私人保险箱]({{<ref "../term/walletSafes.md">}})，每个钱包的所有操作（包括资产转移等）都在独立的保险箱中执行。
因此，每个钱包账户在使用  Evabase 前必须初始化私人保险箱。


{{% alert title="提示" color="primary" %}}
初始化私人保险箱只需要执行一次，不需要每次创建新任务时都执行。
{{% /alert %}}

## 请求授权 {#approve}

如果任务涉及钱包资产，基本都需要用户将资产授权给私人保险箱。比如创建 USDT 兑换 ETH 限价单时需钱包授权USDT 给私人保险箱。


{{% alert title="提示" color="primary" %}}
默认的授权请求都是一次性的，除非用户取消或降低授权额度。
{{% /alert %}}

## 提交 {#submit}

最后一步是将任务信息（ERC20限价单，NFT限价单，自定义Task...）提交到网络中，需要钱包签名。
交易成功时才能创建有效任务。

成功创建任务后，查看任务有一定的延迟， 需等待 5~30 秒才能在[我的任务]({{< ref "tasks.md">}})页面中查看。