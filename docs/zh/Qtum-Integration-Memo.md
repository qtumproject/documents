# 列举在对接过程中，Qtum 与 比特币 的常见不同点

## 关键参数
* 创世块哈希:  `hashGenesisBlock`
* base58地址前缀: `base58Prefixes[PUBKEY_ADDRESS]` 与 `base58Prefixes[SCRIPT_ADDRESS]`
* WIF私钥前缀: `base58Prefixes[SECRET_KEY]`
* EXT公钥、私钥的前缀: `base58Prefixes[EXT_PUBLIC_KEY]` 与 `base58Prefixes[EXT_SECRET_KEY]`
* bech32地址前缀: `bech32_hrp`
* P2P端口号: `nDefaultPort`
* P2P通讯的数据包头：`pchMessageStart`

以上信息可以在 [qtum/src/chainparams.cpp](https://github.com/qtumproject/qtum/blob/master/src/chainparams.cpp) 中找到

## 区块头结构
见 [qtum/src/primitives/block.h](https://github.com/qtumproject/qtum/blob/master/src/primitives/block.h)

注意 **vchBlockSig** 是不定长的，在解析区块头时需要先读取一个Varint类型的长度值，然后根据长度取签名。所以区块头的长度也是不定长的。

## 最低手续费率 和 Dust Threshold
DEFAULT_MIN_RELAY_TX_FEE = 400000;  即 0.00400000 QTUM/kb
见 [qtum/src/validation.h](https://github.com/qtumproject/qtum/blob/master/src/validation.h)

DUST_RELAY_TX_FEE = 400000;
见 [qtum/src/policy/policy.h](https://github.com/qtumproject/qtum/blob/master/src/policy/policy.h)

Dust Threshold 值为 72800 Satoshi

## [成熟期](https://bitcoin.stackexchange.com/questions/1991/what-is-the-block-maturation-time)
COINBASE_MATURITY = 500;
见 [qtum/src/consensus/consensus.h](https://github.com/qtumproject/qtum/blob/master/src/consensus/consensus.h)
通常在修改测试用例的时候需要注意这个，以免钱包余额不足。

## [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) 的 Coin Type
由于一些[历史原因](https://github.com/satoshilabs/slips/pull/196)，现行的Qtum有两套Coin Type值，
其中 Qtum官方钱包、以及Ledger 使用 **88** 作为 Coin Type，
而 Trezor、KeepKey 使用在 [satoshilabs/slips/slip-0044.md](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) 中定义的 **2301** 作为 Coin Type。

## 消息签名
strMessageMagic = "Qtum Signed Message:\n";
见 [qtum/src/validation.h](https://github.com/qtumproject/qtum/blob/master/src/validation.h)

注意，有些项目会在这段字符串签名加上一个16进制数表示长度。如 b"\x15Qtum Signed Message:\n"
