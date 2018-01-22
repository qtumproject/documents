### 概览 (Overview)

这是Qtum量子链钱包的“**概览**”界面，也是启动之后的默认界面，可以看到下面这些信息：

1. 余额

- 可使用的余额
- 等待中的余额
- 总额
- 其他代币

2. 最近交易记录

![overview](https://s.qtum.site/uploads/a8474d1ed50c7a3fe102e667e39fc08a.jpg)


### 发送 (Send)

在发送界面中，可以向Qtum地址发送Qtum。
![send](https://s.qtum.site/uploads/95ff75d66db79da8f74d6eec4fb9cc21.png)

**付给：** 在此处输入想要发送的Qtum接收地址，**请注意只有Qtum地址有效**。
**标签：** 可选项，给上面输入的地址打标签。
**金额：** 在此处输入要发送的Qtum数额。

填写完各项后，点击发送，等待3秒后再次确认，即可将Qtum发送至目标地址。你也可以点击下方的添加收款人同时发送到多个地址。
![send](https://s.qtum.site/uploads/5ea4e80e7ad7f80cd5fc2da227bdea67.png)

#### 找零地址

默认的找零地址是随机生成的新地址，可以通过偏好设置来管理找零地址。在偏好设置->钱包界面，勾选"Don't use change address"将使用发送地址作为找零地址，勾选“启用火币控制功能“可以在发送时指定找零地址。
![change address](https://s.qtum.site/uploads/1ce40c095dff4fd23d7975293ae48077.png)

### 接收 (Receive)

在这里可以生成Qtum接收地址，并看到过往的接收地址。
![Receive](https://s.qtum.site/uploads/7107208942f0a7ac084f6e08713ebff2.png)

点击“请求付款”可以生成一个新的Qtum地址，同时也可以指定金额和备注。下图示例中填写了10个Qtum作为付款金额。
![Receive](https://s.qtum.site/uploads/922636d8a94e03136de58ebdf7f4d4d5.png)


### 智能合约 (Smart Contract)

@todo


### 交易记录 (Transactions)

该页显示钱包所有地址的交易记录，包括收入、支出、发送代币、挖矿等。
![transactions](https://s.qtum.site/uploads/a8474d1ed50c7a3fe102e667e39fc08a.jpg)


### QRC 代币 (QRC Token)

在这里，可以发送、接收、添加QRC代币，也可以通过开启"log events"查看QRC代币的交易记录。
![qrc token](https://s.qtum.site/uploads/caf5288989c2c7d191c315eb5480a0bb.jpg)

#### 添加代币
点击"Add Token"可以添加一个新的QRC代币。
**Contract Address**: 代币合约地址。
**Token Name**: 代币名称，填写完合约地址后回自动识别出来。
**Token Symbol**:  代币符号，填写完合约地址后回自动识别出来。
**Decimals**: 小数位，填写完合约地址后回自动识别出来。
**Token Address**: 用于接收代币的Qtum地址，通过下拉选择一个地址。
填写完以上信息之后，点击"Confirm"即可添加一个QRC代币到你的钱包。同一个代币绑定同一个Qtum地址只能添加一次。
![add token](https://s.qtum.site/uploads/58d4fa9db9baadfa3bb562ac9159d119.png)

#### 发送代币
在左侧选择一个代币，点击"Send"进入发送界面，与发送Qtum有些相似。
**PayTo**: 代币接收地址。
**Amount**: 代币数量，最大值为当前余额，注意少数代币最大发送数额必须小于当前余额，如INK。
**Description**:  本次交易备注，可选项。
**GasLimit**: 默认即可。
**GasPrice**: 默认即可。
填写完以上信息之后，点击“Confirm"即可发送QRC代币到指定地址。
![send token](https://s.qtum.site/uploads/3ffbaeec9a0fb6ca27419869edd3cd22.png)

#### 接收代币
接收代币十分简单，选择一个代币，点击"Receive"右侧即出现接收地址，也可以右键点击，选择“Copy receive address"。
![receive token](https://s.qtum.site/uploads/909bfef7ddc127936d5af35067e87bc6.png)

#### 开启"log events"
在偏好设置->主要界面，勾选"Enable log events"，点击确认后钱包会重启并开启"log events"，此时即可查看QRC代币交易记录。
![enable log events](https://s.qtum.site/uploads/323a99782406fb6525ed0be9fab3246e.png)


### 加密钱包

首先，在备份钱包之前加密你的钱包将使得你的备份也倍加密。点击"Settings -> Encrypt Wallet"。
![encrypt wallet](https://s.qtum.site/uploads/21cf1e8e477ba04e1a7f5924f733662b.jpg)

然后，然输入密码，**请务必保管好这个密码，否则你会丢掉你的Qtum**。
![encrypt wallet](https://s.qtum.site/uploads/35bfd89a3f4dd199a84d6dbce237fce9.png)

输入完两个密码并确认之后，钱包会自动重启，并变成加密模式。


### 备份钱包

强烈推荐**加密钱包之后**再备份钱包！

点击"File -> Backup Wallet"以备份钱包。
![backup wallet](https://s.qtum.site/uploads/27b682aea3931eec88f9ef9e73682b29.png)

输入备份的文件名，选择好保存位置后点击保存，即可备份钱包。
![backup wallet](https://s.qtum.site/uploads/88cd46b92d811f46e538d3646a5bee24.png)


### 从备份中恢复钱包

最新版本的Qtum钱包已经在界面上实现了备份管理。你可以轻松的备份、恢复你的钱包。
​

#### Mac系统

点击"File ->  Restore Wallet"，在弹出的对话框里选择要恢复的钱包备份文件。

![Receive](http://92.222.69.86/images/restore.png)

![Receive](http://92.222.69.86/images/restore2.png)

![Receive](http://92.222.69.86/images/restore3.png)

通常情况下选择```reindex```选项即可，除非你遇到特殊的情况。


#### Windows系统

和Mac基本一样。

![Receive](http://92.222.69.86/images/win/1.jpg)

![Receive](http://92.222.69.86/images/win/3.jpg)

![Receive](http://92.222.69.86/images/win/4.jpg)

![Receive](http://92.222.69.86/images/win/2.jpg)


#### Linux系统

和Mac的也没差多少。

![Receive](http://92.222.69.86/images/linux/4.jpg)

![Receive](http://92.222.69.86/images/linux/1.jpg)

![Receive](http://92.222.69.86/images/linux/8.jpg)

![Receive](http://92.222.69.86/images/linux/5.jpg)

![Receive](http://92.222.69.86/images/linux/10.jpg)

![Receive](http://92.222.69.86/images/linux/9.jpg)

![Receive](http://92.222.69.86/images/linux/2.jpg)


### 挖矿

当你满足如下条件时就可以进行挖矿：

1. 钱包中有超过500个确认的Qtum；
2. 解锁钱包；
3. 保持钱包在线状态。

更多细节可以参考：https://github.com/qtumproject/documents/blob/master/zh/How-to-Staking-with-Qtum.md