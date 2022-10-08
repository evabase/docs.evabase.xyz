---
title: 'Require'
type: docs
weight: 10
---

在程序开发中，一般使用逻辑判断来执行不同分支语句，或检测逻辑执行结果是否符合预期。Evabase 支持在创建 Task 中使用 Require 积木来检测状态是否符合预期，或作为任务执行的检查条件之一。
![require控件](/img/require01.png)
A vs B 是变量 A 和 B 的值的比较运算（>,<, >=,<=, !=, =），当比较结果为 True 时，任务才能得以继续执行，否则回滚任务并终止执行任务。

选择 Require 控件后，A、B 默认值为空，需用户自行选择变量 A 和 B 值的计算方式，支持设定为固定值或通过读取合约动态获取。为了方便用户使用从合约读取数据，会默认将一些常见读取合约数据封装。
计算方式如下，不同计算方式，对应不同的数据计算方式。

1. 动态值：  
   a. Call contract : 从任意合约读取数据。  
   b. Price oracle: 从 Chain Link 预言机中读取数据。  
   c. Token balance: 查询 Token 余额。
2. 固定值：  
   a. Number: 整数固定值( uint256)。  
   b. Address: 地址固定值( 20 bytes, uint160)。  
   c. Bool: 布尔固定值(uint8)。  
   d. Bytes32: 字节固定值(uint256)。 （32 字节的数据，[32]byte max uint256 = 2^8^32-1）

**Call contract**  
同 Execute 控件一样，依次完成以下步骤：输入合约地址，选取要调用的合约方法，填充完整合约方法需要的参数，操作完以上步骤以后，点击 ➊ 右侧的刷新按钮，将调用合约方法模拟出执行结果，若 A 中 ➊ 的返回结果与 B 中 ➋ 的返回结果一致，那么该步骤将被成功执行，该任务也将继续执行。
![require控件](/img/require03.png)

**Price oracle**  
Evabase 集成 Chainlink 预言机 Data Feed 数据，允许用户通过 UI 选择从 Chainlink 中读取 Oracle 数据。
点击`Pair`打开 Data feed 选择面板，选择自己需要查询的 pair
![require控件](/img/require04.png)
选择后点击`Current data`中的刷新按钮即可通过合约获取到 oracle 数据并显示在`Current data`中  
![require控件](/img/require05.png)

**Token balance**  
Evabase 封装了获取 ERC20 Token 余额方法，点击 ➊ 将弹出 token 选择弹窗，选择 token 后，在 ➋ 选择或输入要查询的该 toten 余额的地址，然后同上`Current data`中调用合约获取数据。
![require控件](/img/require06.png)

**固定值**  
固定值支持 4 种类型：

1. Number: bigint 整数固定值（必须不小于 0）。
2. Address: 地址固定值,必须是一个合法的地址。
3. Bool: 布尔固定值。
4. Bytes32: 字节固定值（最长 32 字节）。
   ![require控件](/img/require07.png)
