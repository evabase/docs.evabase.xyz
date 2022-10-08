---
title: '创建计划任务'
type: docs
weight: 31
---

Evabase 支持自定义任务，允许将多笔交易合并成一笔交易，并允许设置执行计划。

导航路径：[App Home](https://app.evabase.net) / [Create](https://app.evabase.xyz/create) 。

{{% pageinfo color="primary" %}}
通过本文学习，您将学会使用 Evabase 创建自定义计划任务。
{{% /pageinfo %}}

## 场景 {#case}

Evabase 当前版本只实现了 Call any contract - Execute 控件、Require - 断言控件、Uniswap v3 Swap - Uniswap 兑换控件，后续将陆续提供其他功能性控件，如：Compound 存款控件等等。利用丰富的控件，可以如同积木一样搭建更丰富的交互场景：

1. 定投：固定每周买入 200 USDT 的 BTC。
2. 工资发放：固定每月一号发放 ETH 工资给员工。
3. 抢公售 NFT：提前创建 Mint 任务，让 Evabase 在第一时间 Mint NFT ，不用担心错过时间。
4. 交易：设定 ETH 下跌 10% 则立即买入，并可设置挂单卖出价格。
5. GameFi: 定期自动和游戏交互。
6. 复投：定期定量将挖矿代币存入抵押池或卖出再投资。
7. ...

利用 Evabase 控件积木组合能力，让 Evabase 帮你实现低代码编程，减轻运维烦恼。

## 计划任务 {#taskPage}

进入计划任务页面，默认只展示一个`+`按钮，点击`+`打开控件选择面板，根据自己的需要选择添加不同的控件。其他信息随着不断交互操作，会实时显示。

![控件选择面板](/img/task01.jpeg)

![控件选择](/img/selectBlock.jpeg)

## 操作步骤

提交计划任务，需要完成四个操作：

1. 选择添加控件并填充完整控件内容。
2. 设置执行计划：多种方式设置任务执行触发器。
3. 自定义名称。
4. 提交任务。

{{% alert title="提示" color="primary" %}}
下文将以测试环境中的 ERC20 Token 为例，创建铸币任务：

设定每分钟执行一次铸币，并将代币转入到指定钱包中。
{{% /alert %}}

### 选择添加控件并填充控件内容

以下为现有控件的使用说明。

[Call any contract - Execute 控件]({{< ref "../controllers/execute.md" >}})  
[Require - 断言控件]({{< ref "../controllers/require.md" >}})  
[Uniswap v3 Swap - Uniswap 兑换控件]({{< ref "../controllers/uniswapV3swap.md" >}})

用户可以根据自己的需求，选择添加多个控件

{{% alert title="提示" color="primary" %}}
多个控件时可通过鼠标按住控件名称名称，拖动修改控件执行顺序。
{{% /alert %}}

### 设置执行计划

设置好执行内容后，系统将自动显示执行计划设置面板。

![计划任务](/img/task05.png)

Evabase 支持三种执行模式：

1. Time - 定时器模式：设定执行间隔，定时自动执行。
2. Whennever possible - 永动模式：只要系统能够发送交易，则尽可能的发送执行指令。最高频率是每个区块中执行一次任务。
3. Resolver - 自定义模式：需要用户自行编写符合规范的触发器合约，Evabase 将一直监控触发器，一旦触发器告知可以执行，Evabase 将立即响应执行一次。（当前 Evabase 尚未开放该模式）

定时器模式是常规使用方式，允许设置更多与执行相关的参数。
➊ One-time: 勾选表示只执行一次，不论执行成功与否，立即关闭任务。
➋ Interval：默认选项，可设置执行周期。在任务有效期内将按时间间隔执行任务。
➌ Effective immediately: 默认勾选，表示任务立即生效。也可以不勾选，自定义任务生效开始时间。如下图设定的生效时间为 2022 年 7 月 4 日 00:06:00 时。

![计划任务](/img/task07.png)

### 自定义名称

确定任务后，还需设定任务名称和追加 Gas 预付：

1. ➊ Fund Balance: 钱包在 Evabase 中预留的 Gas 资金。用于任务自动执行时代扣 Gas 费。如果 Fund Balance 为零或者不足时，即使创建了任务，任务也不会自动执行，直达 Fund Balance 充足。
2. ➋ Task Name: 限价单任务名，可自定义，名字越短越节省 Gas。一经确定，任务名称不可修改。

![计划任务](/img/task08.png)

## 提交任务 {#submit}

点击对应的操作按钮将任务进行提交或分享，更多细节请参见 [创建、分享、查看任务]({{< ref "submitTask.md" >}}) 文档。

![提交任务](/img/task09.png)

## 查看任务 {#see}

成功创建任务后，查看任务有一定的延迟，需等待 5~30 秒才能在[我的任务]({{< ref "../term/task.md">}})页面中查看。

下方是刚在测试网络中创建的计划任务详情：

![计划任务列表](/img/task11.png)
![计划任务明细](/img/task12.png)

<!-- ➊ ➋ ➌ ➍ ➎ ➏ ➐ ➑ ➒ ➓ -->
