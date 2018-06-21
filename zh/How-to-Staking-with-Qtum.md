# Qtum量子链Staking（PoS挖矿）教程

Qtum采用PoS共识机制，与比特币等采用的PoW机制有所不同。与比特币中挖矿类似，Qtum PoS机制中称为Staking。**为方便读者理解，本教程统一将该过程表述为“Staking（挖矿）”**。每次Staking（挖矿）成功可累计获得至少**4 QTUM**作为奖励。实际获得奖励一般超过4QTUM，因为交易手续费和合约调用费用也将作为Staking（挖矿）奖励。

开始Staking（挖矿）需满足两个基本条件：

1. 运行Qtum全节点，并保持在线（不需要矿机，任何PC/Mac，甚至树莓派都可以运行Qtum全节点）；
2. 拥有QTUM量子币（无论数量多少都可以Staking（挖矿），但拥有Qtum数量越多，挖到矿的可能性越高）。

如果你还没有QTUM量子币，请先通过各种平台获取一定数量QTUM备用。

Qtum官方核心钱包可以运行Qtum全节点，是目前唯一支持Staking（挖矿）的钱包。请注意，**手机钱包不支持Staking（挖矿）**。

有两种方式进行Staking（挖矿）：

* 方式一：用命令行运行`qtumd`进行Staking（挖矿）；
* 方式二：用带有图形界面的`qtum-qt`钱包进行Staking（挖矿）。

方式一适用于熟悉Linux/OSX/Windows命令行操作的用户，包括树莓派用户；方式二适用于适用有图形界面钱包的用户。读者可以根据自身需求选择其中一种方式进行Staking（挖矿）。两种方式完全等效，Staking（挖矿）效果没有任何区别。

## 方式一：用命令行运行`qtumd`进行Staking(挖矿)

### 1. 运行`qtumd`

`qtumd`运行和交互的方法请参考教程《[如何部署Qtum量子链节点](Guidance-of-Qtum-Deployment-and-RPC-Settings.md)》中“获取Qtum节点”和“部署Qtum节点”部分。

按照以上教程运行`qtumd`:

```
./qtumd -daemon
```

Staking（挖矿）功能在钱包未加密时将默认开启，无需其他设置。 

### 2. 转入QTUM量子币

首先获取钱包地址，命令为：

```
./qtum-cli getnewaddress
```

命令将返回一个新生成的地址，地址以Q开头。可以向该地址转入一笔或多笔QTUM用于Staking（挖矿）。读者可以用同样方法生成任意多地址，并向地址中转入任意多笔Qtum进行Staking（挖矿）。

注意：**刚转入的QTUM需要等待500个区块确认才可用于Staking（挖矿），即大概需要等待17小时**。这与Qtum采用的MPoS共识机制有关，对其运行原理感兴趣的读者可以参考《[Qtum区块链指南](Qtum-Blockchain-Guide.md#mpos共识算法)》进一步了解。

在区块同步完成后，可以通过`./qtum-cli getbalance`查看钱包余额，或`./qtum-cli listunspent`查看所有UTXO。（[什么是UTXO?](Qtum-Blockchain-Guide.md#utxo账户模型)）。

建议在QTUM转入500个区块后再进行以下步骤，因为确认数小于500个的UTXO无法进行Staking（挖矿）。

### 3. 查看Staking状态

通过以下命令可以查看staking状态：

```
./qtum-cli getstakinginfo
```

运行类似结果如下：

```
{
  "enabled": true,
  "staking": true,
  "errors": "",
  "currentblocksize": 1000,
  "currentblocktx": 0,
  "pooledtx": 5,
  "difficulty": 5683612.564280176,
  "search-interval": 46,
  "weight": 53206430,
  "netstakeweight": 2278172497819029,
  "expectedtime": 5480654870
}
```

其中`enabled`代表是否开启Staking（挖矿）功能，该功能是默认开启的;`staking`代表目前是否有QTUM正在Staking（挖矿），`true`即代表正在Staking;`weight`代表目前正在staking（挖矿）的Qtum数量，单位是10^-8QTUM，本例子中约0.532QTUM;`expectedtime`代表目前你挖到矿的期望时间，单位是秒。

### 4. 加密的钱包如何Staking（挖矿）？

如果读者不需要对钱包加密，请跳过此步骤。但是钱包未加密状态下，通过钱包收发QTUM将

钱包可以通过`encryptwallet`命令进行加密，进一步保证资金安全。然而，在钱包加密的状态下，Staking功能将被默认关闭。加密后`./qtum-cli getstakinginfo`将获得如下结果：

```
{
  "enabled": true,
  "staking": false,
  "errors": "",
  "currentblocksize": 1000,
  "currentblocktx": 0,
  "pooledtx": 94,
  "difficulty": 5788429.670171153,
  "search-interval": 0,
  "weight": 53206430,
  "netstakeweight": 2438496688951881,
  "expectedtime": 0
}
```

注意`staking`状态变为`false`，说明没有在Staking（挖矿）。

通过如下`walletpassphrase`命令可以对钱包进行解锁：

```
./qtum-cli walletpassphrase "<你设置的密码>" 99999999 true
```

其中第一个参数为用户加密时设置的密码，第二个参数`99999999`为需要解锁的时间，单位是秒，可以根据用户需要进行设置；第三个参数表示是否只解锁staking功能，设置为true则表示只解锁用于Staking（挖矿），而发送QTUM仍需要输入密码。若第三个参数缺省，则表示完全解锁钱包，不仅可以Staking，也可以正常发送QTUM。

解锁后用`getstakinginfo`可查看状态，一切正常的话即可以在钱包加密状态下Staking(挖矿)了。

## 方式二：用有用户界面的Qtum-qt钱包Staking（挖矿）

Qtum-qt钱包的基本使用方法请参考[qt钱包教程(点击打开)](Qtum-Wallet-Tutorial.md)。目前支持的Mac/Linux/Windows，用户可以自行下载安装。

### 1. 打开Qtum qt钱包

打开已经安装好的Qtum钱包。

### 2. 转入QTUM量子币

如果钱包中已有QTUM可跳过此步骤。

若钱包中无QTUM，则向钱包地址中转入一定数量的QTUM，方法请参考[qt钱包教程(点击打开)](Qtum-Wallet-Tutorial.md)。

注意，新转入的QTUM需要等待500个区块（约17小时）的成熟时间，才可进行Staking（挖矿）。因此，建议用户等待500个区块后再进行以下步骤。

### 3. 查看Staking（挖矿）状态

通过钱包右下角的闪电标志可以查看Staking（挖矿）的状态。

**若闪电为实心，表示正在Staking（挖矿）**。将鼠标放到闪电标志上，可以看到Staking（挖矿）相关信息，如下图所示：

![正在Staking（挖矿）](https://s.qtum.site/uploads/898c1564fa8ea81b4383047c1f047f98.png)

* `Staking`表示正在挖矿；
* `Your weight is`表示当前你正在参与Staking（挖矿）的QTUM数量，单位是1QTUM；
* `Network weight is`表示网络中正在参与Staking（挖矿）的QTUM数量，单位是1QTUM；
* `Expected time`表示挖到矿的期望时间，单位是天。

**若闪电为空心，表示不在Staking（挖矿）**。可能的原因有：

* 钱包里没有超过500个区块确认的QTUM -- 解决方法：这时请向钱包转入QTUM，并等待500个区块（约17小时）；

![没有成熟的QTUM导致无法Staking](https://s.qtum.site/uploads/ff56f4442175cfadfffe5cda9561510f.png)

* 钱包处于锁定状态 -- 解决方法：解锁钱包。[如何解锁钱包?](Encrypt-and-Unlock-Qtum-Wallet/README.md)

![钱包未解锁导致无法Staking](https://s.qtum.site/uploads/55e240b15626dcc9f9c6d3b31e5094f8.jpeg)

**若无闪电标志，说明禁用了Staking功能**

* 钱包未开启staking功能 -- 解决方法：修改运行参数或配置文件，开启Staking。[如何添加配置文件？](Guidance-of-Qtum-Deployment-and-RPC-Settings.md#rpc调用设置)

![钱包未开启Staking](https://s.qtum.site/uploads/2626afb29dbab216326e8a6f2b9aec10.jpeg)

## 关于Staking（挖矿）奖励

如果用户顺利挖到一个区块，可以累积获得超过4QTUM的奖励。关于挖矿奖励有以下几点需要注意：

* 奖励会以一笔新交易的形式发送给你，命令行用户可通过`getbalance`命令查看余额变化，qt钱包用户可以直接看到收入的交易；
* Staking（挖矿）成功，你会立刻收到一笔0.4QTUM的奖励；
* **剩余3.6QTUM的奖励会在500个区块（约17个小时）之后，在连续九个区块中奖励给你，每个区块你将获得0.4QTUM**，与上条中0.4QTUM合计共4QTUM；
* Staking（挖矿）成功的那个币（UTXO）将被锁定500个区块，直到500区块之后才可以进行交易或继续进行Staking（挖矿）。为了不让资金锁定太久，用户可以选择将一个大的UTXO分成若干个较小的UTXO，这样只有挖到矿的那个UTXO会被锁定；

这一奖励机制和Qtum采用的MPoS机制有关，有兴趣了解原理的读者可以参考《[Qtum区块链指南](Qtum-Blockchain-Guide.md#mpos共识算法)》。

## 如何关闭Staking（挖矿）功能

Qtum钱包会默认开启Staking（挖矿），但有些情况用户或交易所想要关闭该功能。有以下几种方式可以停止Staking（挖矿）：

1 命令行用户可以在运行时加上`-staking=false`选项，如：

```
./qtumd -staking=false -daemon
```

启动qt钱包的命令：

```
./qtum-qt -staking=false
```

2 在配置文件`qtum.conf`中添加`staking=false`，[如何使用配置文件？](Guidance-of-Qtum-Deployment-and-RPC-Settings.md#rpc调用设置)

3 锁定钱包，钱包在锁定状态下会自动停止Staking。[如何锁定钱包？](Encrypt-and-Unlock-Qtum-Wallet/README.md)
