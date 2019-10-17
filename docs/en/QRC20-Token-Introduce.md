# QRC20 Token

## About QRC20

QRC20 is the implementation of a standard API for tokens within smart contracts on Qtum，basically it is the same as [ERC20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md).
<br>
Methods and Events：

```
function name() constant returns (string name)
function symbol() constant returns (string symbol)
function decimals() constant returns (uint8 decimals)
function totalSupply() constant returns (uint256 totalSupply)
function balanceOf(address _owner) constant returns (uint256 balance)
function transfer(address _to, uint256 _value) returns (bool success)
function transferFrom(address _from, address _to, uint256 _value) returns (bool success)
function approve(address _spender, uint256 _value) returns (bool success)
function allowance(address _owner, address _spender) constant returns (uint256 remaining)
event Transfer(address indexed _from, address indexed _to, uint256 _value)
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```

## Implementation

One example offeres：[QRC20Token](https://github.com/qtumproject/QRC20Token), you can use this code to publish your token on Qtum.

In [QRC20Token.sol](https://github.com/qtumproject/QRC20Token/blob/master/QRC20Token.sol), change `name`、`symbol` and `totalSupply` to your own preference.

![](https://s.qtum.site/uploads/7cf98db2a2f60f944e8295ced1b76917.png)


## Deployment

### Install the wallet

Download the latest Qtum Core wallet from [https://eco.qtum.org/wallet](https://eco.qtum.org/wallet) or [https://github.com/qtumproject/qtum/releases/latest](https://github.com/qtumproject/qtum/releases/latest).

Once finish，you should withdraw some qtum coins to your wallet to pay for the gas fee.
<br>
Click `Request payment` to get your receive address.

![](https://s.qtum.site/uploads/0f30abe838aca957a1bacb2ed9209575.png)

### Compile the code

Open [https://ethereum.github.io/browser-solidity/](https://ethereum.github.io/browser-solidity/) in your browser.

Click the “+” button on the top-right side，create new files `SafeMath.sol` and `QRC20Token.sol`, copy & paste you code heer.
![](https://s.qtum.site/uploads/095deff475a970dc2a25b9e6960436db.png)
<br>
Click “detail” on the right side, copy the save BYTECODE。
![](https://s.qtum.site/uploads/47380517f0f34253511cb2c6bfc77bb7.png)
![](https://s.qtum.site/uploads/fd6f45a90362e4b27a345a4557c4c5e4.png)

### Create contract

Open Qtum Core wallet, go to “Smart Contract” =》 “Create”, paste the BYTECODE.
![](https://s.qtum.site/uploads/bb9efeaad7f8068a982ad948aa02e0e5.png)
<br>
Click “Create Contract” button, save the `SenderAddress` and `ContractAddress` for future using.
![](https://s.qtum.site/uploads/3d739f869437a96cabd9e2171199b118.png)
<br>
Wait some time until the transaction get confirmed, and the contract is created successfully.

### Test on testnet

Before publish your code on mainnet, you'd better test it on testnet.

Go to [https://github.com/qtumproject/documents/blob/master/en/Testnet-User-Guide.md](https://github.com/qtumproject/documents/blob/master/en/Testnet-User-Guide.md) to get more information about Qtum testnet.

## Wallet usage

### Add token

In Qtum Core wallet, go to “QRC Token” page and click “Add Token” button, input your `SenderAddress`, and choose `SenderAddress` as your `Token Address`, click “Confirm” button to get this done.

![](https://s.qtum.site/uploads/0b1aa0c2354522ec07cb41913f0b48d4.png)

If you cannot find the `SenderAddress` in the `Token Address` combobox, please send some qtum coins to the `SenderAddress` and try again.

### Receive and send tokens

In “QRC Token” page, click to choose your token，the you can click the “Send” and “Receive” button below to receive and send tokens。

![](https://s.qtum.site/uploads/49e40c268a4e75c9e1afe06c46f58496.png)


## More to know

* A small amount of QTUM coins is needed to pay for the token sending gas fee, please ensure you have enough QTUMs in the token binding address.




