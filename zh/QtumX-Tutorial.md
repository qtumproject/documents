# QtumX使用教程（内测）

## 安装
根据自己的环境选择对应的安装包，下载至任意目录。目前提供的安装包列表如下：

```
qtum-0.15.1-aarch64-linux-gnu.tar.gz	
qtum-0.15.1-osx64.tar.gz		
qtum-0.15.1-win64.zip
qtum-0.15.1-arm-linux-gnueabihf.tar.gz	
qtum-0.15.1-win32-setup-unsigned.exe	
qtum-0.15.1-x86_64-linux-gnu.tar.gz
qtum-0.15.1-i686-pc-linux-gnu.tar.gz	
qtum-0.15.1-win32.zip
qtum-0.15.1-osx-unsigned.dmg		
qtum-0.15.1-win64-setup-unsigned.exe
```

其中exe结尾文件为windows下的安装文件，直接运行安装。dmg结尾的文件为mac osx下的安装文件，运行后拖拽图标至文件夹内即成功安装。其余包的安装方式都是解压后直接运行相应程序。内测期间源码暂不公开，后续会进行公开。

由于QtumX是基于Qtum 0.15.1版本开发，所以安装包的命名和其保持一致，若使用exe或dmg方式安装，则会覆盖系统中原本的Qtum程序。如果系统中原本已经安装了Qtum，建议使用解压的方式进行安装QtumX。

QtumX在不同环境下的默认数据存储目录如下。可以看到QtumX的数据位于Qtum默认目录的poa文件夹下，因此不会与Qtum的数据产生冲突。不过你也可以通过启动时通过命令行参数的方式手动指定目录。

```
// Windows < Vista: C:\Documents and Settings\Username\Application Data\Qtum\poa
// Windows >= Vista: C:\Users\Username\AppData\Roaming\Qtum\poa
// Mac: ~/Library/Application Support/Qtum/poa
// Unix: ~/.qtum/poa
```

## 启动
如果是exe或是dmg的方式安装，则直接点击安装后的图标启动。

如果是解压安装，则进入解压后的目录，运行 ./bin/qtumd 来启动命令行钱包，或是 ./bin/qtum-qt 启动QT图形界面的钱包。举例如下（mac osx环境）。


```
$ tar zxf qtum-0.15.1-osx64.tar.gz 
$ cd qtum-0.15.1
$ mkdir data

$ ./bin/qtumd -datadir=./data
or
$ ./bin/qtum-qt -datadir=./data
```

## 进入命令行
如果启动的是QT钱包，则进入Help-Debug window，然后点击控制台标签。如果是命令行钱包，则运行./bin/qtum-cli。举例如下（通过help命令查看所有支持的命令）。


```
$ ./bin/qtum-cli -datadir=./data/ help
== Blockchain ==
callcontract "address" "data" ( address )
getaccountinfo "address"
getbestblockhash
getblock "blockhash" ( verbosity ) 
getblockchaininfo
getblockcount
getblockhash height
getblockheader "hash" ( verbose )

...


$ ./bin/qtum-cli -datadir=./data/ help setpoaminer
setpoaminer "address"

set the miner for the poa consensus.

Arguments:
1. "address"      (string, required) The base58 address

Note: The miner's private key should be imported to the wallet.

...

```

## 配置
使用getpeerinfo命令查看当前连接的节点。目前内测期间我们设置了3台官方节点，分别是：

```
47.90.74.140:13777 [香港]
47.88.61.227:13777 [美国]
116.62.70.220:13777 [中国]
```

如果getpeerinfo返回的结果中不包含中国节点（通常为网络原因），造成区块下载速度慢，请通过以下命令手动添加。

```
./bin/qtum-cli -datadir=./data/ addnode "116.62.70.220:13777" add
```

通过getblockchaininfo命令可以获取目前同步的区块链状况。
、
```
$ ./bin/qtum-cli -datadir=./data/ getblockchaininfo
{
  "chain": "poa",
  "blocks": 63775,
  "headers": 63775,

...

```
也可以前往官方的区块链浏览器（[http://qtumx.info/](http://qtumx.info/)）查看当前的区块链状态。

## token操作
通过getnewaddress命令生成一个新的地址，然后通过邮件把地址发给官方以获得内测环境的token。
```
$ ./bin/qtum-cli -datadir=./data/ getnewaddress
QefmCRE8omt3jndykxSQTMDwLzBJGUr1BM

```

通过getreceivedbyaddress命令可以查看地址下是否有了token，或是把地址粘贴到区块链浏览器中进行获取。

得到token后就可以自由进行一些token转移操作，例如使用sendtoaddress命令可以往指定地址发送指定数量的token。

```
$ ./bin/qtum-cli -datadir=./data/ getnewaddress
QVymcpv6wDocxcQocMnWtyc9Poukt8QtyG
$ ./bin/qtum-cli -datadir=./data/ sendtoaddress QVymcpv6wDocxcQocMnWtyc9Poukt8QtyG 20
d29d09118c821340a91af779f8eb9f446ab54ee83074aa008a826bfc06fae6df
```

## 合约操作
首先通过listcontracts命令查看目前链上有哪些合约。


```
$ ./bin/qtum-cli -datadir=./data/ listcontracts
{
  "569b6c121d25a59bfb90fdec1464827aa8d57d14": 0.00000000,
  "0000000000000000000000000000000000000080": 0.00000000,
  "0000000000000000000000000000000000000085": 0.00000000,
  "9811d1e878dec479d1d8219e1cb20a3ee9f7bdd2": 0.00000000,
  "0000000000000000000000000000000000000081": 0.00000000,
  "0000000000000000000000000000000000000083": 0.00000000,
  "0000000000000000000000000000000000000084": 0.00000000,
  "0000000000000000000000000000000000000082": 0.00000000
}
```

其中，80-85为DGP合约，分别用于 gas_schedule、block_size、gas_price、预留、block_gas_limit、miner_list 参数的在线管理。

可以使用createcontract命令创建新的合约，callcontract去调用合约中的函数查看返回结果，sendtocontract去向合约发送token和数据。更多合约操作请查看：[Qtum智能合约使用方法及说明](https://docs.qtum.org/zh/Qtum-Contract-Usage.html)。

## 成为矿工
QtumX作为联盟链，矿工列表是通过DGP的方式授权指定的（参照[QtumX技术白皮书](https://docs.qtum.org/zh/Technical-White-Paper-for-QtumX/)）。可以从区块链浏览器（[http://qtumx.info/](http://qtumx.info/)）上看到，矿工会按顺序轮流生成新的区块。

目前内测环境下，DGP的权限由官方保留。所以如果你想要成为矿工，请将自己的矿工地址minerAddress通过邮件发送至官方，邮件中注明想成为矿工。然后由官方进行新矿工的投票生效过程。

注意：因为目前的PoA共识机制在半数矿工离线的情况下就会停止工作，所以一旦你成为矿工，请保证你的节点大多数情况下都会在线。

当新的矿工投票生效后，你可以通过setpoaminer命令将自己的minerAddress设置成矿工开始挖矿。

## 更新矿工

矿工列表的DGP部署在了地址"0000000000000000000000000000000000000085"上，其源码在Github上可以找到：[dgp-template.sol.js](https://github.com/qtumproject/qtum-dgp/blob/master/dgp-template.sol.js)。矿工列表的存储合约 minerList-dgp.sol 如下：


```
pragma solidity ^0.4.8;

contract minerList{

address[] _minerList=[
0x47210a1bacc15175bb24c3384e5d3650991a7bc4,
0xfe6e43ffb52ef746a0db8cc51cb95921c34ca0a3,
0x6cadd7aefdb363ae680fc234dcfe4c40919781d3
];
function getMinerList() constant returns(address[] vals){
	return _minerList;
}

}
```

更新矿工的过程可以简述如下：
1.  确定每位矿工的address，然后用gethexaddress命令得到对应的hexaddress。
2.  将所有矿工的hexaddress填入minerList-dgp.sol中的_minerList参数中，得到新的矿工列表。
3.  编译生成minerList-dgp.sol的二进制代码，并用createcontract命令部署上链。
4.  得到部署后的合约地址minerListAddress，然后调用dgp-template.sol中的addAddressProposal(minerListAddress, 2)函数，对新的minerListAddress进行投票。
5.  收到足够多的投票后，新的minerListAddress通过，记入进paramsHistory参数中，延迟若干个block（当前为500）后生效。

## 查看矿工

我们可以首先查看一下当前生效的minerListAddress。为了简便起见，合约的操作通过QT钱包进行。
1.  打开QT钱包，点击界面左侧的Smart Contracts - Call。
2.  Contract Address处填入0000000000000000000000000000000000000085，ABI处填入用dgp-template.sol编译得到的ABI，Function选择getParamsForBlock，uint _reqBlockHeight处填写一个任意高度，如10000。
6.  点击CALL CONTRACT，查看结果，得到569b6c121d25a59bfb90fdec1464827aa8d57d14。
7.  然后回到Call Contract标签页，Contract Address填写569b6c121d25a59bfb90fdec1464827aa8d57d14，ABI填写minerList-dgp.sol编译得到的ABI，Function选择getMinerList。
8.  CALL CONTRACT。得到vals为[47210a1bacc15175bb24c3384e5d3650991a7bc4, fe6e43ffb52ef746a0db8cc51cb95921c34ca0a3, 6cadd7aefdb363ae680fc234dcfe4c40919781d3]，即为高度10000上通过的矿工列表。
  
后续如果有需求，可以把矿工更新、查看相关的功能封装成接口。
