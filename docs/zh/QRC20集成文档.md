# QRC20集成技术文档

---

> 本文档说明了怎么使用`qtumd`提供的命令完成基础的QRC20操作

## 一、基础说明
交易所使用一个主地址来存储所有用户的token，以下用`MAIN_QRC_ADDRESS`来指代。
QRC20代币的合约地址以下使用`TOKEN_CONTRACT_ADDRESS`来指代。
gas limit使用`DEFAULT_GAS_LIMIT`指代，推荐为`250000`。
gas price使用`DEFAULT_GAS_PRICE`指代，推荐为`0.00000040`。
`TOKEN_DECIMALS`定义了token的小数点位置，值为`8`。
还需要定义如下操作:
`addressToHash160`把编码后的地址转义为hash160地址，这是基础概念，不过多解释。
`to32bytesArg`把十六进制字符串的参数进行编码，编码后的结果为向参数前补字符0，扩展到64个字符的字符串。
`addDecimals`把金额转为十六进制字符串, 具体操作可以参考如下php代码:
```php
function addDecimals($amount){
    $decimalPos=getNumberOfDecimals($amount);
    $amount= gmp_init(str_replace(".","",$amount));
    return gmp_strval(gmp_mul($amount,gmp_pow(10,(TOKEN_DECIMALS-$decimalPos))),16);
}

function getNumberOfDecimals($amount){
    if (($pos = strpos($amount, ".")) !== FALSE) {
        return strlen(substr($amount, $pos+1));
    }else{
        return 0;
    }
}
```

请使用`-logevents -txindex`参数运行`qtumd`。
命令行中出现`{}`的地方请带入前面定义的值进行替换。
注意命令行中的空格。

## 二、获取账户金额
账户地址为`$userAddress`。
```
qtum-cli callcontract {TOKEN_CONTRACT_ADDRESS} 70a08231{to32bytesArg(addressToHash160($userAddress))}
```
输出结果为json，里面的`executionResult.output`即为账户余额。

## 三、提现
提现地址为`$userAddress`, 提现金额为`$amount`（单位为1token）。
```
qtum-cli sendtocontract {TOKEN_CONTRACT_ADDRESS} a9059cbb{to32bytesArg(addressToHash160($userAddress))}{to32bytesArg(addDecimals($amount)) 0 {DEFAULT_GAS_LIMIT} {DEFAULT_GAS_PRICE} {MAIN_QRC_ADDRESS}
```
命令执行结果的txid即本次交易id，可以用来查询。

## 四、获取新充值地址
`QTUM`的充值地址和QRC20代币的充值地址都是同样的格式，对于交易所来说，同一个用户下面的`QTUM`充值地址和QRC20代币的充值地址可以是同一个。
也可以使用如下命令获取新的充值地址：
```
qtum-cli getnewaddress
```

## 五、获取充值\提现记录
要查询的地址为`$depositAddress`。开始查询的区块高度为`$startingBlock`(含此区块，可以为0，为了提高效率建议从用户触发操作后区块开始查)
```
qtum-cli searchlogs {$startingBlock} 999999999 '{"addresses": ["{TOKEN_CONTRACT_ADDRESS}"]}' '{"topics": ["ddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef"]}'
```
注意：参数里面有json，最外层的`{}`不需要去替换。

查询结果是一个json数组，通过解析`log`字段可以得到所需要的记录。

## 六、查询交易确认数
交易id为`$txid`。
```
qtum-cli gettransaction {$txid}
```
命令结果的`confirmations`字段即为确认数。
