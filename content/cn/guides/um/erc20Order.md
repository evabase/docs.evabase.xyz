---
title: "ERC20限价单"
type: docs
weight: 30
---

{{% pageinfo color="primary" %}}
通过本文学习，您将学会使用 Evabase 创建 ERC20 Token 限价单。
{{% /pageinfo %}}

## 入口 {#enter}

在 Market 页面中点击 `Buy token at the specified price` 控件的 `Use` 按钮。
![ERC20限价单控件](/img/erc20order00.png)

随后，进入 ERC20限价单 操作页面：

![ERC20限价单 操作页面](/img/erc20order02.png)

## 选择资产与设置价格 {#input}

在提交限价单前，需要您设置限价单相关信息，以确定您的下单意图。

下面，将以 “用 1230 USDT价格将 1 ETH 兑换成 USDT”为例，说明操作过程。


{{< cardpane >}}
  {{< card >}}
![ERC20限价单选择资产与设置价格](/img/erc20order03.png)
  {{< /card >}}
  {{< card >}}
![ERC20限价单选择资产与设置价格](/img/erc20order04.png)
  {{< /card >}}
{{< /cardpane >}}
<!-- ➊ ➋ ➌ ➍ ➎ ➏ ➐ ➑ ➒ ➓ -->

- ➊ Pay: 将被兑换出去的资产（也称卖出的或支付的资产），如 “ETH”。点击下拉按钮可从列表中[选择资产](#select)。
- ➋ Balance：选择卖出资产后，系统将刷新自动显示钱包的该资产余额。点击可自动填充所有资产余额到资产输入框中。
- ➌ 卖出资产数量输入框，不得超过钱包余额。
- ➍ 价格更新按钮，将实时从 Uniswap 中读取该交易对的价格。点击按钮将自动填充最新价格到价格输入框中。
- ➎ 价格输入框，表示最低卖出价格。可以手工输入，将会根据输入的价格联动更新可兑换的资产数量。
- ➏ Receive：将被兑换到的资产（也称买入资产），如 “USDT”。 点击下拉按钮可从列表中[选择资产](#select) 。
- ➐ 最少可兑换得到的资产数量。默认将根据价格自动计算显示，也可以手工输入，将会根据输入联动更新价格输入框。


### 选择资产 {#select}

点击资产选择框，将弹出资产选择窗口。

在该弹窗中可输入资产符号检索资产。如果没有找到，可直接输入资产地址并按下回车键，系统将自动查询出该地地址，可以点击 `Import token` 选择并保存资产信息到浏览器中，供下次使用。

![查询选择资产](/img/selectToken.png)

## 预付Gas费与设置任务名称  {#setGasAndTaskName}

确定限价单信息后，根据实际情况有可选输入项信息：

1. Fund Balance: 钱包在 Evabase 中预留的 Gas 资金。用于任务自动执行时代扣 Gas 费。如果 Fund Balance 为零或者不足时，即使创建了限价单等任务，任务不会自动执行，直达 Fund Balance 充足。
2. Task Name: 限价单任务名，可自定义，名字越短越节省 Gas。一经确定，任务名称不可修改。

![预付Gas费与设置任务名称](/img/erc20order05.png)

## 提交限价单 {#submit}

点击`Submit`将提交限价单到网络中，更多细节请参见 [提交任务]({{< ref "submitTask.md" >}}) 文档。

![提交限价单](/img/erc20order06.png)

## 查看任务 {#see}

成功创建任务后，查看任务有一定的延迟，需等待 5~30 秒时间才能在[我的任务]({{< ref "tasks.md">}})页面中查看。

下面是一个 ERC20 限价单的任务详情：

![ERC20 限价单的任务详情](/img/erc20orderTask.png)