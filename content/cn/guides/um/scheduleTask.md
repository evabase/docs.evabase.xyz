---
title: "创建计划任务"
type: docs
weight: 31
---

Evabase 支持自定义任务，允许将多笔交易合并成一笔交易，并允许设置执行计划。

导航路径：[App Home](https://app.evabase.net) / [Create](https://app.evabase.xyz/create) 。


{{% pageinfo color="primary" %}}
通过本文学习，您将学会使用 Evabase 创建自定义计划任务。
{{% /pageinfo %}}


## 场景 {#case}


Evabase 当前版本只实现了 Call any contract - Execute控件、Require - 断言控件、Uniswap v3 Swap - Uniswap兑换控件，后续将陆续提供其他功能性控件，如：Compound 存款控件等等。利用丰富的控件，可以如同积木一样搭建更丰富的交互场景：

1. 定投：固定每周买入 200 USDT 的 BTC。
2. 工资发放：固定每月一号发放 ETH 工资给员工。
3. 抢公售NFT：提前创建  Mint 任务，让 Evabase 在第一时间 Mint  NFT ，不用担心错过时间。
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

#### Call any contract - Execute控件

自定义任务需要用户自行输入待执行的合约信息，系统将自根据输入的合约地址，自动分析合约接口。如果合约已开源则能自动加载并显示合约所有能执行的合约接口，如果加载失败，则说明合约尚未开源，用户可自行填写合约接口。

➊ 将合约地址`0xC272e20C2d0F8fb7B9B05B9F2Ba4407E95928CbF` 填写到输入框中。
➋ 因为该 Token 合约源代码已开源，Evabase 将能自动显示 Token 接口。
➌ 点击会展开显示所有合约接口，从中选择目标 `mint(uint256 amount)`方法。

![计划任务](/img/task02.png)

此时，➊ 输入铸币数量， ➋ 并点击`+`按钮再添加一个 Execute 控件。
![计划任务](/img/task03.png)

在 `Execute2` 中，输入合约地址后，选择 `transfer` 方法。因为 `transfer` 有两个参数：`to` 表示 Token 接收人地址，`amount` 表示转账数量。要输入的参数个数由选择的接口方法决定。

![计划任务](/img/task04.png)
➊为address地址组件，用户可选择My wallet - 自己的钱包地址、My smart wallet - 用户的保险箱地址、Input other - 自行输入其他地址三个选项。
![地址组件](/img/addressCom.png)


{{% alert title="提示" color="primary" %}}
在以太坊网络中，可试试输入 USDT 合约地址 `0xdac17f958d2ee523a2206206994597c13d831ec7`。记得，先在钱包中选择 `Ethereum Mainnet` 网络。
{{% /alert %}}

{{% alert title="警告" color="warning" %}}

Evabase 执行 Execute 控件内容的主体(`msg.sender`)是钱包保险箱。如果任务涉及从用户钱包转移资产，则需要先将资产授权给保险箱。

当前版本 Evabase 咱无相关检测提示。

{{% /alert %}}

#### Require - 断言控件

在程序开发中，一般使用逻辑判断来执行不同分支语句，或检测逻辑执行结果是否符合预期。Evabase支持在创建Task中使用 Require 积木来检测状态是否符合预期，或作为任务执行的检查条件之一。
![require控件](/img/require01.png)
A vs B 是变量A和B的值的比较运算（>,<, >=,<=, !=, =），当比较结果为 True 时，任务才能得以继续执行，否则回滚任务并终止执行任务。

选择Require控件后，A、B默认值为空，需用户自行选择变量 A 和 B 值的计算方式，支持设定为固定值或通过读取合约动态获取。为了方便用户使用从合约读取数据，会默认将一些常见读取合约数据封装。
计算方式如下，不同计算方式，对应不同的数据计算方式。
1. 动态值：  
  a. Call contract : 从任意合约读取数据。  
  b. Price oracle: 从Chain Link 预言机中读取数据。  
  c. Token balance: 查询 Token余额。  
2. 固定值：  
  a. Number: 整数固定值( uint256)。  
  b. Address:  地址固定值( 20 bytes,  uint160)。  
  c. Bool: 布尔固定值(uint8)。  
  d. Bytes32: 字节固定值(uint256)。 （32 字节的数据，[32]byte  max uint256 = 2^8^32-1）

**Call contract**  
同Execute控件一样，依次完成以下步骤：输入合约地址，选取要调用的合约方法，填充完整合约方法需要的参数，操作完以上步骤以后，点击➊右侧的刷新按钮，将调用合约方法模拟出执行结果，若A中➊的返回结果与B中➋的返回结果一致，那么该步骤将被成功执行，该任务也将继续执行。
![require控件](/img/require03.png)

**Price oracle**  
Evabase 集成 Chainlink 预言机 Data Feed 数据，允许用户通过UI选择从 Chainlink 中读取 Oracle 数据。
点击`Pair`打开Data feed选择面板，选择自己需要查询的pair
![require控件](/img/require04.png)
选择后点击`Current data`中的刷新按钮即可通过合约获取到oracle数据并显示在`Current data`中
![require控件](/img/require05.png)

**Token balance**  
Evabase 封装了获取 ERC20 Token 余额方法，点击➊将弹出token选择弹窗，选择token后，在➋选择或输入要查询的该toten余额的地址，然后同上`Current data`中调用合约获取数据。
![require控件](/img/require06.png)

**固定值**  
固定值支持4种类型：
1. Number:  bigint 整数固定值（必须不小于0）。
2. Address:  地址固定值,必须是一个合法的地址。
3. Bool: 布尔固定值。
4. Bytes32: 字节固定值（最长32字节）。
![require控件](/img/require07.png)

#### Uniswap v3 Swap - Uniswap兑换控件

该控件与Uniswap v3的swap功能类似：  
➊选择Input token，  
➋选择Output token，  
➌输入选择的两个token其中一个的数量（另一个token的数量会根据输入的token的数量以及价格自动计算出来），  
➍如果input token未在平台授权过或授权额度不足，需要先进行授权。  
➎为选择的两个token的相对价格，  
➏为用户钱包中Input token的余额。

![swap控件](/img/swap.png)

{{% alert title="提示" color="primary" %}}
多个控件时可通过鼠标按住控件名称名称，拖动修改控件执行顺序。
{{% /alert %}}

###  设置执行计划

设置好执行内容后，系统将自动显示执行计划设置面板。

![计划任务](/img/task05.png)

Evabase 支持三种执行模式：

1. Time - 定时器模式：设定执行间隔，定时自动执行。
2. Whennever possible - 永动模式：只要系统能够发送交易，则尽可能的发送执行指令。最高频率是每个区块中执行一次任务。
3. Resolver - 自定义模式：需要用户自行编写符合规范的触发器合约，Evabase 将一直监控触发器，一旦触发器告知可以执行，Evabase 将立即响应执行一次。（当前 Evabase 尚未开放该模式）

定时器模式是常规使用方式，允许设置更多与执行相关的参数。
➊ One-time: 勾选表示只执行一次，不论执行成功与否，立即关闭任务。
➋ Interval：默认选项，可设置执行周期。在任务有效期内将按时间间隔执行任务。
➌ Effective immediately: 默认勾选，表示任务立即生效。也可以不勾选，自定义任务生效开始时间。如下图设定的生效时间为2022年7月4日 00:06:00 时。

![计划任务](/img/task07.png)


###  自定义名称

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
