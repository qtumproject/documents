Qtum Electrum 是基于知名比特币钱包Electrum修改而来的一款Qtum桌面端轻钱包。
相比较于目前的Qtum Core全节点钱包，Qtum Electrum 占用的磁盘空间更小、同步区块所需时间更短，它支持多重签名和硬件钱包、支持冷钱包模式、支持导入手机钱包的助记词，同时采用了SPV验证保证了安全性。

## 功能介绍

### 下载安装

在浏览器中访问 [https://github.com/qtumproject/qtum-electrum/releases/latest](https://github.com/qtumproject/qtum-electrum/releases/latest) 即可找到最新版Qtum Electrum的下载链接。

![](http://ojaivn2ch.bkt.clouddn.com/825e23cb2418573327113f136c6e27ea.png)

请根据你的操作系统选择合适的二进制程序，portable 意为绿色版，数据都存储在自身目录下，可以放在U盘之类的地方；setup 意为安装版，将会在把程序安装在C盘程序目录下，并在桌面创建快捷方式；

如果你使用的是linux系统，请遵循 [https://github.com/qtumproject/qtum-electrum/blob/master/README.md](https://github.com/qtumproject/qtum-electrum/blob/master/README.md) 中的步骤安装依赖环境。

### 创建和恢复钱包

第一次打开钱包时，选择 “Auto Connect” 连接服务器。

接下来会提示选择创建钱包的种类,

![](http://ojaivn2ch.bkt.clouddn.com/cfaf17237ff138adf4c601eadedea24b.png)

推荐选择 “Standard Wallet”，这将使用遵循BIP44标准的模式创建助记词和公私钥，创建新钱包请继续选择 “Create a new seed”， 恢复助记词请选择 “I already have a seed”。

**请务必将助记词抄写在安全的地方进行备份。**
**请务必将助记词抄写在安全的地方进行备份。**
**请务必将助记词抄写在安全的地方进行备份。**

然后根据软件中的提示进行操作，建议为钱包设置一个安全的密码。

如果你要从已有的手机钱包助记词中恢复，请选择 “Qtum mobile wallet compatible” 选项。

如果你想将Qtum Core全节点钱包里的地址恢复到Qtum Electrum上，请执行`qtum-cli dumpwallet ~/Desktop/wallet.txt` 并将其中的 extended private masterkey 拷贝出来，并选择 “Qtum Qt Core wallet compatible” 选项。


### 收发QTUM

Qtum Electrum 的界面非常简洁，点击上面的按钮可进行tab间的切换。

![](http://ojaivn2ch.bkt.clouddn.com/e59638ccadae90e1f366534142340575.png)
点击右下角的设置按钮，在弹窗中的“Appearance”页下可以进行语言切换，“Chinese” 即为中文，设置完成后关闭软件，重新打开就能生效。
  
  

![](http://ojaivn2ch.bkt.clouddn.com/7cdacbe408a98d3a00a9e128beb26e30.png)
在 “发送” 页，填写对方的Qtum地址和金额，使用默认手续费，点击“发送”即可。
  
  

![](http://ojaivn2ch.bkt.clouddn.com/4e994a885963f09389d2c1be10e5924e.png)
在 “接收” 页，我们可以将地址或者二维码拷贝下来，发送给其他人。 由于Qtum Electrum使用的是一个助记词管理多个地址的模式，因此你会发现接收地址会经常变化。
  
  

![](http://ojaivn2ch.bkt.clouddn.com/d2ef6659a47a55686b6c6ef2fec58331.png)
在 “历史”页，可以查看所有的收发记录，双击可查看交易详情。

### 多重签名钱包
QTUM使用的是和比特币相同的多重签名机制，相比较于以太坊通过智能合约来实现多重签名管理大额资金，QTUM拥有更高的安全性。

如果你对多重签名不了解，请不要使用这个功能。

在 Qtum Electrum 中创建多重签名钱包非常简单。
![](http://ojaivn2ch.bkt.clouddn.comn/0e9cd174e07aa82ae5104c55704f4de7.png)
![](http://ojaivn2ch.bkt.clouddn.com/955ebe89b5d0e21918c91476fdabd44e.png)
在创建钱包的时候选择"Multi-signature wallet"
  

![](http://ojaivn2ch.bkt.clouddn.com/e418b21d572d84539c4df6efe944cc5c.png)
接着选择伙伴数量和最小所需签名数。
  

然后根据提示填写自己的助记词和伙伴提供的公钥，你的伙伴们需要进行相同的前述操作才能看到他们自己的公钥。
![](http://ojaivn2ch.bkt.clouddn.com/8d2c936a3b5b735c2c0a083eb8b06b76.png)
  

**任何时候都不要把自己的私钥或者助记词给别人。**
**任何时候都不要把自己的私钥或者助记词给别人。**
**任何时候都不要把自己的私钥或者助记词给别人。**

### 硬件钱包

这里将以 ledger 为例进行说明。

首先将 ledger 连接到电脑上并解锁，同时按下两个按键进入Qtum App。

新建钱包, 选择 “Standard wallet” -> “Use a hardware device”,  一直点“下一步”。
如果中间出现错误，请检查是否打开了其他钱包导致设备被占用，并尝试重新插拔ledger。
  
![](http://ojaivn2ch.bkt.clouddn.com/0b2b70d7163e15df5efe59448d54ebc7.png)
当软件右下角硬件钱包图标显示为小绿点是表示硬件钱包已经成功连接上。

使用硬件钱包发送QTUM时，点击“发送”之后需要在ledger进行确认。

## 后期规划

Qtum Electrum 将支持智能合约的部署、数据读取、函数调用。

Qtum Electrum正处于Beta公测阶段，如果你在使用过程中发现任何问题欢迎给我们提交issue [https://github.com/qtumproject/qtum-electrum/issues](https://github.com/qtumproject/qtum-electrum/issues)



