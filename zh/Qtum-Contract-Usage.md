# Qtum智能合约使用方法及说明

Qtum是一个基于比特币UTXO模型，权益证明机制(pos)和支持EVM智能合约的区块链项目。它通过创新的账户抽象层(Account Abstraction Layer)实现了比特币与以太坊两大生态的融合。如果想了解更多关于Qtum的信息，可以访问我们的官网[www.qtum.org](www.qtum.org)，欢迎加入我们的社区。

## 基于Qtum的智能合约
首先需要说明的是，使用Qtum的智能合约接口仍然需要一定的技术储备。本文对智能合约的操作在命令行中使用`qtum-cli`，或者在图形钱包`qtum-qt`的debug窗口中使用。
为了演示如何简单创建和操作一个智能合约，我们将会使用如下的合约代码：

```
pragma solidity ^0.4.0;
contract QtumTest {
   uint storedNumber;
   function QtumTest() {
       storedNumber=1;
   }
   function setNumber(uint number) public{
       storedNumber = number;
   }
   function logNumber() constant public{
        log1("storedNumber", uintToBytes(storedNumber));
   }
   function returnNumber() constant public returns (uint){
       return storedNumber;
   }
   function deposit() public payable{
   }
   function withdraw() public{
       if(!msg.sender.send(this.balance)){
           throw;
       }
   }
   //utility function
   function uintToBytes(uint v) constant returns (bytes32 ret) {
       if (v == 0) {
           ret = '0';
       }
       else {
           while (v > 0) {
               ret = bytes32(uint(ret) / (2 ** 8));
               ret |= bytes32(((v % 10) + 48) * 2 ** (8 * 31));
               v /= 10;
           }
       }
       return ret;
   }
}
```
编译以上的合约代码，生成EVM的bytecode如下：

	6060604052341561000c57fe5b5b60016000819055505b5b6102bd806100266000396000f30060606040523615610076576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680633450bd6a146100785780633ccfd60b1461009e5780633fb5c1cb146100b057806394e8767d146100d05780639f2c436f1461010c578063d0e30db01461011e575bfe5b341561008057fe5b610088610128565b6040518082815260200191505060405180910390f35b34156100a657fe5b6100ae610133565b005b34156100b857fe5b6100ce6004808035906020019091905050610190565b005b34156100d857fe5b6100ee600480803590602001909190505061019b565b60405180826000191660001916815260200191505060405180910390f35b341561011457fe5b61011c610246565b005b61012661028e565b005b600060005490505b90565b3373ffffffffffffffffffffffffffffffffffffffff166108fc3073ffffffffffffffffffffffffffffffffffffffff16319081150290604051809050600060405180830381858888f19350505050151561018d57610000565b5b565b806000819055505b50565b600060008214156101ce577f3000000000000000000000000000000000000000000000000000000000000000905061023d565b5b600082111561023c5761010081600190048115156101e957fe5b0460010290507f01000000000000000000000000000000000000000000000000000000000000006030600a8481151561021e57fe5b06010260010281179050600a8281151561023457fe5b0491506101cf565b5b8090505b919050565b61025160005461019b565b6000191660405180807f73746f7265644e756d6265720000000000000000000000000000000000000000815250600c01905060405180910390a15b565b5b5600a165627a7a72305820326efcd34df5fdba07e7a1afe7ffd4b42873ef749ae9a5915db46fd20b9c251c0029


同时还会得到如下的JSON接口文件:

    [{"constant":true,"inputs":[],"name":"returnNumber","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"withdraw","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"number","type":"uint256"}],"name":"setNumber","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"v","type":"uint256"}],"name":"uintToBytes","outputs":[{"name":"ret","type":"bytes32"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"logNumber","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"deposit","outputs":[],"payable":true,"type":"function"},{"inputs":[],"payable":false,"type":"constructor"}]

任何一个合约的这些信息都可以通过[Browser Solidity](https://ethereum.github.io/browser-solidity/)这个网站获得，输入你的合约代码后，在右方点击"contract details"即可查询。

*（提示：如果使用QT钱包中的debug窗口，在以下的命令中都不需要再包含`./qtum-cli`）*

首先我们创建合约：

    ./qtum-cli createcontract 6060604052341561000c57fe5b5b60016000819055505b5b6102bd806100266000396000f30060606040523615610076576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680633450bd6a146100785780633ccfd60b1461009e5780633fb5c1cb146100b057806394e8767d146100d05780639f2c436f1461010c578063d0e30db01461011e575bfe5b341561008057fe5b610088610128565b6040518082815260200191505060405180910390f35b34156100a657fe5b6100ae610133565b005b34156100b857fe5b6100ce6004808035906020019091905050610190565b005b34156100d857fe5b6100ee600480803590602001909190505061019b565b60405180826000191660001916815260200191505060405180910390f35b341561011457fe5b61011c610246565b005b61012661028e565b005b600060005490505b90565b3373ffffffffffffffffffffffffffffffffffffffff166108fc3073ffffffffffffffffffffffffffffffffffffffff16319081150290604051809050600060405180830381858888f19350505050151561018d57610000565b5b565b806000819055505b50565b600060008214156101ce577f3000000000000000000000000000000000000000000000000000000000000000905061023d565b5b600082111561023c5761010081600190048115156101e957fe5b0460010290507f01000000000000000000000000000000000000000000000000000000000000006030600a8481151561021e57fe5b06010260010281179050600a8281151561023457fe5b0491506101cf565b5b8090505b919050565b61025160005461019b565b6000191660405180807f73746f7265644e756d6265720000000000000000000000000000000000000000815250600c01905060405180910390a15b565b5b5600a165627a7a72305820326efcd34df5fdba07e7a1afe7ffd4b42873ef749ae9a5915db46fd20b9c251c0029 300000

注意，最后的参数300000是表示这笔交易的`gas limit`，对于这个合约，默认的数值太小，所以我们将其提升到300000。

跑完以上的代码之后，我们将会得到一个如下所示的结果:

```
{
  "txid": "72b0e0576d289c1e4e6c777431e4845f77d0884d3b3cff0387a5f4a1a3a874ea",
  "sender": "qZbjaE8N18ZU1m7851G7QGhvxKL74SRBTt",
  "hash160": "aff3e34ab836edb8d214a993d9da105915e4a6e9",
  "address": "5bde092dbecb84ea1a229b4c5b25dfc9cdc674d9"
}
```

现在可以将上面结果中的`address`保存起来，方便后面使用。

	export CONTRACT=5bde092dbecb84ea1a229b4c5b25dfc9cdc674d9

现在需要等待你创建的合约被打包进一个区块，你可以通过如下的方法去确认是否被打包：

	./qtum-cli getaccountinfo $CONTRACT

如果提示说`Address does not exist`，那么不是你的交易还未被打包进新的区块（可以通过`getrawtransaction`加上你的交易id来确认是否打包），就是你未提供足够多的gas。如果合约被成功的创建并且被打包到区块链上，你将会看到类似如下的结果：

```
{
  "address": "5bde092dbecb84ea1a229b4c5b25dfc9cdc674d9",
  "balance": 0,
  "storage": {
    "290decd9548b62a8d60345a988386fc84ba6bc95484008f6362f93160ef3e563": {
      "0000000000000000000000000000000000000000000000000000000000000000": "0000000000000000000000000000000000000000000000000000000000000001"
    }
  },
  "code": "..."
}
```

为了执行合约中的函数，你必须要使用JSON的接口文件来创建ABI数据。有一个简单的工具叫做[ethabi](https://github.com/paritytech/ethabi)可以帮助你实现这个目的。确保JSON文件被保存下来了，假设名字是`interface.json`

为了得到合约中的变量`storedNumber`，我们需要调用函数`returnNumber()`，通过ethabi可以构建出ABI的数值：

	ethabi encode function ~/interface.json returnNumber

返回的结果是

	3450bd6a

因为我们的state还没有发生改变，所以调用命令`callcontract`:

	./qtum-cli callcontract $CONTRACT 3450bd6a

这个命令跑完之后的结果包含了很多有用的字段，但是当前我们只关于字段`output`，它的数值代表了`storedNumber`：

    {
      "address": "5bde092dbecb84ea1a229b4c5b25dfc9cdc674d9",
      "executionResult": {
        "gasUsed": 21664,
        "excepted": "None",
        "newAddress": "5bde092dbecb84ea1a229b4c5b25dfc9cdc674d9",
        "output": "0000000000000000000000000000000000000000000000000000000000000001",
        "codeDeposit": 0,
        "gasRefunded": 0,
        "depositSize": 0,
        "gasForDeposit": 0
      },
      "transactionReceipt": {
        "stateRoot": "ffbeb0377d43c6ed443a2840259ff5ead5158016ab54d55ef21b7b11aa71947f",
        "gasUsed": 21664,
        "bloom": "00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "log": [
        ]
      }
    }


为了改变`storeNumber`的数值，我们可以使用命令`sendtocontract`来在链上执行合约函数。首先我们还是需要ABI的数据：

    ethabi encode function ~/interface.json setNumber -p 123456 --lenient
    3fb5c1cb000000000000000000000000000000000000000000000000000000000001e240

提示，我们加上了`--lenient`这个选项后，可以不用将参数补齐至256bit。现在我们来调用合约：

    ./qtum-cli sendtocontract $CONTRACT 3fb5c1cb000000000000000000000000000000000000000000000000000000000001e240

同样，做完之后我们可以再次调用 `returnNumber()`来检查`output`字段：

    "output": "000000000000000000000000000000000000000000000000000000000001e240",

上面的结果是我们设置的数值123456的16进制形式。

此外，你还可以使用`logNumber()`函数来打印日志。如果你的节点启动的时候有带上参数`-record-log-opcodes`，那么文件 `vmExecLogs.json` 中会包含所有的操作日志。

你还可以通过`deposit()` 和 `withdraw()` 这两个函数来从测试合约中存入和提取代币。
`deposit`和`withdraw`的ABI数值分别是d0e30db0和3ccfd60b。
如下的命令将会向合约中发送10个token：

    ./qtum-cli sendtocontract $CONTRACT d0e30db0 10

同样，从合约中提取代币也非常的简单，调用如下的命令：

    ./qtum-cli sendtocontract $CONTRACT 3ccfd60b

你也可以手动指定以什么地址为`sender`调用合约，假设我的一个钱包地址是`qZbjaE8N18ZU1m7851G7QGhvxKL74SRBTt `，我可以使用如下的命令：

    ./qtum-cli sendtocontract $CONTRACT 3ccfd60b 0 190000 0.0000001 qZbjaE8N18ZU1m7851G7QGhvxKL74SRBTt

如果你的地址里没有足够的代币，会提示`Sender address does not have any unspent outputs`，这个时候你需要先向地址内转入一定的代币：

    ./qtum-cli sendtoaddress qZbjaE8N18ZU1m7851G7QGhvxKL74SRBTt 0.001

下面就可以调用`sendtocontract`了：

    ./qtum-cli sendtocontract $CONTRACT 3ccfd60b 0 190000 0.0000001 qZbjaE8N18ZU1m7851G7QGhvxKL74SRBTt

等以上的交易被打包进一个区块之后，合约中所有的代币就会被提取到指定的地址`qZbjaE8N18ZU1m7851G7QGhvxKL74SRBTt `中


## FAQ

* Q: 使用 `createcontract`创建了合约，但是无法调用合约或者合约不在合约列表中

  A：很有可能是你的gas不够，查看`vm.log`日志可以看到实际需要的gas是多少，然后再手动设置gas limit
  
* Q: 我的gas设置的很大，可是多余的却没有退还

	A: 退款将会在coinstake中生成，需要等待500个区块时间才能被使用
	
* Q: 我开启进程时使用了选项`-reindex`，然后节点就一直处于同步的状态

	A: 现在reindex的话，所有的合约都会被重新执行，所以链上的合约越多，需要等待的时间越长。未来我们会加速这个过程，同时也会缩短初始的同步时间。
	
* Q: "我觉得我发现了一个Qtum的bug"
	
	A: 欢迎报送到这里 [https://github.com/qtumproject/qtum/issues](https://github.com/qtumproject/qtum/issues)



# Qtum新增的RPC命令

Qtum支持所有比特币的RPC命令，并且还新加了如下的命令：

* `createcontract` - 在Qtum上创建和发布智能合约，会消耗gas
* `callcontract` - 这是一个与Qtum上已经部署好的合约进行交互的接口，所有的计算都是在链下进行，不需要消耗gas
* `sendtocontract` - 这也是一个与Qtum上已经部署好的合约进行交互的接口，但是所有的计算都是在链上进行的，并且所有的状态改变都会同步到链上。这个命令可以向合约发送代币，会消耗gas
* `getaccountinfo` - 这个命令可以返回一个合约的基本信息，包括bytecode，存储的数据，合约的余额等
* `listcontracts` - 这个命令会列出当前所有已部署的合约地址和余额，未来这个命令有可能被变更或者删除
* `reservebalance` - 预留一定数额的代币，不用参与staking。如果你的这个数值设置的足够大，超过你的拥有的代币数量，那么你就不会参与到staking和创造新区块的过程中。
* `getstakinginfo` - 显示当前节点的staking状态，包括当前的难度，生成下个区块的期望时间等

# Qtum新增命令行参数

Qtum支持所有的比特币命令行参数，另外Qtum新增如下的参数：

* `-record-log-opcodes` - 在Qtum的数据目录(一般是在~/.qtum)下新建一个log文件，名字是`vmExecLogs.json`，所有的EVM LOG操作都会被记录。


# EVM智能合约改动和限制

因为底层技术的差异，Qtum中执行的结果可能与以太坊略有差异。这些差异包括以下所列，未来随着开发进展还有可能有新加的变动：

* gas的设置与以太坊略有不同，某些操作的价格更贵或者更便宜。因此，基于以太坊的gas评估在qtum上并不适用。我们会开发自己的gas预估工具，并且以后也会详细列出其中的差别。

* `block.coinbase`或者`COINBASE`当前不支持了，仅仅会返回0

* `block.number` 会返回前一个区块的高度
* `block.difficulty` 前一个区块的难度
* `block.timestamp` 前一个区块的时间戳
* `block.blockhash(n)` 与以太坊类似，如果n是当前区块的高度(`block.number+1`)，返回0
* `sender` 当花费的代币(`vin[0].prevout`)是一个非标准交易时，返回0，如果是`pubkey`或者`pubkeyhash`返回160bit的`pubkeyhash`地址。
* 代币可以被发送至合约或者`pubkeyhash`地址，如果发送的时候合约地址不存在，代币将会被自动的转发至一个`pubkeyhash`地址。
* 在`coinbase`或者`coinstake`中不会执行合约操作

更多的设计和操作方法可以看[ITD](https://github.com/qtumproject/qtum-itds)文档。