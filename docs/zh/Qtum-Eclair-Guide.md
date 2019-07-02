# Qtum 闪电网络客户端 Qtum Eclair 使用教程

区块链的可扩展性是实现海量交易的关键，目前比特币网络能达到每秒最多7笔的处理能力，Qtum网络目前可以实现比特币10陪的处理能力，但对于海量交易来说是不够的（例如电子商务应用场景，近年阿里巴巴双十一购物节，支付宝网络峰值交易超过每秒100000交易（TPS）；Visa在2013假期期间，实现每秒47000交易（TPS））。为了解决这种海量交易带来的处理和存储问题，Joseph Poon提出了闪电网络（Lightning Network）解决方案，闪电网络是一个去中心化的系统，无需信任对方以及第三方即可实现实时、海量的交易网络。其基本思想是交易双方在链上通过交易脚本创建支付通道，之后双方实时、海量的支付交易在链下完成，通过链接多个通道可以实现网络内任意两点之间的资金交易，完成价值转移，而无需信任第三方进行资金托管和结算，这些转移可以在不受信任的双方之间通过合约沿着传送路径进行。

Eclair 是一个在比特币区块链上对闪电网络的一个参考实现，目前可以支持闪电网络的支付通道创建、接收付款等功能。Qtum在 Eclair 的基础上做了相应修改形成Qtum Eclair，使得在 Qtum 下也可以实现诸如通道创建、实时交易、小额交易等功能。下面在通过在Qtum 测试网络(testnet) 对这几个闪电网络功能进行测试。

## 1. 安装运行Qtum Core钱包

Qtum Eclair 需要一个同步过的，非修剪的，支持segwit、zeromq、转账以及交易索引的 Qtum Core 钱包。 
Qtum Eclair 将使用它在 Qtum Core 钱包中找到的任何 Qtum 来支付您选择打开的任何闪电网络通道。 
当通道关闭时，通道内的 Qtum余额 将返回到 Qtum Core 钱包中。
您可以将 Qtum Core 钱包配置为使用 p2sh-segwit 地址或 bech32 地址，Qtum Eclair 与这两种模式都兼容。 

核心钱包下载地址: https://github.com/qtumproject/qtum/releases，选择对应的操作系统和架构下载程序包。 

创建并编辑配置文件 `qtum.conf` 为如下内容：
```
server=1
rpcuser=foo
rpcpassword=bar
txindex=1
addresstype=bech32
zmqpubrawblock=tcp://127.0.0.1:29000
zmqpubrawtx=tcp://127.0.0.1:29000
```

配置文件中的**rpcuser**和**rpcpassword**建议修改为更安全的值。

* 在 Linux 下，`qtum.conf`的路径为 `~/.qtum/qtum.conf` 
* 在 Mac OSX 下，`qtum.conf`的路径为 `~/Library/Application\ Support/Qtum/qtum.conf`
* 在 Windows 下，`qtum.conf`的路径为 `%APPDATA%\Qtum\qtum.conf`

运行 Qtum Core 钱包，等待区块同步完毕，并发送一定数量的测试币到此钱包中。

测试币可在 http://testnet-faucet.qtum.info/ 领取。

## 2. 安装 Qtum Eclair

### 2.1 安装 JDK 和 Maven

Qtum Eclair使用Scala语言进行开发，要运行 Qtum Eclair 首先得要安装 JDK 环境，推荐使用 OpenJDK 11 或以上版本。

* 在 Linux 下，`apt-get install default-jdk`
* 在 Mac OSX 下，`brew cask install adoptopenjdk`
* 在 Windows 下，从 https://jdk.java.net/archive/ 下载安装程序。

同时还需要安装Maven，可从 http://maven.apache.org/download.cgi 下载。

执行`mvn -v`, 得到类似如下的返回表明安装成功
![](https://imgur.com/SLLa58n.png)

### 2.2 编译 Qtum Eclair

* `git clone https://github.com/qtumproject/lightning-demo.git`
* `cd lightning-demo`
* `mvn install -DskipTests`

## 3. 运行 Qtum Eclair

创建并编辑配置文件 `~/.qtum-eclair/eclair.conf`，内容如下：

```
eclair {
  chain = "testnet" // "mainnet" for mainnet, "testnet" for testnet, "regtest" for regtest
  server {
    public-ips = []
    binding-ip = "0.0.0.0"
    port = 9735
  }
  api {
    enabled = false
    binding-ip = "127.0.0.1"
    port = 8080
    password = "qtum-eclair"
    use-old-api = false
  }

  watcher-type = "bitcoind"
  bitcoind {
    host = "localhost"
    rpcport = 13889
    bitdir = ""
    rpcuser = "foo"
    rpcpassword = "bar"
    zmqblock = "tcp://127.0.0.1:29000"
    zmqtx = "tcp://127.0.0.1:29000"
  }

  default-feerates {
    delay-blocks {
      1 = 1200000
      2 = 1000000
      6 =  800000
      12 = 600000
      36 = 500000
      72 = 410000
    }
  }
  min-feerate = 400
  smooth-feerate-window = 6 // 1 = no smoothing
  node-alias = "qtum-eclair"
  node-color = "49daaa"
  global-features = ""
  local-features = "8a"
  override-features = []
  channel-flags = 1
  dust-limit-satoshis = 72800
  max-htlc-value-in-flight-msat = 500000000000 // 5 QTUM
  htlc-minimum-msat = 1
  max-accepted-htlcs = 30
  reserve-to-funding-ratio = 0.01
  max-reserve-to-funding-ratio = 0.05
  to-remote-delay-blocks = 3600
  max-to-local-delay-blocks = 10080
  mindepth-blocks = 3
  expiry-delta-blocks = 720
  fee-base-msat = 400000
  fee-proportional-millionths = 100
  max-feerate-mismatch = 1.56
  update-fee_min-diff-ratio = 0.1
  revocation-timeout = 20 seconds
  ping-interval = 30 seconds
  ping-timeout = 10 seconds
  ping-disconnect = true
  auto-reconnect = true
  payment-handler = "local"
  payment-request-expiry = 1 hour
  min-funding-satoshis = 1000000  // 0.01 Qtum
  max-payment-attempts = 5
  autoprobe-count = 0

  router {
    randomize-route-selection = true
    channel-exclude-duration = 60 seconds
    broadcast-interval = 60 seconds
    init-timeout = 5 minutes

    path-finding {
      max-route-length = 6 
      max-cltv =  5040
      fee-threshold-sat = 8400
      max-fee-pct = 0.03
      heuristics-enable = true
      ratio-cltv = 0.15            
      ratio-channel-age = 0.35  
      ratio-channel-capacity = 0.5 
    }
  }
}

// do not edit or move this section
eclair {
  backup-mailbox {
    mailbox-type = "akka.dispatch.BoundedMailbox"
    mailbox-capacity = 1
    mailbox-push-timeout-time = 0
  }
  backup-dispatcher {
    executor = "thread-pool-executor"
    type = PinnedDispatcher
  }
}

```

上述配置文件中的**public-ips**为本机公网IP的数组，同时 **rpcuser**、**rpcpassword** 也要做相应的修改。

使用命令 `java -jar ./eclair-node-gui/target/lightning-capsule.jar` 启动客户端。

![](https://imgur.com/pb2fkTb.png)

## 4. 创建闪电网络通道

![](https://imgur.com/WMGMVNX.png)
在本地的 Qtum Eclair 客户端左下角右键选择 “Copy URI” 即可得到自己的节点地址。

![](https://imgur.com/6xUx3TP.png)
点击左上角的 "Channel" 按钮，选择 “Open Channel”。

![](https://imgur.com/ceB9BsU.png)
在弹出的页面中，填入通道对方的URI，和通道的容量，这里设为了10个 QTUM。
点击 “Connect”，创建通道，这时还需要等到6个区块，让交易得到确认，通道才真正创建成功。

![](https://imgur.com/YiTMOWN.png)

## 5. 闪电网络支付
通道建好之后就可以使用闪电网络进行微支付操作了。

![](https://imgur.com/J30F2F1.png)

点击左上角的 "Channel" 按钮，选择 “Reveive Payment”, 在弹出的页面中填写收款金额，点击 “Generate” 按钮，得到自己的收款地址。
这里我们选择了一个非常小的金额 1 Satoshi，相当于 0.00000001 个QTUM，如此小金额的转账，在不使用闪电网络的情况下是难以想象的。

![](https://imgur.com/nPVtrTY.png)
点击左上角的 "Channel" 按钮，选择 “Send Payment”, 在弹出的页面中填写对方的闪电网络收币地址和金额，点击“Send”按钮，即可向对方转账。

![](https://imgur.com/Aaem14c.png)
转账完成后，双方的金额瞬间发生了变化，因为这是纯链下的交易，无需等待区块确认，也无需支付手续费，。

## 6. 关闭通道进行结算
当通道不再需要的时候，可以关闭通道。

![](https://imgur.com/iOZxlg4.png)

点击 “Close” 按钮关闭通道。

![](https://imgur.com/LfQEWlm.png)

关闭后，通道内的 QTUM 余额就会返回各自的 Qtum Core 钱包内。

## 7. 使用 Docker 在服务器上快速部署 Qtum Eclair 服务

以上是普通用户的图形界面客户端使用教程，如果你想在服务器上部署 Qtum 闪电网络节点，可参考本小节进行快速部署。

* `sudo docker pull qtum/qtum:latest`
* `mkdir /opt/qtum`
* `vim /opt/qtum/qtum.conf`, 并输入如下配置信息：
```
server=1
rpcallowip=172.17.0.0/24
rpcbind=0.0.0.0
rpcuser=foo
rpcpassword=bar
txindex=1
addresstype=bech32
zmqpubrawblock=tcp://0.0.0.0:29000
zmqpubrawtx=tcp://0.0.0.0:29000
```

* `sudo docker run -tid --rm -v "/opt/qtum:/root/.qtum" --name qtum qtum/qtum:latest qtumd --testnet`
* 通过 `sudo docker exec -ti qtum qtum-cli --testnet getblockchaininfo`, 查看区块同步进度，等待区块完全同步


* `git clone https://github.com/qtumproject/lightning-demo.git`
* `cd lightning-demo`
* `mkdir /opt/qtum-eclair`
* `vim /opt/qtum-eclair/eclair.conf`, 并输入在第三节中的配置信息, 替换 bitcoind 下的 localhost 和 127.0.0.1 为`qtumhost`
* `sudo docker build -t qtum-eclair-img .`
* `sudo docker run -ti --rm --name qtum-eclair -v "/opt/qtum-eclair:/data" -p 9735:9735 --link qtum:qtumhost -e "JAVA_OPTS=-Declair.printToConsole" qtum-eclair-img`

## 8. Qtum Testnet 闪电网络公开节点

* URI：`030fa5900d9ddb1fb0641220b50e695c7e4a791dda682c9d70e1c20278d2f84a98@39.104.93.51:13415`

* URI：`02b88d5a2b3f3e5aba35a5fb4497294cf1cf15bb60532e788eeff756dc53633e7c@39.104.100.220:13435`

你可以与这些节点建立闪电网络通道进行微支付测试。

## 总结
通过以上的测试可以看到，基于 Qtum 的闪电网络的基本可以实现在链下进行实时的交易和结算，只涉及到两方的交易可以不用支付手续费，使得诸如小额支付等成为可能。理论上可以在通过在Qtum链下建立大量的闪电网络通道，把交易放在链下，可以实现实时、海量的交易。
