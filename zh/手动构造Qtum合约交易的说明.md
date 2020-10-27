# 手动构造Qtum合约交易的说明  

Qtum的交易结构和比特币基本一致，由`version`、`inputs`、`outputs`、`locktime`等组成，其中合约的部分是通过在`outputs`中的`scriptPubKey`中实现的。

## 1. opcode  
Qtum在比特币的基础上新增了 `OP_CREATE` 和 `OP_CALL`这两个指令,  
OP_CREATE = 0xc1，用于创建合约时使用;  
OP_CALL = 0xc2，用于调用合约时使用，即sendtocontract的时候。

## 2. OP_CALL的使用  
一笔调用合约的交易，他的`scriptPubKey`内容为：vm_version + gas_limit + gas_price + datahex + contract_address + OP_CALL  
其中 `datahex` 为编码后的合约函数+参数，我们可以通过 [ethabi](https://github.com/paritytech/ethabi) 来生成。  
比如 调用 `function foo(uint)` 就可以通过 `ethabi encode function test.json foo -p 100 -l` 得到 `datahex`。

参考工具:  
* https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI
* [eth-abi python](https://github.com/ethereum/eth-abi)
* [ethabi-js](https://github.com/jacogr/ethabi-js)

### 2.1 实例解析  
以测试网络上一笔token转账交易为例，txid：[f7eac4a0e40599d7c094353eb139aa2076be02535d66e221799d67d01054c27a](https://testnet.qtum.info/tx/f7eac4a0e40599d7c094353eb139aa2076be02535d66e221799d67d01054c27a)  

其`scriptPubKey`内容为：  
```
01040390d003012844a9059cbb00000000000000000000000081f9fc3ee3667397b58f3a53c60e7556e98cf595000000000000000000000000000000000000000000000000000009184e72a00014e21bc819674c8f7cc7d76b618914ecff082107b3c2
```
  
其中
0104 // vm_version   
0390d003 // gas_limit，16进制的03d090等于250000   
0128 // gas_price，16进制的28等于40   
44a9059cbb00000000000000000000000081f9fc3ee3667397b58f3a53c60e7556e98cf595000000000000000000000000000000000000000000000000000009184e72a000 //datahex    
14e21bc819674c8f7cc7d76b618914ecff082107b3 // contract address   
c2 // OP_CALL 


## 3. 谁是合约的调用者  
**当前仅允许 P2PKH 类型的地址调用合约**，在[QIP5](https://github.com/qtumproject/qips/issues/6) 激活之前，一笔合约交易vin里的首个UTXO对应的拥有者会被视为合约的调用者。

### 3.1 OP_SENDER  
在 [QIP5](https://github.com/qtumproject/qips/issues/6) 中，Qtum引入了一个新的opcode: `OP_SENDER`，将调用者的签名信息放在`txout.scriptpubkey`中，不再需要使用合约调用地址的UTXO。  

`scriptpubkey`的内容为：地址类型 + sender的h160地址 + 序列化的`scriptSig` + OP_SENDER + vm_version + gas_limit + gas_price + datahex + contract_address + OP_CALL  

其中`scriptSig`的内容为 签名+调用者公钥，签名对象为: nVersion + hashPrevouts + hashSequence + outpoint + scriptCode + amount + hashOutputs + nLocktime + nHashType

参考代码：
* https://github.com/qtumproject/qtum/blob/master/test/functional/qtum_op_sender.py

## 4. 手续费
手续费 = total(vin) - total(vout)，由两部分组成：
* 矿工费 = 交易size * feeRate, 其中size的计算和比特币的逻辑一致
* GAS = gasLimit * gasPrice

## 5. GAS找零
gas_price * gas_limit 就是用户调用合约支付的GAS总数，当交易得到确认之后，矿工会在coinstake交易里面加上一笔output用于返还多支付的GAS，返还的对象是合约的调用者。  
注意: **对于交易所来说，需要对GAS找零和正常的用户充值加以区分**

## 6. 参考实现代码
* js: https://github.com/qtumproject/qtumjs-lib/blob/18e05478a28337b210c6dc73fb643a25b23e25cb/src/utils.js#L132
* python: https://github.com/qtumproject/qtum-electrum/blob/9f15393f15889b0239b957528acdac42536ff66f/electrum/gui/qt/main_window.py#L3519
* java: https://github.com/qtumproject/qtumj/blob/1887a23f0f2358087bc59281efc741f2b2245e66/core/src/main/java/org/bitcoinj/wallet/SendRequest.java#L227
