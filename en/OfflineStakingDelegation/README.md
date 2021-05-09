# Offline Staking Address Delegation - Undelegation Transaction Details

### Intended audience

The intended audience for this document are developers who need to build raw transactions or blocks that interact with the offline staking functionality of Qtum.  This document assumes the reader is familiar with basic Ethereum and Bitcoin concepts. In order to understand the delegated PoS block related concepts in this document, the reader should have an understanding of the staking in Qtum's "non-delegated" PoS.

### Introduction

Offline staking allows a holder of QTUM to delegate their staking weight to a third party Super Staker. They do this by sending a smart contract transaction to address 0x0000000000000000000000000000000000000086. This transaction includes the address which they want to allow being staked by a third party Super Staker (the "*delegation*"), the Super Staker address that they want to allow to stake on their behalf (the "*staker*") and a *fee* percentage that the *staker* will receive. For Qtum offline staking all addresses must be legacy addresses starting with a "Q" for Qtum mainnet or "q" for Qtum testnet.

Once such a transaction has been confirmed, the *staker* is able to stake on behalf of the *delegator* by constructing a special type of delegated PoS block.

### Glossary

##### Proof of Delegation (PoD)

The proof of delegation ("PoD") is a compact 65 byte signature made by the *delegation{privkey}* with the *staker{hexpubkeyhash}* as message. This is done in order to prove that the delegator has at some point allowed the *staker* to stake blocks on behalf of the *delegator*. More specifically, the message that is signed is: 

*sha256d(staker{hexpubkeyhash})*

i.e., equivalent to a message signed using the *signmessage* RPC call in Qtum.  Note that the *staker{pubkeyhash}* should be hex-encoded and is therefore 40 bytes.

The message signed is shown in the script below as `sha256d("\x15Qtum signed message:\n\x28"+staker{hexpubkeyhash})` where `\x15` hexadecimal represents 21 decimal ASCII characters "Qtum signed message:" plus the newline character 0x0A. These characters are concatinated with `\28` hexadecimal or 40 decimal characters of the staker hexpubkeyhash.

##### Offline staking contract address

The offline staking contract is located at address 0x0000000000000000000000000000000000000086.

##### OP_CALL script

An OP_CALL (i.e., a contract execution) script requires the following scriptpubkey structure: "\<VERSION\> \<GASLIMIT\> \<GASPRICE\> \<CALLDATA\> \<CONTRACTADDRESS\> OP_CALL". For the purposes of this document VERSION will always equal 4. GASLIMIT should be *2250000* for an *addDelegation* call and may be set to *100000* for a *removeDelegation* call. GAS_PRICE will typically be 40. The CONTRACTADDRESS will always equal 0x0000000000000000000000000000000000000086 in this document. The only variable value in an OP_CALL script will be the CALLDATA in this document. CALLDATA is equivalent to the same concept in Ethereum and should be ABI-encoded in the same way as in Ethereum.

##### Transaction sender

The sender of a transaction is the pubkeyhash responsible for executing a contract transaction ("msg.sender" in solidity). The sender in Qtum is defined as either the address of the first input to a transaction or the address which is defined by an OP_SENDER subscript (beyond the scope of this document). For the purposes of this document we will always assume that the sender is defined by the address of the first input to a transaction. That output being spent must have either a P2PK or P2PKH script.

### Delegating an address to a staker ("addDelegation")

To delegate the staking authority of a particular address the process is as follows:

The delegator selects their address they want to delegate to a staker, the "*delegation*".

The delegator selects a staker to that will be allowed to submit blocks by staking using the *delegation*'s utxos: the "*staker*".

The delegator creates a PoD by signing the *staker{hexpubkeyhash}* using the *delegation{privkey}*.


The delegator creates a transaction that has one OP_CALL txout that executes the *addDelegation* function of the offline staking contract. The transaction sender must be the *delegation* address. The sender (e.g., the first vin prevout's address of the transaction) must be from the *delegation* address. The output that calls the *addDelegation* function should contain the following contract calldata:   

*4c0e968c + staker{pubkeyhash} + fee + 0x60 + 0x41 + PoD* 

The contract calldata follows the normal rules for Ethereum's  ABI encoding, e.g., all values in the calldata should be left padded by zero bytes to the nearest 32 byte multiple except for the function ABI param (4c0e968c). The fee should be an integer value between 0 and 100, determining the fee percentage which is assigned to the *staker* upon a successful block being found. *0x60* is the position of the PoD byte array (for more details see the Ethereum ABI specification). *0x41* is the length of the PoD bytes (65 bytes). The PoD bytes is the signature produced by signing *staker{pubkeyhash}* using the *delegation{privkey}* (see "Proof of Delegation" for more details). 

For example, a *delegation{pubkeyhash} = 0x4008700e91bba17d858722d7112adf436ca416ed* to the *staker{pubkeyhash} = 0x7da6be640325a6048cd67f070c314fa405df126b* with a *fee* of 99%, the calldata could be the following:

```
4c0e968c 

0000000000000000000000007da6be640325a6048cd67f070c314fa405df126b

0000000000000000000000000000000000000000000000000000000000000063

0000000000000000000000000000000000000000000000000000000000000060

0000000000000000000000000000000000000000000000000000000000000041

1f0db6005c1788cf46383ba6750de747edad798648bb9f69086e7e661a1ccaa408717f7b005c0e0fc3817cd7cf6cc3561cad2c5c221951f1fb26fa71e4eabd48fa00000000000000000000000000000000000000000000000000000000000000
```

The full output's scriptPubKey would therefore be:

```
4 2250000 40 4c0e968c0000000000000000000000007da6be640325a6048cd67f070c314fa405df126b0000000000000000000000000000000000000000000000000000000000000063000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000411f0db6005c1788cf46383ba6750de747edad798648bb9f69086e7e661a1ccaa408717f7b005c0e0fc3817cd7cf6cc3561cad2c5c221951f1fb26fa71e4eabd48fa00000000000000000000000000000000000000000000000000000000000000 0000000000000000000000000000000000000086 OP_CALL
```

See appendix for a full example transaction.

### Removing a delegation ("removeDelegation")

To remove an active delegation, the *delegator* makes a contract call to *removeDelegation* ("bffe3486") with *delegation* as sender. The calldata would therefore simply be:

3d666e8b

The full output's scriptPubKey would therefore be:

4 100000 40 3d666e8b 0000000000000000000000000000000000000086 OP_CALL

See appendix for a full example transaction.

### Staking a delegated block by the Staker

After the transaction that calls *addDelegation* has been confirmed, the *staker* is able to stake blocks on behalf of *delegation*. To find new blocks, the *staker* iterates over all *delegation* utxos with an **unused** *depth > 2000* (i.e., they must be confirmed more than 2000 blocks as well as unused for staking for the last 2000 blocks), checking whether the following condition is true:

*sha256d(modifier + utxo{blocktime} + utxo{hash} + utxo{vout} + block{time}) <= target * utxo{value}*

i.e., the exact same process as normal PoS blocks in Qtum, except that the utxos here are the *delegation*'s utxos and not the *staker*'s. Upon finding a valid block, a staker follows the normal procedures for constructing a Qtum PoS block. Once the block has been constructing and the *staker* wishes to sign the block, they should create a compact signature on the following message using *staker{privkey}*:

*sha256d(version + prevblock + merkleroot + time + bits + nonce + stateroot + utxoroot + utxo{hash} + utxo{vout} + PoD)*

Note that the utxo here refers to the delegated utxo and the PoD is the proof of delegation created previously. These are the fields that differ when signing delegated PoS blocks. Once this signature has been created, the blocksig field of the should be set to this signature + PoD. i.e., the blockSig field should be a 130 bytes long variable length byte string consisting of two signatures. The stakePrevout field of the block should be set to the delegation utxo. See appendix for the structure of all fields of the block header.

The first input to the coinstake transaction must be an output with a value >= 100 QTUM. The first output of the coinstake transaction must, as in "non-delegated" PoS blocks, be empty. The second output must be the reward to the to *staker* (*reward * fee / 100*). The third output must be to *delegation* with the remaining reward.

For example, for a delegated PoS block with a *delegation{pubkeyhash} = 0x4008700e91bba17d858722d7112adf436ca416ed* and a *staker{pubkey} = 0x0225a9966a7184dc0542bf8c24ced4a0fab4080f9331e683773d2df138fce6fee2* with a *fee*  of 99%, the coinstake outputs would be the following assuming the input value from *staker* is exactly 100 Qtum and the block subsidy is 4 Qtum:

| output index | scriptPubKey                                                 | value  |
| ------------ | ------------------------------------------------------------ | ------ |
| 0            |                                                              | 0      |
| 1            | 0225a9966a7184dc0542bf8c24ced4a0fab4080f9331e683773d2df138fce6fee2 OP_CHECKSIG | 103.96 |
| 2            | OP_DUP OP_HASH160 4008700e91bba17d858722d7112adf436ca416ed OP_EQUALVERIFY OP_CHECKSIG | 0.04   |



### Appendix

##### Delegated PoS block header structure

| Size | Description          | Data type | Comments                                                     |
| ---- | -------------------- | --------- | ------------------------------------------------------------ |
| 4    | version              | int32_t   | Block version, typically 4.                                  |
| 32   | prev_block           | char[32]  | The previous block hash.                                     |
| 32   | merkle_root          | char[32]  | The Merkle tree root of the block's transactions.            |
| 4    | timestamp            | uint32_t  | Block creation timestamp, the 4 least significant bits must be set to 0. Must be greater than the previous block's timestamp. |
| 4    | bits                 | uint32_t  | The difficulty of this block.                                |
| 4    | nonce                | uint32_t  | A nonce, unused in PoS blocks and therefore usually set to 0. |
| 32   | state_root           | char[32]  | The root of the state trie                                   |
| 32   | utxo_root            | char[32]  | The root of the contract utxo balances trie.                 |
| 32   | stake_prevout_hash   | char[32]  | The delegated staking utxo's hash                            |
| 4    | staking_prevout_vout | uint32_t  | The delegated staking utxo's vout index                      |
| 131  | blockSig             | varlength | The block's signature created by the staker concatenated with the PoD created by the delegator during delegation. Note that the field will be prefixed by a 0x82 byte specifying the length. |

##### addDelegation raw transaction

```
{'blockhash': '2faf179a5253081fabc531bd10f9705502621b15975d841665dbeb8b310f6335',
 'blocktime': 1610453886,
 'confirmations': 1,
 'hash': '51dfe41dc303b99b860c5aa44adabb41bf1de371a52e3204c89fa52b02f10dca',
 'hex': '010000000100647301a87adbb2eb5e72b29f334798574ff1e9f520a9a9c1125ff20cdf01c6000000006a47304402205240e8420b5d1f868c9d54f172edb911966ed7ff91d646e4437b442ee4c44da102204214e6248ff2703fca45f311bc043da3cc4295e05f32b05228887a5b8a66e87c01210390724f049390d99491f805c887d87841e71a22e53f01ccbf38bad074276520b100000000020000000000000000e501040310552201284cc54c0e968c0000000000000000000000007da6be640325a6048cd67f070c314fa405df126b00000000000000000000000000000000000000000000000000000000000000630000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000004120465e98e1dc7f7fa4bdef6bd1775e27cc86e195cd948b28f61bd7cfb9a613247c31032df1dccf43edf24228b942c337e420b06c196a24605e54b75bfd9e16e69e140000000000000000000000000000000000000086c280d5eca3d10100001976a9144008700e91bba17d858722d7112adf436ca416ed88ac00000000',
 'locktime': 0,
 'size': 429,
 'time': 1610453886,
 'txid': '51dfe41dc303b99b860c5aa44adabb41bf1de371a52e3204c89fa52b02f10dca',
 'version': 1,
 'vin': [{'scriptSig': {'asm': '304402205240e8420b5d1f868c9d54f172edb911966ed7ff91d646e4437b442ee4c44da102204214e6248ff2703fca45f311bc043da3cc4295e05f32b05228887a5b8a66e87c[ALL] '
                               '0390724f049390d99491f805c887d87841e71a22e53f01ccbf38bad074276520b1',
                        'hex': '47304402205240e8420b5d1f868c9d54f172edb911966ed7ff91d646e4437b442ee4c44da102204214e6248ff2703fca45f311bc043da3cc4295e05f32b05228887a5b8a66e87c01210390724f049390d99491f805c887d87841e71a22e53f01ccbf38bad074276520b1'},
          'sequence': 0,
          'txid': 'c601df0cf25f12c1a9a920f5e9f14f579847339fb2725eebb2db7aa801736400',
          'vout': 0}],
 'vout': [{'n': 0,
           'scriptPubKey': {'asm': '4 2250000 40 '
                                   '4c0e968c0000000000000000000000007da6be640325a6048cd67f070c314fa405df126b00000000000000000000000000000000000000000000000000000000000000630000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000004120465e98e1dc7f7fa4bdef6bd1775e27cc86e195cd948b28f61bd7cfb9a613247c31032df1dccf43edf24228b942c337e420b06c196a24605e54b75bfd9e16e69e '
                                   '0000000000000000000000000000000000000086 '
                                   'OP_CALL',
                            'hex': '01040310552201284cc54c0e968c0000000000000000000000007da6be640325a6048cd67f070c314fa405df126b00000000000000000000000000000000000000000000000000000000000000630000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000004120465e98e1dc7f7fa4bdef6bd1775e27cc86e195cd948b28f61bd7cfb9a613247c31032df1dccf43edf24228b942c337e420b06c196a24605e54b75bfd9e16e69e140000000000000000000000000000000000000086c2',
                            'type': 'call'},
           'value': Decimal('0E-8')},
          {'n': 1,
           'scriptPubKey': {'addresses': ['qPPxWa7P2dk6TW1QEwmutwMwSPo6Fw51sB'],
                            'asm': 'OP_DUP OP_HASH160 '
                                   '4008700e91bba17d858722d7112adf436ca416ed '
                                   'OP_EQUALVERIFY OP_CHECKSIG',
                            'hex': '76a9144008700e91bba17d858722d7112adf436ca416ed88ac',
                            'reqSigs': 1,
                            'type': 'pubkeyhash'},
           'value': Decimal('19999.10000000')}],
 'vsize': 429,
 'weight': 1716}

```

##### removeDelegation transaction

```
{'blockhash': '2641e2e6582a720476a6617834b88bc11f51aed5e8fbd1c07d39cb06b9676b21',
 'blocktime': 1610453886,
 'confirmations': 1,
 'hash': 'e2fa242270373b3b7bc42b5292fb7babada277781c22fc9d8827941a1a09b770',
 'hex': '0100000001009f8abbe57e7e594775241884dc2fc9d393199b106daff90768dc00d4e75153000000006a47304402203da7a5ef757547dace39856be8e7a36a94d346052d4b9e005b7a42a1db371626022017522913bd341532f983fc3e591c062736d594c2e1da68a21aaaae9d422e74d701210390724f049390d99491f805c887d87841e71a22e53f01ccbf38bad074276520b1000000000200000000000000002301040350c3000128043d666e8b140000000000000000000000000000000000000086c2809b2ba9d10100001976a9144008700e91bba17d858722d7112adf436ca416ed88ac00000000',
 'locktime': 0,
 'size': 235,
 'time': 1610453886,
 'txid': 'e2fa242270373b3b7bc42b5292fb7babada277781c22fc9d8827941a1a09b770',
 'version': 1,
 'vin': [{'scriptSig': {'asm': '304402203da7a5ef757547dace39856be8e7a36a94d346052d4b9e005b7a42a1db371626022017522913bd341532f983fc3e591c062736d594c2e1da68a21aaaae9d422e74d7[ALL] '
                               '0390724f049390d99491f805c887d87841e71a22e53f01ccbf38bad074276520b1',
                        'hex': '47304402203da7a5ef757547dace39856be8e7a36a94d346052d4b9e005b7a42a1db371626022017522913bd341532f983fc3e591c062736d594c2e1da68a21aaaae9d422e74d701210390724f049390d99491f805c887d87841e71a22e53f01ccbf38bad074276520b1'},
          'sequence': 0,
          'txid': '5351e7d400dc6807f9af6d109b1993d3c92fdc8418247547597e7ee5bb8a9f00',
          'vout': 0}],
 'vout': [{'n': 0,
           'scriptPubKey': {'asm': '4 100000 40 -191784509 '
                                   '0000000000000000000000000000000000000086 '
                                   'OP_CALL',
                            'hex': '01040350c3000128043d666e8b140000000000000000000000000000000000000086c2',
                            'type': 'call'},
           'value': Decimal('0E-8')},
          {'n': 1,
           'scriptPubKey': {'addresses': ['qPPxWa7P2dk6TW1QEwmutwMwSPo6Fw51sB'],
                            'asm': 'OP_DUP OP_HASH160 '
                                   '4008700e91bba17d858722d7112adf436ca416ed '
                                   'OP_EQUALVERIFY OP_CHECKSIG',
                            'hex': '76a9144008700e91bba17d858722d7112adf436ca416ed88ac',
                            'reqSigs': 1,
                            'type': 'pubkeyhash'},
           'value': Decimal('19999.96000000')}],
 'vsize': 235,
 'weight': 940}
```

##### coinstake transaction for delegated PoS block

```
{'blockhash': '739a79af31febfee43bb2e3b3acf65231d58eadd76092a10a4e6354a426d2661',
 'blocktime': 1610453888,
 'confirmations': 1,
 'hash': '9ac332299c26b07b6b666d29f4c9e10fc66f92a854068591b47e3d88adf0c1fe',
 'hex': '01000000010ce0e34187d786b1512cb0ddb29c58886664619560c3eaff6adac2253a76ef27000000006a47304402206712c2c824d2ddc08228a2df0462816f87d1240d95bf3549826a97bda536a58102205c36d24a2092cd3ec70e66accf2c3051ac9fa5d0f92d14801de8a76c7e960fa101210225a9966a7184dc0542bf8c24ced4a0fab4080f9331e683773d2df138fce6fee2000000000300000000000000000000787caa9e03000023210225a9966a7184dc0542bf8c24ced4a0fab4080f9331e683773d2df138fce6fee2ac00c817a8040000001976a9144008700e91bba17d858722d7112adf436ca416ed88ac00000000',
 'locktime': 0,
 'size': 244,
 'time': 1610453888,
 'txid': '9ac332299c26b07b6b666d29f4c9e10fc66f92a854068591b47e3d88adf0c1fe',
 'version': 1,
 'vin': [{'scriptSig': {'asm': '304402206712c2c824d2ddc08228a2df0462816f87d1240d95bf3549826a97bda536a58102205c36d24a2092cd3ec70e66accf2c3051ac9fa5d0f92d14801de8a76c7e960fa1[ALL] '
                               '0225a9966a7184dc0542bf8c24ced4a0fab4080f9331e683773d2df138fce6fee2',
                        'hex': '47304402206712c2c824d2ddc08228a2df0462816f87d1240d95bf3549826a97bda536a58102205c36d24a2092cd3ec70e66accf2c3051ac9fa5d0f92d14801de8a76c7e960fa101210225a9966a7184dc0542bf8c24ced4a0fab4080f9331e683773d2df138fce6fee2'},
          'sequence': 0,
          'txid': '27ef763a25c2da6affeac3609561646688589cb2ddb02c51b186d78741e3e00c',
          'vout': 0}],
 'vout': [{'n': 0,
           'scriptPubKey': {'asm': '', 'hex': '', 'type': 'nonstandard'},
           'value': Decimal('0E-8')},
          {'n': 1,
           'scriptPubKey': {'asm': '0225a9966a7184dc0542bf8c24ced4a0fab4080f9331e683773d2df138fce6fee2 '
                                   'OP_CHECKSIG',
                            'hex': '210225a9966a7184dc0542bf8c24ced4a0fab4080f9331e683773d2df138fce6fee2ac',
                            'type': 'pubkey'},
           'value': Decimal('103.96000000')},
          {'n': 2,
           'scriptPubKey': {'addresses': ['qPPxWa7P2dk6TW1QEwmutwMwSPo6Fw51sB'],
                            'asm': 'OP_DUP OP_HASH160 '
                                   '4008700e91bba17d858722d7112adf436ca416ed '
                                   'OP_EQUALVERIFY OP_CHECKSIG',
                            'hex': '76a9144008700e91bba17d858722d7112adf436ca416ed88ac',
                            'reqSigs': 1,
                            'type': 'pubkeyhash'},
           'value': Decimal('0.04000000')}],
 'vsize': 244,
 'weight': 976}
```


##### Test case for adding delegation, submitting a valid delegated block and removing delegation

```
#!/usr/bin/env python3

from test_framework.test_framework import BitcoinTestFramework
from test_framework.messages import *
from test_framework.script import *
from test_framework.mininode import *
from test_framework.qtum import *
from test_framework.qtumconfig import *
from test_framework.util import *
import time
import base64
import pprint

pp = pprint.PrettyPrinter()

def signmessage(key, msg):
    sighash = hash256(b"\x15Qtum Signed Message:\n\x28"+msg.encode('ascii'))
    sig = key.sign_ecdsa(sighash, low_s=True, der_sig=False)
    return sig

def signdelegatedblock(key, block, pod):
    sigdata = b""
    sigdata += struct.pack("<i", block.nVersion)
    sigdata += ser_uint256(block.hashPrevBlock)
    sigdata += ser_uint256(block.hashMerkleRoot)
    sigdata += struct.pack("<I", block.nTime)
    sigdata += struct.pack("<I", block.nBits)
    sigdata += struct.pack("<I", block.nNonce)
    sigdata += ser_uint256(block.hashStateRoot)
    sigdata += ser_uint256(block.hashUTXORoot)
    sigdata += block.prevoutStake.serialize()
    sigdata += struct.pack("<b", len(pod)) + pod
    blocksig = key.sign_ecdsa(hash256(sigdata), low_s=True, der_sig=False)
    return blocksig


class QtumSimpleDelegationContractTest(BitcoinTestFramework):
    def set_test_params(self):
        self.setup_clean_chain = True
        self.num_nodes = 2
        self.extra_args = [['-txindex=1', '-logevents=1'], ['-txindex=1', '-logevents=1']]

    def run_test(self):
        mocktime = 1610443886
        for n in self.nodes: n.setmocktime(mocktime)

        self.delegator = self.nodes[0]
        delegator_address = "qPPxWa7P2dk6TW1QEwmutwMwSPo6Fw51sB"
        delegator_address_hex = "4008700e91bba17d858722d7112adf436ca416ed"
        delegator_privkey = "cQA8JyNZc4YTsvV44Y6HFQMLfRTfS49rSDMSuNSgRauwtBCj9ieq"
        delegator_eckey = wif_to_ECKey(delegator_privkey)
        self.delegator.importprivkey(delegator_privkey)

        self.staker = self.nodes[1]
        staker_address = "qV1mNZokPVcrQcH8RdnfzHsVVyVSGFnaue"
        staker_address_hex = "7da6be640325a6048cd67f070c314fa405df126b"
        staker_privkey = "cNYezxiDtCu5DMUjqAv31tnGAMMi3Kh7xLYFR7tWUCvbSdMz78N8"
        staker_eckey = wif_to_ECKey(staker_privkey)
        self.staker.importprivkey(staker_privkey)

        self.staker.generatetoaddress(1, staker_address)
        self.sync_all()
        self.delegator.generatetoaddress(COINBASE_MATURITY+100, delegator_address)
        self.sync_all()
        self.staker.generatetoaddress(COINBASE_MATURITY, staker_address)
        self.sync_all()
        for n in self.nodes: n.setmocktime(mocktime+10000)


        offline_staking_contract_address = bytes.fromhex("0000000000000000000000000000000000000086")
        pod = signmessage(delegator_eckey, staker_address_hex)
        calldata = bytes.fromhex("4c0e968c") # function abi
        calldata += b'\x00'*12 + bytes.fromhex(staker_address_hex)
        calldata += b'\x00'*31 + b'\x63'
        calldata += b'\x00'*31 + b'\x60'
        calldata += b'\x00'*31 + b'\x41'
        calldata += pod
        contract_call_script = CScript([b'\x04', CScriptNum(2250000), CScriptNum(40), calldata, offline_staking_contract_address, OP_CALL])
        change_script = CScript([OP_DUP, OP_HASH160, bytes.fromhex(delegator_address_hex), OP_EQUALVERIFY, OP_CHECKSIG])

        delegator_unspent = self.delegator.listunspent()[0]
        delegator_unspent_outpoint = COutPoint(int(delegator_unspent['txid'], 16), delegator_unspent['vout'])
        tx = CTransaction()
        tx.vin = [CTxIn(delegator_unspent_outpoint)]
        tx.vout.append(CTxOut(0, scriptPubKey=contract_call_script)) # The contract call
        tx.vout.append(CTxOut(int(delegator_unspent['amount']*COIN) - 2250000*40, scriptPubKey=change_script)) # change output
        tx = rpc_sign_transaction(self.delegator, tx)
        txid = self.delegator.sendrawtransaction(tx.serialize().hex())
        self.delegator.generatetoaddress(1, delegator_address)

        # We have now added a delegation, let's stake a block for that delegation.
        prevblock = self.delegator.getblock(self.delegator.getbestblockhash())
        blocktime = (prevblock['time']+0x10) & 0xfffffff0

        for delegator_unspent in self.delegator.listunspent():
            if delegator_unspent['confirmations'] <= 500:
                continue

            delegator_utxo = COutPoint(int(delegator_unspent['txid'], 16), delegator_unspent['vout'])
            txtime = self.delegator.getrawtransaction(delegator_unspent['txid'], True)['time']

            target = uint256_from_compact(int(prevblock['bits'], 16))
            data = b""
            data += ser_uint256(int(prevblock['modifier'], 16))
            data += struct.pack("<I", txtime)
            data += delegator_utxo.serialize()
            data += struct.pack("<I", blocktime)
            kernel = uint256_from_str(hash256(data))

            # valid block found?
            if kernel <= (target*int(delegator_unspent['amount']*COIN)) & (2**256 - 1):
                coinbase = create_coinbase(prevblock['height']+1)
                coinbase.vout[0].nValue = 0
                coinbase.vout[0].scriptPubKey = b""
                coinbase.rehash()

                block = create_block(int(prevblock['hash'], 16), coinbase, blocktime)
                block.nTime = blocktime
                block.hashStateRoot = int(prevblock['hashStateRoot'], 16)
                block.hashUTXORoot = int(prevblock['hashUTXORoot'], 16)
                block.prevoutStake = delegator_utxo

                # Find an unspent staker tx with value > 100, we know that all unspent staker txs fulfill this requirement
                staker_unspent = self.staker.listunspent()[0]
                staker_subsidy = INITIAL_BLOCK_REWARD*COIN*99//100
                staker_reward_script = CScript([staker_eckey.get_pubkey().get_bytes(), OP_CHECKSIG])
                delegation_reward_script = CScript([OP_DUP, OP_HASH160, bytes.fromhex(delegator_address_hex), OP_EQUALVERIFY, OP_CHECKSIG])

                coinstake_tx = CTransaction()
                coinstake_tx.vin = [CTxIn(COutPoint(int(staker_unspent['txid'], 16), staker_unspent['vout']))]
                coinstake_tx.vout.append(CTxOut())
                coinstake_tx.vout.append(CTxOut(staker_subsidy + int(staker_unspent['amount']*COIN), scriptPubKey=staker_reward_script))
                coinstake_tx.vout.append(CTxOut(int(INITIAL_BLOCK_REWARD*COIN-staker_subsidy), scriptPubKey=delegation_reward_script))
                coinstake_tx = rpc_sign_transaction(self.staker, coinstake_tx)
                block.vtx.append(coinstake_tx)
                block.hashMerkleRoot = block.calc_merkle_root()

                # create the signature
                blocksig = signdelegatedblock(staker_eckey, block, pod)
                block.vchBlockSig = blocksig + pod
                block.rehash()
                self.staker.submitblock(block.serialize().hex())
                break

        # Finally remove the delegation
        calldata = bytes.fromhex("3d666e8b") # function abi
        contract_call_script = CScript([b'\x04', CScriptNum(100000), CScriptNum(40), calldata, offline_staking_contract_address, OP_CALL])
        change_script = CScript([OP_DUP, OP_HASH160, bytes.fromhex(delegator_address_hex), OP_EQUALVERIFY, OP_CHECKSIG])

        delegator_unspent = self.delegator.listunspent()[0]
        delegator_unspent_outpoint = COutPoint(int(delegator_unspent['txid'], 16), delegator_unspent['vout'])
        tx = CTransaction()
        tx.vin = [CTxIn(delegator_unspent_outpoint)]
        tx.vout.append(CTxOut(0, scriptPubKey=contract_call_script)) # The contract call
        tx.vout.append(CTxOut(int(delegator_unspent['amount']*COIN) - 100000*40, scriptPubKey=change_script)) # change output
        tx = rpc_sign_transaction(self.delegator, tx)
        txid = self.delegator.sendrawtransaction(tx.serialize().hex())
        self.delegator.generatetoaddress(1, delegator_address)

if __name__ == '__main__':
    QtumSimpleDelegationContractTest().main()
```