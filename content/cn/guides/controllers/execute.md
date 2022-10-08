---
title: 'Call any contract'
type: docs
weight: 10
---

自定义任务需要用户自行输入待执行的合约信息，系统将自根据输入的合约地址，自动分析合约接口。如果合约已开源则能自动加载并显示合约所有能执行的合约接口，如果加载失败，则说明合约尚未开源，用户可自行填写合约接口。

➊ 将合约地址`0xC272e20C2d0F8fb7B9B05B9F2Ba4407E95928CbF` 填写到输入框中。
➋ 因为该 Token 合约源代码已开源，Evabase 将能自动显示 Token 接口。
➌ 点击会展开显示所有合约接口，从中选择目标 `mint(uint256 amount)`方法。

![计划任务](/img/task02.png)

此时，➊ 输入铸币数量， ➋ 并点击`+`按钮再添加一个 Execute 控件。
![计划任务](/img/task03.png)

在 `Execute2` 中，输入合约地址后，选择 `transfer` 方法。因为 `transfer` 有两个参数：`to` 表示 Token 接收人地址，`amount` 表示转账数量。要输入的参数个数由选择的接口方法决定。

![计划任务](/img/task04.png)
➊ 为 address 地址组件，用户可选择 My wallet - 自己的钱包地址、My smart wallet - 用户的保险箱地址、Input other - 自行输入其他地址三个选项。
![地址组件](/img/addressCom.png)

{{% alert title="提示" color="primary" %}}
在以太坊网络中，可试试输入 USDT 合约地址 `0xdac17f958d2ee523a2206206994597c13d831ec7`。记得，先在钱包中选择 `Ethereum Mainnet` 网络。
{{% /alert %}}

{{% alert title="警告" color="warning" %}}

Evabase 执行 Execute 控件内容的主体(`msg.sender`)是钱包保险箱。如果任务涉及从用户钱包转移资产，则需要先将资产授权给保险箱。

当前版本 Evabase 咱无相关检测提示。

{{% /alert %}}
