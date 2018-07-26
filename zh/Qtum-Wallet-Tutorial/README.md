### 概览 (Overview)

这是 Qtum 量子链钱包的“**概览**”界面，也是启动之后的默认界面，可以看到下面这些信息：

1. 余额

- 可使用的余额
- 等待中的余额
- 总额
- 其他代币

2. 最近交易记录

![overview](overview.png)


### 发送 (Send)

在发送界面中，可以向 Qtum 地址发送 Qtum 。

![send](send.png)

**付给：** 在此处输入想要发送的Qtum接收地址，**请注意只有Qtum地址有效**。
**标签：** 可选项，给上面输入的地址打标签。
**金额：** 在此处输入要发送的Qtum数额。

填写完各项后，点击发送，等待3秒后再次确认，即可将 Qtum 发送至目标地址。你也可以点击下方的添加收款人同时发送到多个地址。

![beforesend](beforesend.png)

#### 找零地址

默认的找零地址是随机生成的新地址，可以通过偏好设置来管理找零地址。在偏好设置->钱包界面，勾选 "Don't use change address" 将使用发送地址作为找零地址，勾选“启用货币控制功能“可以在发送时指定找零地址。

![change address](change-address.png)

### 接收 (Receive)

在这里可以生成 Qtum 接收地址，并看到过往的接收地址。

![Receive](receive-1.png)

点击“请求付款”可以生成一个新的 Qtum 地址，同时也可以指定金额和备注。下图示例中填写了10个 Qtum 作为付款金额。

![Receive](receive-2.png)


### 智能合约 (Smart Contract)

@todo


### 交易记录 (Transactions)

该页显示钱包所有地址的交易记录，包括收入、支出、发送代币、挖矿等。

![transactions](transactions.png)


### QRC 代币 (QRC Token)

在这里，可以发送、接收、添加 QR C代币，也可以通过开启 "log events" 查看QRC代币的交易记录。

![qrc token](qrc.png)

#### 添加代币
点击 "Add Token" 可以添加一个新的 QRC 代币。
**Contract Address**: 代币合约地址。
**Token Name**: 代币名称，填写完合约地址后回自动识别出来。
**Token Symbol**:  代币符号，填写完合约地址后回自动识别出来。
**Decimals**: 小数位，填写完合约地址后回自动识别出来。
**Token Address**: 用于接收代币的 Qtum 地址，通过下拉选择一个地址。
填写完以上信息之后，点击 "Confirm" 即可添加一个QRC代币到你的钱包。同一个代币绑定同一个 Qtum 地址只能添加一次。

![add token](add-token.png)

#### 发送代币
在左侧选择一个代币，点击 "Send" 进 入发送界面，与发送Qtum有些相似。
**PayTo**: 代币接收地址。
**Amount**: 代币数量，最大值为当前余额，注意少数代币最大发送数额必须小于当前余额，如INK。
**Description**:  本次交易备注，可选项。
**GasLimit**: 默认即可。
**GasPrice**: 默认即可。
填写完以上信息之后，点击 “Confirm" 即可发送QRC代币到指定地址。

![send token](send-token.png)

#### 接收代币
接收代币十分简单，选择一个代币，点击 "Receive" 右侧即出现接收地址，也可以右键点击，选择 "Copy receive address" 。

![receive token](receive-token.png)

#### 开启 "log events"
在偏好设置->主要界面，勾选 "Enable log events" ，点击确认后钱包会重启并开启 "log events" ，此时即可查看 QRC 代币交易记录。

![enable log events](enable-log-events.png)


### 加密钱包

首先，在备份钱包之前加密你的钱包将使得你的备份也被加密。点击 "Settings -> Encrypt Wallet" 。

![encrypt wallet](encrypt-1.png)

然后，然输入密码，**请务必保管好这个密码，否则你会丢掉你的Qtum**。

![encrypt wallet](encrypt-2.png)

输入完两个密码并确认之后，钱包会自动重启，并变成加密模式。


### 备份钱包

强烈推荐**加密钱包之后**再备份钱包！

点击 "File -> Backup Wallet" 以备份钱包。

![backup wallet](backup-1.png)

输入备份的文件名，选择好保存位置后点击保存，即可备份钱包。

![backup wallet](backup-2.png)


### 从备份中恢复钱包

最新版本的 Qtum 钱包已经在界面上实现了备份管理。你可以轻松的备份、恢复你的钱包。
​

#### Mac系统

点击 "File ->  Restore Wallet" ，在弹出的对话框里选择要恢复的钱包备份文件。

![restore](restore-1.png)

![restore](restore-2.png)

通常情况下选择```reindex```选项即可，除非你遇到特殊的情况。


#### Windows系统

和 Mac 系统下操作基本一样。


#### Linux系统

和 Mac 系统下操作基本一样。


### 挖矿

当你满足如下条件时就可以进行挖矿：

1. 钱包中有超过500个确认的 Qtum ；
2. 解锁钱包；
3. 保持钱包在线状态。

更多细节可以参考：[http://docs.qtum.site/zh/How-to-Staking-with-Qtum/](http://docs.qtum.site/zh/How-to-Staking-with-Qtum/)