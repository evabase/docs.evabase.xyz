---
title: "创建NFT限价单"
type: docs
weight: 20
---

NFT 限价单是 Evabase 核心功能，提供 OpenSea NFT交易市场的挂单功能，服务于**挂单买入NFT**。

导航路径：[App Home](https://app.evabase.net) / [Market](https://app.evabase.xyz/market) / [NFT 限价单](https://app.evabase.xyz/market/nft_limit_order)。


{{% pageinfo color="primary" %}}
通过本文学习，您将学会使用 Evabase 创建  NFT 限价单。
{{% /pageinfo %}}

![NFT限价单](/img/nftorder01.png)

## 交易场景 {#case}

1. 无需盯盘，自动低价批量买入NFT。
2. 捡漏，自动监控市场卖出信号，当发现错误的卖出价格时，自动快速买入。
3. 项目方做市，在一定价位自动买入 NFT，活跃市场。
4. 无需盯盘，当心仪的 NFT 跌入预期价格范围时，自动买入。

{{% alert title="提示" color="primary" %}}
结合 Evabase 的自定义Task功能可以积木式构建更丰富的场景，但涉及智能合约编程。
{{% /alert %}}

{{% alert title="提示" color="warning" %}}
Evabase NFT 不适合市价或更高价格批量扫单，因为这比OpenSea官网的买入功能消耗更多的 Gas 。
{{% /alert %}}

<!-- ##  -->

## NFT限价单页面 {#page}

可以从 [Market]({{< ref "market.md">}}) 进入 NFT 限价单页面，也可以之间通过固定链接 https://app.evabase.xyz/market/nft_limit_order 打开。


![NFT限价单](/img/nftorder00.png)

## 输入 {#input}

创建 NFT 限价单流程如下：

1. 输入 NFT 链接
2. 输入 NFT 挂单买入价格与买入数量
3. 自定义 NFT 限价单任务名称
4. 提交订单

每个操作环节具体说明如下。

### 输入NFT链接 {#nfturl}

如何确定NFT链接呢？这需要用户先在 [OpenSea](https://opensea.io/) 中浏览 NFT，打开希望挂单买入的 NFT 网页。
然后，将 NFT 页面的网页地址复制出来。如喜欢无聊猿(https://opensea.io/collection/cryptopunks)，想试试运气来捡漏则可以在 Evabase 创建一个无聊猿低价单。

![NFT限价单](/img/nftorder02.png)

➊ 只需将无聊猿在OpenSea中的网址 https://opensea.io/collection/cryptopunks 复制到输入框中。 ➋ 然后，点击`Load`按钮。稍等片刻，会在下方加载显示无聊猿 NFT 相关信息：

![NFT限价单输入NFT链接](/img/nftorder03.png)

➊ 是 无聊猿 NFT 集合的图片，来自 OpenSea 网站。
➋ 是 无聊猿 NFT 集合名称，点击`[⤴︎]`可网页跳转到无聊猿 OpenSea 中。
➌ 如果在 OpenSea 中有显示 NFT 地板价，那么这里也同样显示地板价。`- ETH` 表示没有地板价。
➍ 是 NFT 在 OpenSea 中的 24 小时交易额。

如果只希望买入特定的单个 NFT，则可以输入单个 NFT 的 OpenSea 网址。如喜欢 Token 编号为 6981 的无聊猿，
则复制 https://opensea.io/assets/ethereum/0xb47e3cd837ddf8e4c57f05d70ab865de6e193bbb/6981 网址到输入框中就行。

![NFT限价单输入NFT链接](/img/nftorder04.png)


### 输入价格与数量 {#price}

确定要买入的 NFT 后，需要根据自己的判断输入挂单买入价格和购买数量。

![NFT价格与数量](/img/nftorder05.png)

➊ 买入价格：Evabase 将监控 OpenSea 的卖出挂单信息(NFT List)，一旦卖出价格低于或者等于买入价格，Evabase 将自动从查询到的多个 NFT 报价中挑选最低报价的 NFT 买入。

➋ 买入数量：只有选择买入指定 NFT 集合中任意 NFT 时，才允许输入数量。Evabase 将持续买入 NFT 直到全部买入或者任务过期。

### 自定义任务名 {#taskName}

第三步是自定义任务名称和追加预付 Gas 。

1. Task Name：任务名称，由 Evabase 默认生成，也可以随意更改。但一旦提交，不可再次修改。
2. Fund Balance：预留 Gas 余额，需要确保钱包有存入足够的 ETH 作为 Gas 预付款才能确保 Evabase 及时买入 NFT。

![提交任务-签名](/img/nftorder10.png)


### 提交任务 {#submit}

点击`Submit`将提交限价单到网络中，更多细节请参见 [提交任务]({{< ref "submitTask.md" >}}) 文档。 NFT 限价单的提交需要完成三个动作：

➊ 初始化私人保险箱（单个钱包只执行一次）。
➋ 签名限价单：通过钱包对限价单内容签名，签名不产生交易费，也不会发送交易到网络中。只为确保第三方无法篡改订单信息。
![提交任务-签名](/img/nftorder07.png)

➌ 第三个动作，则是将签名的NFT限价单任务提交到Evabase协议中，需要钱包发送交易。在钱包中点击【确定】等待交易完成。
![提交任务-发送交易](/img/nftorder08.png)


## 查看任务 {#see}

成功创建任务后，查看任务有一定的延迟，需等待 5~30 秒时间才能在[我的任务]({{< ref "tasks.md">}})页面中查看。

![NFT价格与数量](/img/nftorder09.png)

<!-- ➊ ➋ ➌ ➍ ➎ ➏ ➐ ➑ ➒ ➓ -->
