# QtumX一键发链教程

# 下载
从[Github](https://github.com/qtumproject/qtum-enterprise/releases)下载最新的安装包，安装至任意目录。

# 注册登录
1. 运行qtumd或者qtum-qt，启动Qtum主链。
2. 打开QT钱包的 Help - Debug window - Console 或是通过qtum-cli执行rpc命令。
3. 执行getnewaddress命令，生成一个新的地址作为账户，记录下来。
4. 执行dumpprivkey命令，获得新地址的私钥，记录下来。
5. 打开QtumX[主页](https://qtumx.net/)，点击LOGIN，进入登录页。
6. 执行signmessage命令，使用刚才生成的地址对登陆页中的message进行签名，将签名结果填进登陆页。
7. 点击LOGIN完成登录。
![image](3.jpg)
![image](4.jpg)

# 搭建私链
为了便于理解，我们先介绍如何建立自己的私链。

## 生成配置
点击LAUNCH A NEW CHAIN，进入发链页。填写好所有新链的信息后，点击SUBMIT发布新链。各字段的含义如下。
1. Chain id：链名，只支持小写字母和数字，唯一。例如mychain123。
2. Token name：币名，只支持大写字母和数字，唯一。例如BTC、QTX。
3. Description：链的描述，用来介绍该链，也用于生成创世区块。例如：my first blockchain。
4. Message Header：网络包头，用于在网络传输的时候区分不同的链。4字节长度，十六进制表示，即8个0-9a-f的字符，例如：1234fedc。
5. Algorithm：共识算法。目前仅支持PoA共识，后续会提供更多选择。想更多了解PoA共识，参考[QtumX技术白皮书](https://docs.qtum.org/zh/Technical-White-Paper-for-QtumX/)。
6. Miner list: PoA的矿工列表，一个或多个address，逗号分隔。我们第一步建立私链，则使用默认填入的账户地址。
7. Block interval、Timeout：见技术白皮书，可直接使用默认值。
8. Default port：默认的端口地址。
9. Dns seed、Ip seed：新的节点在加入的时候，默认连接的网络中的种子节点。由于是私链，此处留空。
10. Init Reward：初始每个块的奖励。
11. Halving interval：奖励在多少个块后折半。
12. Halving times：最多折半几次。

## 启动私链
我们生成了一个名为x的链（[链接](https://qtumx.net/#/chain/view?chainId=x)），按以下步骤启动该链。
1. 使用 qtumd -chain=x 或是 在qtum-qt中如下图配置重启后，启动名为x的链。
![image](1.jpg)
1. 执行importprivkey命令，导入账户的私钥。
2. 执行setpoaminer命令，开始使用账户挖矿。每次节点重启后需要运行该命令开启挖矿。
3. 可以从QT钱包或是执行getblockchaininfo命令，看到block数在不断增加。
![image](2.jpg)
5. 新链启动成功，试着发交易或是智能合约吧！

## 连接私链
假设我们已经在机器A上启动了私链x并进行挖矿，这时我们需要在机器B上启动节点并接入该私链。
1. 在机器B上使用 qtumd -chain=x 或是 在qtum-qt配置后启动链x的节点。
2. 运行 addnode "ip_A" add 命令，连接机器A上的节点。
3. 连接之后，可以通过getpeerinfo命令查看节点情况。
4. 试着在两个节点之间互发交易吧！

# 种子节点
区块链新节点在启动的时候可以通过连接种子节点（seed）快速地找到网络，省去了上文中addnode的步骤。种子节点可以是一个ip或是一个域名，对应的服务器上保持有节点运行。以下讲解配置种子节点的流程。
1. 新建一条名为xx的链（[链接](https://qtumx.net/#/chain/view?chainId=xx)），Dns seed中填写自己的域名，或是Ip seed中填写一台自己的服务器地址。如果使用域名的话，请将域名解析到自己的服务器上。
```
Dns seed:  beta.qtumx.net
Ip seed:  116.62.70.220
```
2. 登录服务器（116.62.70.220），使用 ./qtumd -chain=xx 的方式启动节点
```
root@116.62.70.220:./qtumd -chain=xx -daemon
```
3. 配置完成，这时候使用任何机器启动xx链，都会连接到种子节点获取数据。可以通过getpeerinfo看到连接上的节点。
![image](6.jpg)

