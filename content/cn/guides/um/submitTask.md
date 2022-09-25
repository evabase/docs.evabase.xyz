---
title: "创建、分享、查看任务"
type: docs
weight: 40
---

创建完成一个任务后，可以对该任务进行3种操作：  
➊分享该任务  
➋查看该任务的策略代码  
➌将该任务提交到网络中

![提交任务](/img/task09.png)

## 分享任务
点击分享按钮，将出现以下弹窗
![分享任务](/img/sharetask01.png)
填入Title(必填)、Description(选填)后，点击`Share`按钮将打开钱包进行签名，签名成功后将弹出如下弹窗
![分享任务](/img/sharetask02.png)
➊点击`Copy link`按钮可复制一个格式为https://app.evabase.xyz/create/[strategyHash]的分享链接，其他用户可打开该链接使用该策略  
➋点击`Task Code`按钮可打开一个新页面查看该策略的策略代码,点击新页面的`Use`按钮会新打开一个页面直接引用该策略  
![分享任务](/img/sharetask02.png)
➌点击`Share to Twitter`按钮可以将该策略的分享链接直接分享到Twitter上  
➍点击`Back to reedit`可充新编辑完善该策略

## 查看任务策略代码
点击该按钮将新打开一个页面，显示该策略的策略代码，此时只能查看，不能做其他操作
![查看任务](/img/viewtask.png)

## 创建任务

在 Evabase 中任意类型[任务]({{<ref "../term/task.md">}})的创建都将按三个步骤处理:

1. 初始化[私人保险箱]({{<ref "../term/walletSafes.md">}})
2. 请求授权
3. 提交订单

![提交任务三个步骤](/img/submitOrder.png)

### 初始化私人保险箱 {#initWallet}

Evabase 为每个钱包创建相互隔离的[私人保险箱]({{<ref "../term/walletSafes.md">}})，每个钱包的所有操作（包括资产转移等）都在独立的保险箱中执行。
因此，每个钱包账户在使用  Evabase 前必须初始化私人保险箱。


{{% alert title="提示" color="primary" %}}
初始化私人保险箱只需要执行一次，不需要每次创建新任务时都执行。
{{% /alert %}}

### 请求授权 {#approve}

如果任务涉及钱包资产，基本都需要用户将资产授权给私人保险箱。比如创建 USDT 兑换 ETH 限价单时需钱包授权USDT 给私人保险箱。


{{% alert title="提示" color="primary" %}}
默认的授权请求都是一次性的，除非用户取消或降低授权额度。
{{% /alert %}}

### 提交 {#submit}

最后一步是将任务信息（ERC20限价单，NFT限价单，自定义Task...）提交到网络中，需要钱包签名。
交易成功时才能创建有效任务。

成功创建任务后，查看任务有一定的延迟， 需等待 5~30 秒才能在[我的任务]({{< ref "../term/task.md">}})页面中查看。