### 我的钱包 (My wallet)

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

默认的找零地址是随机生成的新地址，可以通过偏好设置来管理找零地址。在偏好设置->钱包界面，勾选 "Don't use change address" 将使用发送地址作为找零地址，勾选"启用货币控制功能"可以在发送时指定找零地址。

![change address](change-address.png)

### 接收 (Receive)

在这里可以生成 Qtum 接收地址，并看到过往的接收地址。

![Receive](receive-1.png)

点击“请求付款”可以生成一个新的 Qtum 地址，同时也可以指定金额和备注。下图示例中填写了10个 Qtum 作为付款金额。

![Receive](receive-2.png)


### 智能合约 (Smart Contract)

智能合约分为创建、发送和调用三个部分，下面以一个 QRC20 代币合约做说明。

合约代码如下使用[https://github.com/icodeface/QRC20Token](https://github.com/icodeface/QRC20Token)的 v2 版本，使用[Remix](https://remix.ethereum.org/)对合约代码进行编译，得到的 `Bytecode` 和 `ABI` 如下：

Bytecode （请注意他很长）

```
60806040526040805190810160405280600581526020017f416c70686100000000000000000000000000000000000000000000000000000081525060009080519060200190620000519291906200020a565b506040805190810160405280600581526020017f414c504841000000000000000000000000000000000000000000000000000000815250600190805190602001906200009f9291906200020a565b506008600260006101000a81548160ff021916908360ff1602179055506000600355348015620000ce57600080fd5b506040516200101a3803806200101a8339810180604052810190808051820192919060200180518201929190602001805190602001909291908051906020019092919050505083600090805190602001906200012c9291906200020a565b508260019080519060200190620001459291906200020a565b5081600260006101000a81548160ff021916908360ff16021790555080600381905550600354600460003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055503373ffffffffffffffffffffffffffffffffffffffff1660007fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef6003546040518082815260200191505060405180910390a350505050620002b9565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106200024d57805160ff19168380011785556200027e565b828001600101855582156200027e579182015b828111156200027d57825182559160200191906001019062000260565b5b5090506200028d919062000291565b5090565b620002b691905b80821115620002b257600081600090555060010162000298565b5090565b90565b610d5180620002c96000396000f3006080604052600436106100a4576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806306fdde03146100a9578063095ea7b31461013957806318160ddd1461019e57806323b872dd146101c9578063313ce5671461024e5780635a3b7e421461027f57806370a082311461030f57806395d89b4114610366578063a9059cbb146103f6578063dd62ed3e1461045b575b600080fd5b3480156100b557600080fd5b506100be6104d2565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156100fe5780820151818401526020810190506100e3565b50505050905090810190601f16801561012b5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561014557600080fd5b50610184600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610574565b604051808215151515815260200191505060405180910390f35b3480156101aa57600080fd5b506101b3610724565b6040518082815260200191505060405180910390f35b3480156101d557600080fd5b50610234600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061072e565b604051808215151515815260200191505060405180910390f35b34801561025a57600080fd5b50610263610a0e565b604051808260ff1660ff16815260200191505060405180910390f35b34801561028b57600080fd5b50610294610a25565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156102d45780820151818401526020810190506102b9565b50505050905090810190601f1680156103015780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561031b57600080fd5b50610350600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610a5e565b6040518082815260200191505060405180910390f35b34801561037257600080fd5b5061037b610a76565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156103bb5780820151818401526020810190506103a0565b50505050905090810190601f1680156103e85780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561040257600080fd5b50610441600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610b18565b604051808215151515815260200191505060405180910390f35b34801561046757600080fd5b506104bc600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610cc9565b6040518082815260200191505060405180910390f35b606060008054600181600116156101000203166002900480601f01602080910402602001604051908101604052809291908181526020018280546001816001161561010002031660029004801561056a5780601f1061053f5761010080835404028352916020019161056a565b820191906000526020600020905b81548152906001019060200180831161054d57829003601f168201915b5050505050905090565b60008260008173ffffffffffffffffffffffffffffffffffffffff161415151561059d57600080fd5b600083148061062857506000600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054145b151561063357600080fd5b82600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508373ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff167f8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925856040518082815260200191505060405180910390a3600191505092915050565b6000600354905090565b60008360008173ffffffffffffffffffffffffffffffffffffffff161415151561075757600080fd5b8360008173ffffffffffffffffffffffffffffffffffffffff161415151561077e57600080fd5b610804600560008873ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205485610cee565b600560008873ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055506108cd600460008873ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205485610cee565b600460008873ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550610959600460008773ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205485610d07565b600460008773ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508473ffffffffffffffffffffffffffffffffffffffff168673ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef866040518082815260200191505060405180910390a36001925050509392505050565b6000600260009054906101000a900460ff16905090565b6040805190810160405280600981526020017f546f6b656e20302e31000000000000000000000000000000000000000000000081525081565b60046020528060005260406000206000915090505481565b606060018054600181600116156101000203166002900480601f016020809104026020016040519081016040528092919081815260200182805460018160011615610100020316600290048015610b0e5780601f10610ae357610100808354040283529160200191610b0e565b820191906000526020600020905b815481529060010190602001808311610af157829003601f168201915b5050505050905090565b60008260008173ffffffffffffffffffffffffffffffffffffffff1614151515610b4157600080fd5b610b8a600460003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205484610cee565b600460003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550610c16600460008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205484610d07565b600460008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508373ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef856040518082815260200191505060405180910390a3600191505092915050565b6005602052816000526040600020602052806000526040600020600091509150505481565b6000818310151515610cfc57fe5b818303905092915050565b6000808284019050838110151515610d1b57fe5b80915050929150505600a165627a7a723058200a1e9096aed2390ca8c214d802cecae0479f8f12c10148784f2bd5f226f8775d0029
```

ABI

```json
[
	{
		"constant": true,
		"inputs": [],
		"name": "name",
		"outputs": [
			{
				"name": "_name",
				"type": "string"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "_spender",
				"type": "address"
			},
			{
				"name": "_value",
				"type": "uint256"
			}
		],
		"name": "approve",
		"outputs": [
			{
				"name": "success",
				"type": "bool"
			}
		],
		"payable": false,
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [],
		"name": "totalSupply",
		"outputs": [
			{
				"name": "_totalSupply",
				"type": "uint256"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "_from",
				"type": "address"
			},
			{
				"name": "_to",
				"type": "address"
			},
			{
				"name": "_value",
				"type": "uint256"
			}
		],
		"name": "transferFrom",
		"outputs": [
			{
				"name": "success",
				"type": "bool"
			}
		],
		"payable": false,
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [],
		"name": "decimals",
		"outputs": [
			{
				"name": "_decimals",
				"type": "uint8"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [],
		"name": "standard",
		"outputs": [
			{
				"name": "",
				"type": "string"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [
			{
				"name": "",
				"type": "address"
			}
		],
		"name": "balanceOf",
		"outputs": [
			{
				"name": "",
				"type": "uint256"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [],
		"name": "symbol",
		"outputs": [
			{
				"name": "_symbol",
				"type": "string"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "_to",
				"type": "address"
			},
			{
				"name": "_value",
				"type": "uint256"
			}
		],
		"name": "transfer",
		"outputs": [
			{
				"name": "success",
				"type": "bool"
			}
		],
		"payable": false,
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [
			{
				"name": "",
				"type": "address"
			},
			{
				"name": "",
				"type": "address"
			}
		],
		"name": "allowance",
		"outputs": [
			{
				"name": "",
				"type": "uint256"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"name": "_name",
				"type": "string"
			},
			{
				"name": "_symbol",
				"type": "string"
			},
			{
				"name": "_decimals",
				"type": "uint8"
			},
			{
				"name": "_totalSupply",
				"type": "uint256"
			}
		],
		"payable": false,
		"stateMutability": "nonpayable",
		"type": "constructor"
	},
	{
		"payable": true,
		"stateMutability": "payable",
		"type": "fallback"
	},
	{
		"anonymous": false,
		"inputs": [
			{
				"indexed": true,
				"name": "_from",
				"type": "address"
			},
			{
				"indexed": true,
				"name": "_to",
				"type": "address"
			},
			{
				"indexed": false,
				"name": "_value",
				"type": "uint256"
			}
		],
		"name": "Transfer",
		"type": "event"
	},
	{
		"anonymous": false,
		"inputs": [
			{
				"indexed": true,
				"name": "_owner",
				"type": "address"
			},
			{
				"indexed": true,
				"name": "_spender",
				"type": "address"
			},
			{
				"indexed": false,
				"name": "_value",
				"type": "uint256"
			}
		],
		"name": "Approval",
		"type": "event"
	}
]
```

#### 创建合约 (Create)

将上面的 `Bytecode` 和 `ABI` 填入表里，钱包会自动识别出参数列表，填写好之后点击创建智能合约，若执行成功，则可以看到结果。

![create](contract-create.png)
![create](contract-create-2.png)

如上图得到你的合约地址是 `91191f443b6aa395ba24ab72430f00297e5d2121`。

#### 向合约发送数据 (Send To)

向合约发送数据需要填写合约地址和 ABI ，合约地址在上一个步骤得到， ABI 与之前的一致。填写好之后钱包会识别出来可以调用的方法，这里以 `transfer` 为例。注意 `Send To` 操作会消耗你的 Qtum。

![create](contract-sendto.png)
![create](contract-sendto-2.png)

*注意*，这里的地址填写的是16进制格式地址，可以通过控制台的 `gethexaddress` 命令获取。

![create](contract-sendto-3.png)

#### 本地调用 (Call)

和发送一样，填写好合约地址和 ABI ，钱包会识别出来可以本地调用的方法，本地调用无需消耗 Qtum。

![create](contract-call.png)
![create](contract-call-2.png)


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

最新版本的 Qtum 钱包已经在界面上实现了备份管理。你可以轻松的备份、恢复你的钱包。点击 "File ->  Restore Wallet" ，在弹出的对话框可以看到有 4 种方式来恢复钱包，每种方式均可以选择一个备份文件来恢复钱包，若不选择将会使用现有的钱包目录下的 wallet.dat 文件。

![restore](restore-1.png)

1. 从备份文件恢复（ Restore file ）。此方式适用于恢复其他地方备份的钱包文件，通常为 .dat 文件。
2. 重新扫描 —— 重新扫描区块，以查找遗漏的交易。此方式用于修复遗漏交易、余额低于实际值等问题
3. zapwallettxes=2 —— 回复没有元数据的交易。此方式用于修复同时出现遗漏交易、余额低于实际值、孤块以及分叉链的问题。建议执行此命令后再次备份钱包。
4. 删除区块链数据 —— 删除区块链本地副本，重新同步整个区块链的数据。此方式用于修复区块链同步、区块链受损及分叉链等问题。
​

在右侧选择要恢复的文件，然后点击 OK ，在弹出的框中点击 YES ，Qtum 钱包会自动启动，并使用你刚刚选择的备份文件恢复。

![restore](restore-2.png)

### 挖矿

当你满足如下条件时就可以进行挖矿：

1. 钱包中有超过500个确认的 Qtum ；
2. 解锁钱包；
3. 保持钱包在线状态。

更多细节可以参考：[http://docs.qtum.site/zh/How-to-Stake-with-Qtum/](http://docs.qtum.site/zh/How-to-Stake-with-Qtum/)

***

# Offline Staking

* [将地址委托给Super Staker](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#将地址委托给super-staker)
* [委托地址操作](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#委托地址操作)
* [配置Super Staker](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#配置super-staker)
* [以Super Staker身份登录Qtum Core](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#以super-staker身份登录qtum-core)
* [qtumd Super Staker](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#qtumd-super-staker)
* [Super Staker操作](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#super-staker操作)
* [恢复](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#恢复)

# 将地址委托给Super Staker

Qtum Offline Staking允许未staking的钱包地址（可以进行委托任务转账）被委托给Super Staker。Offline Staking无需托管，委托用户对自己的资产和私钥有完全的控制权。地址委托通过一次来自委托用户钱包的智能合约转账实现，在这个过程中委托者的地址、Super Staker的地址和委托者同意支付的费用都在转账中有所体现。如果Super Staker接受该费率，它将会开始为委托地址的UTXO进行staking。

委托的UTXO遵循与普通stakingUTXO同样的规则：

* UTXO只有在成熟（达到500个区块的确认）之后才能被用于staking。
* Super Staker将会设置一个stake的最小UTXO限制，默认为100 QTUM。低于该值的委托UTXO将被忽略。
* 从回报角度来看，委托UTXO的最佳值在100-200 QTUM之间。对于Qtum Core钱包的用户来说，可以通过`splitutxosforaddress`命令实现UTXO的拆分。细节请见下文。

如果想从Qtum Core钱包进行委托操作，您可以在"Stake"中选择"委托"，然后点击右上角的"+"按钮添加委托。之后，输入Staker名（为了方便辨识）、Staker地址、想要支付的费用比例和您想要委托的地址。如果您对Gas费用没有特别要求，请使用默认设置。委托转账需要至少0.9QTUM作为费用，多余的费用将被退还。

![1  Add Delegation Assignment - CN](https://user-images.githubusercontent.com/29760787/85623682-ca7e8580-b636-11ea-8b92-2fd1fe735897.jpg)

点击"确认"和"是"发送委托转账。

委托也可以通过Qtum Electrum钱包完成，同时支持Ledger硬件钱包地址。

# 委托地址操作

委托地址转账会被发送到一个智能合约中，该合约将记录委托任务，Super Staker也将从合约处领取任务。您将可以在钱包或浏览器[qtum.info](https://qtum.info/)中查看委托地址的区块奖励转账。

如果一个钱包的QTUM存在多个地址中，每个地址必须单独委托（转账费也必须单独支付）。因此，把UTXO合并到一个地址中再拆分委托可能更符合委托者的利益。在这种情况下，可以手动将不同地址的币合并到一个地址中。另一种方式是使用`sendmanywithdupes`命令，该命令可以将钱包内所有余额以合适的UTXO值发送到一个新地址内。

如果Super Staker接受了某一费率的一项委托，之后该Super Staker又降低了自己的费率标准（接受更低费率的委托任务），委托者如果也想享受该更低的费率，就必须重新设定费率，重新进行委托。

某个钱包的委托可以在"Stake"页的"委托"选项中查看，或者使用`getdelegationinfoforaddress`命令。

请保存一份wallet.dat文件以备份钱包。

# 配置Super Staker

Qtum Core钱包提供了在线的PoS共识，因此登录、配置该钱包之后就可以作为Super Staker进行操作、接受其他地址的委托。

如果想在Qtum-Qt钱包中配置成为Super Staker，请在"Stake"页面选择"Super Staker"，然后选择"+"以添加一个新的Super Staker。输入Staker名（仅作为本地识别使用，此处示例中使用地址的第一部分，并用"10"表示10%的费用），之后从下拉菜单中选择Staker地址。

![2  Super Staker Setup CN](https://user-images.githubusercontent.com/29760787/85623694-ce120c80-b636-11ea-9aa2-8587900c6abf.jpg)

作为Super Staker，钱包必须能够检查任意地址（地址索引）、启用日志以便操作智能合约（日志事件）并开启Staking选项。这三项设置可以通过设置`-superstaking=true`参数实现。设置`-superstaking=true`之后首次登录钱包时，钱包将重新扫描区块链以构建包含地址索引和日志事件的数据库。

下一步，钱包将提示您在"设置"-"选项"-"开启Super Staking"，确认之后钱包将重新启动。

![3  Qtum-Qt Enable Super Staker CN](https://user-images.githubusercontent.com/29760787/85623709-d407ed80-b636-11ea-8d6a-a1ea83dde656.jpg)
 
重启之后，钱包将向您确认是否要扫描区块链以便重建数据库。

![4  Rebuild the Database CN](https://user-images.githubusercontent.com/29760787/85623718-d5d1b100-b636-11ea-988f-762fb36bf926.jpg)

钱包将显示"正在硬盘上重新索引区块"以及在重建数据库时显示"同步区块头"。这可能需要几十分钟，具体时间取决于您的计算机配置。

登录之后，返回"Stake"-"Super Staker"页面，选择"设置Super Staker"按钮（现在将能显示齿轮标志）以完成Super Staker配置。点击定制按钮查看默认配置，或更改配置。点击确认完成设置。

![5  Super Staker Options CN](https://user-images.githubusercontent.com/29760787/85623722-d8340b00-b636-11ea-8829-d6c5ad2fbbbe.jpg)

配置选项包括：

* 最低费用 - Staker将会接受的最低委托费率。
* 最小UTXO值 - 设定了该Staker将接受的用于PoS共识的最小的UTXO。随着时间推进，委托地址将有许多小额区块奖励UTXO，管理这些小额UTXO将很低效（委托者应该将这些UTXO合并）。
* 委托列表类型：
  *	接受所有 - 接受所有高于最低费率的委托。
  *	允许列表 - 只接受来自特定地址的委托。使用该模式将使Super Staker只能为特定地址服务，比如只为自己的币进行Staking。
  *	排除列表 - 不接受来自列表内的地址的委托。

接下来，Super Staker将把UTXO分解成有效大小进行Staking。进行Staking的UTXO最小值为100QTUM。在Super Staker页面可以选择拆分按钮（三叉戟图标），拆分可以使用默认值或自行调整，但能用于Staking的UTXO最小值为100QTUM。

![6  Split UTXOs GUI CN](https://user-images.githubusercontent.com/29760787/85623727-d9fdce80-b636-11ea-8502-ff453d6140ce.jpg)

你也可用使用`splitutxosforaddress`命令拆分UTXO。委托地址也可用使用该功能。如果想将UTXO拆分为最小值（minValue）和最大值（maxValue）之间的值，可用使用如下命令：

`splitutxosforaddress "address" minValue maxValue ( maxOutputs )`

例如，如果一个钱包内有数量为40、50、60、70和800QTUM的几个UTXO，要把这些UTXO拆分为最小100最大200的UTXO，可用使用如下命令：

```splitutxosforaddress "qQhm128r4cTuDFSRehLESydnkburYLj9cY" 100 200

{
  "txid": "197a199c3ac9dd8df574ca77da15c5da31db3f7101e2108638a3b2f94248b9f7",
  "selected": "1020.00",
  "splited": "1020.00"
}
```

以上例子中，输入总额为1020QTUM，拆分结果为9个100QTUM和1个119.99566QTUM的UTXO。钱包将发送一次对自己转账，并支付0.00434QTUM的转账费。

在前面的例子中还展示了使用`sendmanywithdupes`命令的方式，但这种方式需要注意格式，并且更适用于您想将资金发送到新地址的情况。而且，无论使用哪个命令，这些UTXO都必须等待500个区块时间的确认，成熟后才能用于Staking。

# 以Super Staker身份登录Qtum Core

以上步骤展示了从默认的Qtum Core普通用户转换为Super Staker的流程。Qtum Core钱包也可以直接以Super Staker身份登录以缩短配置流程。这种情况下，起始的区块链同步就已经包括了为地址索引和日志事件构建数据库的过程，所以钱包就可以直接支持Super Staker使用。

Qtum Core钱包可以通过"设置"-"选项"-"允许Super Staking"设置来开启Super Staker模式，或者直接在命令行中使用`-superstaking=true`参数（示例为测试网环境）。

![7  Linux Launch CN](https://user-images.githubusercontent.com/29760787/85623735-dc602880-b636-11ea-8dc6-c8d6d250f755.png)

该命令在Windows的默认程序目录中使用方式如下：

`qtum-qt -testnet -superstaking=true`

![8  Windows Command Line Launch CN](https://user-images.githubusercontent.com/29760787/85623743-dec28280-b636-11ea-9b69-5e30797db423.jpg)

当钱包登录并同步区块链时（创建地址索引和日志事件），钱包就可以添加Super Staker。配置一个Super Staker，然后选中"设置"-"选项"-"允许Super Staking"即可开启Super Staker。

# qtumd Super Staker

在Qtum Core钱包中以Super Staker身份运行的任何地址都可能受到委托地址的委托，并以独立的Super Staker进行操作。桌面图形界面版的Qtum-Qt钱包允许配置多个Super Staker地址，分别设置不同的费率和最小UTXO值。deamon/server钱包qtumd中，所有Super Staker地址只能使用同一费率和最小UTXO设置。如果在qtumd中多个Super Staker需要不同的设置，可以在Qtum-Qt钱包中设置好后将wallet.dat文件转移到qtumd中运行。

下面的流程展示了在qtumd中配置一个Super Staker地址的过程。

安装qtumd后，以以下参数登录（示例为测试网环境）：

`./qtumd -testnet -superstaking=true`

可以添加一些非必须参数以修改费率（10%）和最小UTXO值（100QTUM），例如：

`-stakingminfee=12  -stakingminutxovalue=120`

一旦钱包完成同步，就可以取得一个地址，并向该地址发送一些QTUM。这个地址就将是演示用的Super Staker地址。使用如下命令：

`./qtum-cli -testnet getnewaddress "legacy"`

然后向该地址发送1300QTUM。

![9  Getnewaddress Getbalance CN](https://user-images.githubusercontent.com/29760787/85623752-e124dc80-b636-11ea-9337-3239630551f3.png)

这1300QTUM以一个UTXO的形式发送，想要用于Super Staker操作就必须进行拆分。可以使用`splitutxosforaddress`命令拆分为最小100QTUM、最大200QTUM。

`./qtum-cli -testnet splitutxosforaddress "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d" 100 200`

![10  Split UTXOs for Address qtumd CN](https://user-images.githubusercontent.com/29760787/85623757-e3873680-b636-11ea-907d-36a19e01d11c.png)

命令的执行结果显示1300QTUM被拆分成12个UTXO，可以根据转账的txid在区块链浏览器中查看具体操作。

此时，qtumd钱包已经可以使用地址qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d进行Super Staker操作。可以使用以下命令查看委托情况：

`getdelegationsforstaker "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d"`

# Super Staker操作

Super Staker必须有一定量的UTXO为正在Staking的委托UTXO进行Stake以领取区块奖励。所需UTXO的数量（每个UTXO最少100QTUM）视委托权重占全网权重的百分比而定。比较安全的UTXO数量如下：30UTXO（1%全网权重）、50UTXO（2%全网权重）、100UTXO（5%全网权重）、160UTXO（10%全网权重）。

Super Staker应该时刻关注自己的钱包权重（UTXO权重减去正在Staking的数量），并在下降显著时及时补充UTXO。

请在更改offline staking设置（比如增加Super Staker或增加委托）后及时备份钱包（保存一份wallet.dat）文件，因为offline staking设置保存在wallet.dat文件内。如果wallet.dat文件丢失，也可以通过恢复选项找回设置。

向Super Staker发出的委托可以通过Super Staker页面的"委托"按钮进行查看，或者使用`getdelegationsforstaker`命令。

# 恢复

通常委托和Super Staker设置保存在wallet.dat文件内。如果wallet.dat文件遇到问题，可以通过Super Staker与委托页面的"恢复"按钮恢复委托信息和Super Staker信息。这种情况下，钱包将重新扫描智能合约状态，找到相应地址的offline staking转账相关信息。

![11  Restore super stakers CN](https://user-images.githubusercontent.com/29760787/85623770-e6822700-b636-11ea-8042-0ba6b480ccf0.jpg)

 
***


