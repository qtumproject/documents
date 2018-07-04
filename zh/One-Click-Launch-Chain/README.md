# QtumX一键发链教程

# 下载
从[Github](https://github.com/qtumproject/qtum-enterprise/releases)下载最新的安装包，安装至任意目录。

# 登录
1. 运行qtumd或者qtum-qt，启动Qtum主链。
2. 打开QT钱包的 Help - Debug window - Console 或是通过qtum-cli执行rpc命令。
3. 执行getnewaddress命令，生成一个新的地址作为账户，记录下来。
4. 执行dumpprivkey命令，获得新地址的私钥，记录下来。
5. 打开QtumX[主页](https://qtumx.net/)，点击LOGIN，进入登录页。
6. 执行signmessage命令，使用刚才生成的地址对登陆页中的message进行签名，将签名结果填进登陆页。
7. 点击LOGIN完成登录。

# 建立自己的私链
为了简单起见，我们先介绍如何建立自己的私链。

点击LAUNCH A NEW CHAIN，进入发链页。填写好所有新链的信息后，点击SUBMIT发布新链。
1. Chain id：链名，只支持小写字母和数字，唯一。例如mychain123、x。
2. Token name：币名，只支持大写字母和数字，唯一。例如BTC、QTX。
3. Description：链的描述，用来介绍该链，也用于生成创世区块。例如：qtumx official blockchain。
4. Message Header：网络包头，用于在网络传输的时候区分不同的链。4字节长度，十六进制表示，即8个0-9a-f的字符，例如：1234fedc。
5. Algorithm：共识算法。目前仅支持PoA共识，后续会提供更多选择。想更多了解PoA共识，参考[QtumX技术白皮书](https://docs.qtum.org/zh/Technical-White-Paper-for-QtumX/)。
6. Miner list: PoA的矿工列表，一个或多个address，逗号分隔。我们第一步建立私链，则使用默认填入的账户地址。
7. Block interval、Timeout：见技术白皮书。
8. Default port：默认的端口地址。
9. Dns seed、Ip seed：新的节点在加入的时候，默认连接的网络中的种子节点。由于是私链，此处留空。
10. Init Reward：初始每个块的奖励。
11. Halving interval：奖励在多少个块后折半。
12. Halving times：最多折半几次。

# 启动自己的私链
1. 使用 qtumd -chain=x 或是 在qtum-qt中如下图配置重启后，启动名为x的链。
![image](1.jpg)
2. 执行importprivkey命令，导入账户的私钥。
3. 执行setpoaminer命令，开始使用账户挖矿。
4. 可以从QT钱包或是执行getblockchaininfo命令，看到block数在不断增加。
![image](2.jpg)
5. 新链启动成功，试着发交易或是智能合约吧！
