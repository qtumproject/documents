# 手动构造Qtum合约交易的说明

Qtum的交易结构和比特币基本一致，由version、inputs、outputs、locktime等组成，其中合约的部分是通过在outputs中的scriptPubKey中实现的。

## opcode
Qtum在比特币的基础上新增了OP_CREATE和OP_CALL这两个指令,  

OP_CREATE = 0xc1，用于创建合约时使用;  

OP_CALL = 0xc2，用于调用合约时使用，即sendtocontract的时候。

## OP_CALL的使用
一笔调用合约的交易，他的scriptPubKey内容为：　vm_version + gas_limit + gas_price + datahex + contract_address + OP_CALL
    
其中datahex为编码后的合约函数+参数，我们可以同过 [ethabi](https://github.com/paritytech/ethabi) 来生成
  
比如 调用function foo(uint) 就可以通过 `ethabi encode function test.json foo -p 100 -l` 得到datahex。

* https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI
* [eth-abi python](https://github.com/ethereum/eth-abi)
* [ethabi-js](https://github.com/jacogr/ethabi-js)

## 实例解析
以测试网络上一笔token转账交易为例，txid：[f7eac4a0e40599d7c094353eb139aa2076be02535d66e221799d67d01054c27a](https://testnet.qtum.org/tx/f7eac4a0e40599d7c094353eb139aa2076be02535d66e221799d67d01054c27a)  

他的scriptPubKey内容为：01040390d003012844a9059cbb00000000000000000000000081f9fc3ee3667397b58f3a53c60e7556e98cf595000000000000000000000000000000000000000000000000000009184e72a00014e21bc819674c8f7cc7d76b618914ecff082107b3c2
  
其中
0104 // vm_version 

0390d003 // gas_limit，16进制的03d090等于250000 

0128 // gas_price，16进制的28等于40 

44a9059cbb00000000000000000000000081f9fc3ee3667397b58f3a53c60e7556e98cf595000000000000000000000000000000000000000000000000000009184e72a000 //datahex  

14e21bc819674c8f7cc7d76b618914ecff082107b3 // contract address 

c2 // OP_CALL


## 谁是合约的调用者
一笔合约交易vin里的首个UTXO对应的拥有者会被视为合约的调用者。

## GAS找零
gas_price * gas_limit 就是用户调用合约支付的GAS总数，当交易得到确认之后，矿工会在coinstake交易里面加上一笔output用于返还多支付的GAS，返还的对象是合约的调用者。

**对于交易所来说，需要对GAS找零和正常的用户充值加以区分**

## 参考实现代码
* https://github.com/qtumproject/qtumjs-lib/blob/master/src/utils.js#L132
* https://github.com/qtumproject/qtum-electrum/blob/master/gui/qt/main_window.py#L3212
* https://github.com/wangh09/bitcoincashj/blob/master/core/src/main/java/org/bitcoincashj/wallet/Wallet.java#L3821


