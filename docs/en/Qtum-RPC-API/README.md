# Qtum-RPC-API

**This document includes the full list of Qtum RPCs based on Qtum core v0.17.6. According to this document you can learn how to use Qtum RPC API.** 

## Tables of Contents 

- [Blockchain](#blockchain)
	- [callcontract](#callcontract)
	- [getaccountinfo](#getaccountinfo)
	- [getbestblockhash](#getbestblockhash)
	- [getblock](#getblock)
	- [getblockchaininfo](#getblockchaininfo)
	- [getblockcount](#getblockcount)
	- [getblockhash](#getblockhash)
	- [getblockheader](#getblockheader)
	- [getblockstats](#getblockstats)
	- [getchaintips](#getchaintips)
	- [getchaintxstats](#getchaintxstats)
	- [getdifficulty](#getdifficulty)
	- [getmempoolancestors](#getmempoolancestors)
	- [getmempooldescendants](#getmempooldescendants)
	- [getmempoolentry](#getmempoolentry)
	- [getmempoolinfo](#getmempoolinfo)
	- [getrawmempool](#getrawmempool)
	- [getstorage](#getstorage)
	- [gettransactionreceipt](#gettransactionreceipt)
	- [gettxout](#gettxout)
	- [gettxoutproof](#gettxoutproof)
	- [gettxoutsetinfo](#gettxoutsetinfo)
	- [listcontracts](#listcontracts)
	- [preciousblock](#preciousblock)
	- [pruneblockchain](#pruneblockchain)
	- [savemempool](#savemempool)
	- [scantxoutset](#scantxoutset)
	- [searchlogs](#searchlogs)
	- [verifychain](#verifychain)
	- [verifytxoutproof](#verifytxoutproof)
	- [waitforlogs](#waitforlogs)
- [Control](#control)
	- [getmemoryinfo](#getmemoryinfo)
	- [help](#help)
	- [logging](#logging)
	- [stop](#stop)
	- [uptime](#uptime)
- [Generating ](#Generating )
	- [generate](#generate)
	- [generatetoaddress](#generatetoaddress)
- [Mining ](#mining )
	- [getblocktemplate](#getblocktemplate)
	- [getmininginfo](#getmininginfo)
	- [getnetworkhashps](#getnetworkhashps)
	- [getstakinginfo](#getstakinginfo)
	- [getsubsidy](#getsubsidy)
	- [prioritisetransaction](#prioritisetransaction)
	- [submitblock](#submitblock)
- [Network ](#network )
	- [addnode](#addnode)
	- [clearbanned](#clearbanned)
	- [disconnectnode](#disconnectnode)
	- [getaddednodeinfo](#getaddednodeinfo)
	- [getconnectioncount](#getconnectioncount)
	- [getnettotals](#getnettotals)
	- [getnetworkinfo](#getnetworkinfo)
	- [getpeerinfo](#getpeerinfo)
	- [listbanned](#listbanned)
	- [ping](#ping)
	- [setban](#setban)
	- [setnetworkactive](#setnetworkactive)
- [Rawtransactions](#rawtransactions)
	- [combinepsbt](#combinepsbt)
	- [combinerawtransaction](#combinerawtransaction)
	- [converttopsbt](#converttopsbt)
	- [createpsbt](#createpsbt)
	- [createrawtransaction](#createrawtransaction)
	- [decodepsbt](#decodepsbt)
	- [decoderawtransaction](#decoderawtransaction)
	- [decodescript](#decodescript)
	- [finalizepsbt](#finalizepsbt)
	- [fromhexaddress](#fromhexaddress)
	- [fundrawtransaction](#fundrawtransaction)
	- [gethexaddress](#gethexaddress)
	- [getrawtransaction](#getrawtransaction)
	- [sendrawtransaction](#sendrawtransaction)
	- [signrawtransaction](#signrawtransaction)
	- [signrawtransactionwithkey](#signrawtransactionwithkey)
	- [testmempoolaccept](#testmempoolaccept)
- [Util](#util)
	- [createmultisig](#createmultisig)
	- [estimatesmartfee](#estimatesmartfee)
	- [signmessagewithprivkey](#signmessagewithprivkey)
	- [validateaddress](#validateaddress)
	- [verifymessage](#verifymessage)
- [Wallet](#wallet)
	- [abandontransaction](#abandontransaction)
	- [abortrescan](#abortrescan)
	- [addmultisigaddress](#addmultisigaddress)
	- [backupwallet](#backupwallet)
	- [bumpfee](#bumpfee)
	- [createcontract](#createcontract)
	- [createwallet](#createwallet)
	- [dumpprivkey ](#dumpprivkey )
	- [dumpwallet](#dumpwallet)
	- [encryptwallet](#encryptwallet)
	- [getaddressesbylabel](#getaddressesbylabel)
	- [getaddressinfo](#getaddressinfo)
	- [getbalance](#getbalance)
	- [getnewaddress](#getnewaddress)
	- [getrawchangeaddress](#getrawchangeaddress)
	- [getreceivedbyaddress](#getreceivedbyaddress)
	- [gettransaction](#gettransaction)
	- [getunconfirmedbalance](#getunconfirmedbalance)
	- [getwalletinfo](#getwalletinfo)
	- [importaddress](#importaddress)
	- [importmulti](#importmulti)
	- [importprivkey](#importprivkey)
	- [importprunedfunds](#importprunedfunds)
	- [importpubkey](#importpubkey)
	- [importwallet](#importwallet)
	- [keypoolrefill](#keypoolrefill)
	- [listaccounts](#listaccounts)
	- [listaddressgroupings](#listaddressgroupings)
	- [listlabels](#listlabels)
	- [listlockunspent](#listlockunspent)
	- [listreceivedbyaddress](#listreceivedbyaddress)
	- [listsinceblock](#listsinceblock)
	- [listtransactions](#listtransactions)
	- [listunspent](#listunspent)
	- [listwallets](#listwallets)
	- [loadwallet](#loadwallet)
	- [lockunspent](#lockunspent)
	- [removeprunedfunds](#removeprunedfunds)
	- [rescanblockchain](#rescanblockchain)
	- [reservebalance](#reservebalance)
	- [sendmany](#sendmany)
	- [sendmanywithdupes](#sendmanywithdupes)
	- [sendtoaddress](#sendtoaddress)
	- [sendtocontract](#sendtocontract)
	- [sethdseed](#sethdseed)
	- [settxfee](#settxfee)
	- [signmessage](#signmessage)
	- [signrawtransactionwithwallet](#signrawtransactionwithwallet)
	- [unloadwallet](#unloadwallet)
	- [walletcreatefundedpsbt](#walletcreatefundedpsbt)
	- [walletlock](#walletlock)
	- [walletpassphrase](#walletpassphrase)
	- [walletpassphrasechange](#walletpassphrasechange)
	- [walletprocesspsbt](#walletprocesspsbt)
- [Zmq](#zmq)
	- [getzmqnotifications](#getzmqnotifications)

## Blockchain

### callcontract

callcontract "address" "data" ( address )

**Argument:**

    1. "address" (string, required) The account address
    2. "data"    (string, required) The data hex string
    3. address   (string, optional) The sender address hex string
    4. gasLimit  (string, optional) The gas limit for executing the contract

**Test example:** 

    ./qtum-cli callcontract "74045ec0dc26ec1861473828bc140ebc4c1f3eff" "00000000000000000000000000000000000000000000000000000000000000a9"

**Test result:**

    {
      "address": "74045ec0dc26ec1861473828bc140ebc4c1f3eff",
      "executionResult": {
      "gasUsed": 39999999,
      "excepted": "None",
      "newAddress": "74045ec0dc26ec1861473828bc140ebc4c1f3eff",
      "output": "",
      "codeDeposit": 0,
      "gasRefunded": 0,
      "depositSize": 0,
      "gasForDeposit": 0
      },
      "transactionReceipt": 
      {
        "stateRoot": "1253c56cf79597e89ce179f14e6a86a493356dac410c30efc576503687ad2670",
        "gasUsed": 39999999,
        "bloom": "00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "log": [
      ]
      }
    }
    
### getaccountinfo

Contract details including balance, storage data and code

**Argument:**

    1. "address"(string, required) The contract address

**Result:**

    Contract details including balance, storage data and code

**Test example:**

    ./qtum-cli getaccountinfo "fdb9d0873ba524ef3ea67c1719666968e1eeb110"

### getbestblockhash

Returns the hash of the best (tip) block in the longest blockchain.

**Result:**

    "hex" (string) the block hash hex encoded

**Examples:**

    >qtum-cli getbestblockhash  
    
    >curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbestblockhash", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getbestblockhash

**Test result:**

    e006ada4d1b7caf1559cc1b5b520ab8c54f51486230f2ea18d2692d3a095ba03

### getblock

According the blockhash returns the info of the corresponding block
If verbosity is 0, returns a string that is serialized, hex-encoded data for block 'hash'.
If verbosity is 1, returns an Object with information about block <hash>.
If verbosity is 2, returns an Object with information about block <hash> and information about each transaction.

**Arguments:**
    
    1. "blockhash" (string, required) The block hash
    2. verbosity (numeric, optional, default=1) 0 for hex encoded data, 1 for a json object, and 2 for json object with transaction data

**Result (for verbosity = 0):**

    "data" (string) A string that is serialized, hex-encoded data for block 'hash'.

**Result (for verbosity = 1):**
    
    {
      "hash" : "hash",       (string) the block hash (same as provided)
      "confirmations" : n,   (numeric) The number of confirmations, or -1 if the block is not on the main chain
      "size" : n,            (numeric) The block size
      "strippedsize" : n,    (numeric) The block size excluding witness data
      "weight" : n           (numeric) The block weight as defined in BIP 141
      "height" : n,          (numeric) The block height or index
      "version" : n,         (numeric) The block version
      "versionHex" : "00000000", (string) The block version formatted in hexadecimal
      "merkleroot" : "xxxx", (string) The merkle root
      "tx" : [               (array of string) The transaction ids
         "transactionid"     (string) The transaction id
         ,...
      ],
      "time" : ttt,          (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
      "mediantime" : ttt,    (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
      "nonce" : n,           (numeric) The nonce
      "bits" : "1d00ffff",   (string) The bits
      "difficulty" : x.xxx,  (numeric) The difficulty
      "chainwork" : "xxxx",  (string) Expected number of hashes required to produce the chain up to this block (in hex)
      "nTx" : n,             (numeric) The number of transactions in the block.
      "previousblockhash" : "hash",  (string) The hash of the previous block
      "nextblockhash" : "hash"       (string) The hash of the next block
    }
    
**Result (for verbosity = 2):**
    
    {
        ..., Same output as verbosity = 1.
        "tx" : [ (array of Objects) The transactions in the format of the getrawtransaction RPC. Different from verbosity = 1 "tx" result.
        ,...
        ],
        ,... Same output as verbosity = 1.
    }

**Examples:**

    > qtum-cli getblock "00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblock", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**test examples:**

    ./qtum-cli getblock “eeab43864b89c15bd1ffad21eaabc97f4fa4a576a71b46c9d512afc26168569f”

**Test result:**

    {
      "hash": "eeab43864b89c15bd1ffad21eaabc97f4fa4a576a71b46c9d512afc26168569f",
      "confirmations": 2,
      "strippedsize": 846,
      "size": 882,
      "weight": 3420,
      "height": 402359,
      "version": 536870912,
      "versionHex": "20000000",
      "merkleroot": "359698a4d0e24baadfe9892b56bb5a6090830aea9fe1bf221f4766d7d552eeff",
      "hashStateRoot": "6099ad48961a320b62cc29ba3d89dcbd8bbc0e33069f6c7169ba008039cbc44f",
      "hashUTXORoot": "9e729950c184acd011471252a0c1a4bc279cd4c1e86d543bead4af6df787b2dd",
      "tx": [
        "9cd9f5e952988cd88c73b7cd172cc17f7ba6ec7c34918b50fbfa3901251cbc2f",
        "49260697a2d127541cfd5190fc18a5193f118d4b1cc23504a520983ad7f0ee35"
      ],
      "time": 1562145008,
      "mediantime": 1562144608,
      "nonce": 0,
      "bits": "1a037540",
      "difficulty": 4851625.823213781,
      "chainwork": "000000000000000000000000000000000000000000000114688c263219ba17a6",
      "nTx": 2,
      "previousblockhash": "dd7ccce7a7b419874dac6097c6505c3b00efdce9336aa9ad79363c81d8a05e26",
      "nextblockhash": "60ef2b919581b7d7f684e6e2de574ee72ac94cb924770988d2686ca4c3b6e24a",
      "flags": "proof-of-stake",
      "proofhash": "000001199a996fef47845c16830c9187ed076dea11d34ba734201a011945c962",
      "modifier": "148572257a37c882895429d69b15d8a2446be5ad5f0d74237ecf621841164990",
      "signature": "304402204fe60e75699f3773e3c1d86281f2e7cf17268d23e40628622b3a215fea299e68022041c767b4e2ede77311aeaca2dfafc8f9066f628d2aa3234a57604cebc976c311"
    }

### getblockchaininfo 

Returns an object containing various state info regarding blockchain processing.

**Result:**

    {
      "chain": "xxxx",              (string) current network name as defined in BIP70 (main, test, regtest)
      "blocks": xxxxxx,             (numeric) the current number of blocks processed in the server
      "headers": xxxxxx,            (numeric) the current number of headers we have validated
      "bestblockhash": "...",       (string) the hash of the currently best block
      "difficulty": xxxxxx,         (numeric) the current difficulty
      "mediantime": xxxxxx,         (numeric) median time for the current best block
      "verificationprogress": xxxx, (numeric) estimate of verification progress [0..1]
      "initialblockdownload": xxxx, (bool) (debug information) estimate of whether this node is in Initial Block Download mode.
      "chainwork": "xxxx"           (string) total amount of work in active chain, in hexadecimal
      "size_on_disk": xxxxxx,       (numeric) the estimated size of the block and undo files on disk
      "pruned": xx,                 (boolean) if the blocks are subject to pruning
      "pruneheight": xxxxxx,        (numeric) lowest-height complete block stored (only present if pruning is enabled)
      "automatic_pruning": xx,      (boolean) whether automatic pruning is enabled (only present if pruning is enabled)
      "prune_target_size": xxxxxx,  (numeric) the target size used by pruning (only present if automatic pruning is enabled)
      "softforks": [                (array) status of softforks in progress
         {
            "id": "xxxx",           (string) name of softfork
            "version": xx,          (numeric) block version
            "reject": {             (object) progress toward rejecting pre-softfork blocks
               "status": xx,        (boolean) true if threshold reached
            },
         }, ...
      ],
      "bip9_softforks": {           (object) status of BIP9 softforks in progress
         "xxxx" : {                 (string) name of the softfork
            "status": "xxxx",       (string) one of "defined", "started", "locked_in", "active", "failed"
            "bit": xx,              (numeric) the bit (0-28) in the block version field used to signal this softfork (only for "started" status)
            "startTime": xx,        (numeric) the minimum median time past of a block at which the bit gains its meaning
            "timeout": xx,          (numeric) the median time past of a block at which the deployment is considered failed if not yet locked in
            "since": xx,            (numeric) height of the first block to which the status applies
            "statistics": {         (object) numeric statistics about BIP9 signalling for a softfork (only for "started" status)
               "period": xx,        (numeric) the length in blocks of the BIP9 signalling period 
               "threshold": xx,     (numeric) the number of blocks with the version bit set required to activate the feature 
               "elapsed": xx,       (numeric) the number of blocks elapsed since the beginning of the current period 
               "count": xx,         (numeric) the number of blocks with the version bit set in the current period 
               "possible": xx       (boolean) returns false if there are not enough blocks left in this period to pass activation threshold 
            }
         }
      }
      "warnings" : "...",           (string) any network and blockchain warnings.
    }

**Test example:** 

    ./qtum-cli getblockchaininfo

**Test result:**

    {
      "chain": "main",
      "blocks": 401574,
      "headers": 401574,
      "bestblockhash": "be4cb62080f36d2c3a45127e016460aca82ea1de17af4166ad9341d1a18e00cc",
      "difficulty": 1699339.658646735,
      "moneysupply": 101586296,
      "mediantime": 1562032592,
      "verificationprogress": 0.9999994694221126,
      "initialblockdownload": false,
      "chainwork": "000000000000000000000000000000000000000000000113f4c983f14834f842",
      "size_on_disk": 1939468044,
      "pruned": false,
      "softforks": [
      {
        "id": "bip34",
        "version": 2,
        "reject": {
        "status": true
        }
      },
      {
        "id": "bip66",
        "version": 3,
        "reject": {
        "status": true
        }
      },
      {
        "id": "bip65",
        "version": 4,
        "reject": {
        "status": true
        }
      }
      ],
      "bip9_softforks": {
      "csv": {
        "status": "active",
        "startTime": 0,
        "timeout": 999999999999,
        "since": 6048
      },
      "segwit": {
        "status": "active",
        "startTime": 0,
        "timeout": 999999999999,
        "since": 6048
      }
      },
      "warnings": ""
    }

### getblockcount

Returns the number of blocks in the longest blockchain.

**Result:**

    n (numeric) The current block count

**Examples:**

    > qtum-cli getblockcount 
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:** 

    ./qtum-cli getblockcount
    
**Test result:** 

    395049

### getblockhash    

Returns hash of block in best-block-chain at height provided.

**Arguments:**

    1. height         (numeric, required) The height index

**Result:**   

    "hash"         (string) The block hash  

**Examples:**

    > qtum-cli getblockhash 1000  
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockhash", "params": [1000] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getblockhash 1
    
**Test result:**

    0000d5dab5e76310ae640e9bcfa270c2eb23a1e5948bdf01fc7ed1f157110ab7

### getblockheader

Returns the corresponding block header information according to the given index
If verbose is false, returns a string that is serialized, hex-encoded data for blockheader 'hash'.
If verbose is true, returns an Object with information about blockheader <hash>.

**Arguments:**

    1. "hash"  (string, required) The block hash
    2. verbose (boolean, optional, default=true) true for a json object, false for the hex encoded data
    
**Result (for verbose = true):**

    {
      "hash" : "hash",               (string) the block hash (same as provided)
      "confirmations" : n,           (numeric) The number of confirmations, or -1 if the block is not on the main chain
      "height" : n,                  (numeric) The block height or index
      "version" : n,                 (numeric) The block version
      "versionHex" : "00000000",     (string) The block version formatted in hexadecimal
      "merkleroot" : "xxxx",         (string) The merkle root
      "time" : ttt,                  (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
      "mediantime" : ttt,            (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
      "nonce" : n,                   (numeric) The nonce
      "bits" : "1d00ffff",           (string) The bits
      "difficulty" : x.xxx,          (numeric) The difficulty
      "chainwork" : "0000...1f3"     (string) Expected number of hashes required to produce the current chain (in hex)
      "nTx" : n,                     (numeric) The number of transactions in the block.
      "previousblockhash" : "hash",  (string) The hash of the previous block
      "nextblockhash" : "hash",      (string) The hash of the next block
    }

**Result (for verbose = false):**

    "data" (string) A string that is serialized, hex-encoded data for block 'hash'.
    
**Examples:**

    > qtum-cli getblockheader "00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"
        
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockheader", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getblockheader 
    “ebd10c9b338247a9ccfd45493b484ae5638a5d97ddaa68c44c6ef214ea443c19”

**Test result:**

     {
        "hash": "ebd10c9b338247a9ccfd45493b484ae5638a5d97ddaa68c44c6ef214ea443c19",
        "confirmations": -1,
        "height": 388910,
        "version": 536870912,
        "versionHex": "20000000",
        "merkleroot": "b1a21dd48f978ea8671383f9454d058d2047d19666348340bea543cf89e31aca",
        "time": 1560222144,
        "mediantime": 1560221568,
        "nonce": 0,
        "bits": "1a097561",
        "difficulty": 1773742.122273433,
        "chainwork": "00000000000000000000000000000000000000000000010ca5944ed9b867aaef",
        "nTx": 7,
        "hashStateRoot": "10504057696a3ad9f96254b86424cc8f49f3ef2b271893f933b18174e538b828",
        "hashUTXORoot": "9e729950c184acd011471252a0c1a4bc279cd4c1e86d543bead4af6df787b2dd",
        "previousblockhash": "56044826105d66a95ab6f97f945a7cd18eef7109c59da64a7b6c57c377eaf4bb",
        "flags": "proof-of-stake",
        "proofhash": "0000000000000000000000000000000000000000000000000000000000000000",
        "modifier": "1551ed22c1a43da60aebcb2d66a1e42d9bf6a007276367a4a189325ea37a1f91"
     }

### getblockstats

Compute per block statistics for a given window. All amounts are in satoshis.
It won't work for some heights with pruning.
It won't work without -txindex for utxo_size_inc, *fee or *feerate stats.

**Arguments:**

    1. "hash_or_height"     (string or numeric, required) The block hash or height of the target block
    2. "stats"              (array,  optional) Values to plot, by default all values (see result below)
        [
          "height",         (string, optional) Selected statistic
          "time",           (string, optional) Selected statistic
          ,...
        ]

**Result:**

     {                           
      "avgfee": xxxxx,          (numeric) Average fee in the block
      "avgfeerate": xxxxx,      (numeric) Average feerate (in satoshis per virtual byte)
      "avgtxsize": xxxxx,       (numeric) Average transaction size
      "blockhash": xxxxx,       (string) The block hash (to check for potential reorgs)
      "feerate_percentiles": [  (array of numeric) Feerates at the 10th, 25th, 50th, 75th, and 90th percentile weight unit (in satoshis per virtual byte)
          "10th_percentile_feerate",      (numeric) The 10th percentile feerate
          "25th_percentile_feerate",      (numeric) The 25th percentile feerate
          "50th_percentile_feerate",      (numeric) The 50th percentile feerate
          "75th_percentile_feerate",      (numeric) The 75th percentile feerate
          "90th_percentile_feerate",      (numeric) The 90th percentile feerate
      ],
      "height": xxxxx,          (numeric) The height of the block
      "ins": xxxxx,             (numeric) The number of inputs (excluding coinbase)
      "maxfee": xxxxx,          (numeric) Maximum fee in the block
      "maxfeerate": xxxxx,      (numeric) Maximum feerate (in satoshis per virtual byte)
      "maxtxsize": xxxxx,       (numeric) Maximum transaction size
      "medianfee": xxxxx,       (numeric) Truncated median fee in the block
      "mediantime": xxxxx,      (numeric) The block median time past
      "mediantxsize": xxxxx,    (numeric) Truncated median transaction size
      "minfee": xxxxx,          (numeric) Minimum fee in the block
      "minfeerate": xxxxx,      (numeric) Minimum feerate (in satoshis per virtual byte)
      "mintxsize": xxxxx,       (numeric) Minimum transaction size
      "outs": xxxxx,            (numeric) The number of outputs
      "subsidy": xxxxx,         (numeric) The block subsidy
      "swtotal_size": xxxxx,    (numeric) Total size of all segwit transactions
      "swtotal_weight": xxxxx,  (numeric) Total weight of all segwit transactions divided by segwit scale factor (4)
      "swtxs": xxxxx,           (numeric) The number of segwit transactions
      "time": xxxxx,            (numeric) The block time
      "total_out": xxxxx,       (numeric) Total amount in all outputs (excluding coinbase and thus reward [ie subsidy + totalfee])
      "total_size": xxxxx,      (numeric) Total size of all non-coinbase transactions
      "total_weight": xxxxx,    (numeric) Total weight of all non-coinbase transactions divided by segwit scale factor (4)
      "totalfee": xxxxx,        (numeric) The fee total
      "txs": xxxxx,             (numeric) The number of transactions (excluding coinbase)
      "utxo_increase": xxxxx,   (numeric) The increase/decrease in the number of unspent outputs
      "utxo_size_inc": xxxxx,   (numeric) The increase/decrease in size for the utxo index (not discounting op_return and similar)
    }
    
**Examples:**

    > qtum-cli getblockstats 1000 '["minfeerate","avgfeerate"]'
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockstats", "params": [1000 '["minfeerate","avgfeerate"]'] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### getchaintips

Return information about all known tips in the block tree, including the main chain as well as orphaned branches.

**Result:**

     [
        {
          "height": xxxx,    (numeric) height of the chain tip
          "hash": "xxxx",    (string) block hash of the tip
          "branchlen": 0     (numeric) zero for main chain
          "status": "active" (string) "active" for the main chain
        },
        {
          "height": xxxx,
          "hash": "xxxx",
          "branchlen": 1     (numeric) length of branch connecting the tip to the main chain
          "status": "xxxx"   (string) status of the chain (active, valid-fork, valid-headers, headers-only, invalid)
        }
      ]

**Possible values for status:**
1. "invalid" This branch contains at least one invalid block
2. "headers-only" Not all blocks for this branch are available, but the headers are valid
3. "valid-headers" All blocks are available for this branch, but they were never fully validated
4. "valid-fork" This branch is not part of the active chain, but is fully validated
5. "active" This is the tip of the active main chain, which is certainly valid

**Examples:**

    > qtum-cli getchaintips
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getchaintips", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getchaintips

**Result:**

    [
      {
        "height": 353464,
        "hash": "342e378ff153232fb08efe61ceb2fc00e28b1569aa0de97d031ba0bab98387be",
        "branchlen": 2,
        "status": "invalid"
      },
      {
        "height": 353415,
        "hash": "f1748f4c718cf5d36bab1dc7f4199e0e0379a338e6ea55fb18860daa0bc0c604",
        "branchlen": 1,
        "status": "valid-fork"
      },
      {
        "height": 353388,
        "hash": "1fbd1234497731d8f3296c60e9d21cc5c8d57b19d4fe7f154b4aa17e47b526b8",
        "branchlen": 1,
        "status": "valid-headers"
      },
      {
        "height": 353103,
        "hash": "583b2cd790cc493390474306cb78de68e4ba2f0bfdae852ab36c240fb058c559",
        "branchlen": 1,
        "status": "valid-fork"
      },...
    ]
### getchaintxstats

Compute statistics about the total number and rate of transactions in the chain.

**Arguments:**

    1. nblocks     (numeric, optional) Size of the window in number of blocks (default: one month).
    2. "blockhash" (string, optional) The hash of the block that ends the window.

**Result:**

     {
      "time": xxxxx,                         (numeric) The timestamp for the final block in the window in UNIX format.
      "txcount": xxxxx,                      (numeric) The total number of transactions in the chain up to that point.
      "window_final_block_hash": "...",      (string) The hash of the final block in the window.
      "window_block_count": xxxxx,           (numeric) Size of the window in number of blocks.
      "window_tx_count": xxxxx,              (numeric) The number of transactions in the window. Only returned if "window_block_count" is > 0.
      "window_interval": xxxxx,              (numeric) The elapsed time in the window in seconds. Only returned if "window_block_count" is > 0.
      "txrate": x.xx,                        (numeric) The average rate of transactions per second in the window. Only returned if "window_interval" is > 0.
    }

**Examples:**

    > qtum-cli getchaintxstats
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getchaintxstats", "params": [2016] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
**Test result:**

    {
      "time": 1561602624,
      "txcount": 866823,
      "window_final_block_hash": "ea6b26303facc34404da3174962a5c1d8d00369a3ff27aa50238ba8f24170280",
      "window_block_count": 20250,
      "window_tx_count": 41012,
      "window_interval": 2655920,
      "txrate": 0.01544173017259556
    }
    
### getdifficulty

Returns the proof-of-work difficulty as a multiple of the minimum difficulty.

Returns the proof-of-stake difficulty as a multiple of the minimum difficulty.

**Result:**

    n.nnn (numeric) the proof-of-work difficulty as a multiple of the minimum difficulty.

**Examples:**

    > qtum-cli getdifficulty
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getdifficulty", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
**Test example:**

    ./qtum-cli getdifficulty
**Test result:**

    {
      "proof-of-work": 1.52587890625e-05,
      "proof-of-stake": 7022116.100551808
    }
    
### getmempoolancestors 

If txid is in the mempool, returns all in-mempool ancestors.

**Arguments:**

    1. "txid"  (string, required) The transaction id (must be in mempool)
    2. verbose (boolean, optional, default=false) True for a json object, false for array of transaction ids
    
   **Result (for verbose = false):**
  
      [ 
        "transactionid" (string) The transaction id of an in-mempool ancestor transaction
        ,...
      ]

**Result (for verbose=true):**

    {                           
      "transactionid" : {       
        "size" : n,             (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
        "fee" : n,              (numeric) transaction fee in QTUM (DEPRECATED)
        "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority (DEPRECATED)
        "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
        "height" : n,           (numeric) block height when transaction entered pool
        "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
        "descendantsize" : n,   (numeric) virtual transaction size of in-mempool descendants (including this one)
        "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one) (DEPRECATED)
        "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
        "ancestorsize" : n,     (numeric) virtual transaction size of in-mempool ancestors (including this one)
        "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one) (DEPRECATED)
        "wtxid" : hash,         (string) hash of serialized transaction, including witness data
        "fees" : {
            "base" : n,         (numeric) transaction fee in QTUM
            "modified" : n,     (numeric) transaction fee with fee deltas used for mining priority in QTUM
            "ancestor" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one) in QTUM
            "descendant" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one) in QTUM
        }
        "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
            "transactionid",    (string) parent transaction id
           ... ]
        "spentby" : [           (array) unconfirmed transactions spending outputs from this transaction
            "transactionid",    (string) child transaction id
           ... ]
      }, ...
    }
    
**Examples:**

    > qtum-cli getmempoolancestors "mytxid"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolancestors", "params": ["mytxid"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getmempoolancestors a957d309824b760814feb6426ba386d082f3b8bc95837e3e7ebada6538cf7e2c     

**Test result:**
   
    [
      "c3d044940534fd94fd0c901a895f62505e7beba0dfa44b1563c7aea980279135"     
    ]

### getmempooldescendants

If txid is in the mempool, returns all in-mempool descendants.

**Arguments:**

    1. "txid"   (string, required) The transaction id (must be in mempool)
    2.  verbose (boolean, optional, default=false) True for a json object, false for array of transaction ids

**Result (for verbose = false):**

    [ 
      "transactionid" (string) The transaction id of an in-mempool descendant transaction
      ,...
    ]

**Result (for verbose=true):**

     {                           
      "transactionid" : {       
        "size" : n,             (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
        "fee" : n,              (numeric) transaction fee in QTUM (DEPRECATED)
        "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority (DEPRECATED)
        "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
        "height" : n,           (numeric) block height when transaction entered pool
        "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
        "descendantsize" : n,   (numeric) virtual transaction size of in-mempool descendants (including this one)
        "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one) (DEPRECATED)
        "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
        "ancestorsize" : n,     (numeric) virtual transaction size of in-mempool ancestors (including this one)
        "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one) (DEPRECATED)
        "wtxid" : hash,         (string) hash of serialized transaction, including witness data
        "fees" : {
            "base" : n,         (numeric) transaction fee in QTUM
            "modified" : n,     (numeric) transaction fee with fee deltas used for mining priority in QTUM
            "ancestor" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one) in QTUM
            "descendant" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one) in QTUM
        }
        "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
            "transactionid",    (string) parent transaction id
           ... ]
        "spentby" : [           (array) unconfirmed transactions spending outputs from this transaction
            "transactionid",    (string) child transaction id
           ... ]
      }, ...
    }
    
**Examples:**

    > qtum-cli getmempooldescendants "mytxid"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempooldescendants", "params": ["mytxid"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test result:**

    [
      "9d980a4fcdf13fb2c9a5c7769ad6f3e8668aba1f0608be09ef84a11afaf3d03f",
      "89874d6f44bb3b8a526c50cecda1cbe06c6c6e8107623b79222ee75b79f91d5a",
      "0c2d893fdc510a6fddb18fc3d441b02d5b6050b754dc6f5d5ddd251707c3d995"
    ]

### getmempoolentry

Returns mempool data for given transaction

**Arguments:**

    1. "txid" (string, required) The transaction id (must be in mempool)

**Result:**
  
    {                           
        "size" : n,             (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
        "fee" : n,              (numeric) transaction fee in QTUM (DEPRECATED)
        "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority (DEPRECATED)
        "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
        "height" : n,           (numeric) block height when transaction entered pool
        "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
        "descendantsize" : n,   (numeric) virtual transaction size of in-mempool descendants (including this one)
        "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one) (DEPRECATED)
        "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
        "ancestorsize" : n,     (numeric) virtual transaction size of in-mempool ancestors (including this one)
        "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one) (DEPRECATED)
        "wtxid" : hash,         (string) hash of serialized transaction, including witness data
        "fees" : {
            "base" : n,         (numeric) transaction fee in QTUM
            "modified" : n,     (numeric) transaction fee with fee deltas used for mining priority in QTUM
            "ancestor" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one) in QTUM
            "descendant" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one) in QTUM
        }
        "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
            "transactionid",    (string) parent transaction id
           ... ]
        "spentby" : [           (array) unconfirmed transactions spending outputs from this transaction
            "transactionid",    (string) child transaction id
           ... ]
    }

**Examples:**

    > qtum-cli getmempoolentry "mytxid"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolentry", "params": ["mytxid"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### getmempoolinfo

Returns details on the active state of the TX memory pool.

**Result:**

    {
      "size": xxxxx, (numeric) Current tx count  
      "bytes": xxxxx, (numeric) Sum of all virtual transaction sizes as defined in BIP 141. Differs from actual serialized size because witness data is discounted  
      "usage": xxxxx, (numeric) Total memory usage for the mempool  
      "maxmempool": xxxxx, (numeric) Maximum memory usage for the mempool  
      "mempoolminfee": xxxxx (numeric) Minimum fee rate in QTUM/kB for tx to be accepted. Is the maximum of minrelaytxfee and minimum mempool fee  
      "minrelaytxfee": xxxxx (numeric) Current minimum relay fee for transactions  
    }

**Examples:**

    > qtum-cli getmempoolinfo
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getmempoolinfo
    
**Test result:**

    {
      "size": 10,
      "bytes": 3582,
      "usage": 14176,
      "maxmempool": 300000000,
      "mempoolminfee": 0.00400000,
      "minrelaytxfee": 0.00400000
    }

###  getrawmempool

Returns all transaction ids in memory pool as a json array of string transaction ids.

Hint: use getmempoolentry to fetch a specific transaction from the mempool.

**Arguments:**

    1. verbose (boolean, optional, default=false) True for a json object, false for array of transaction ids

**Result: (for verbose = false):**

    {                           
      "transactionid" : {       
        "size" : n,             (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
        "fee" : n,              (numeric) transaction fee in QTUM (DEPRECATED)
        "modifiedfee" : n,      (numeric) transaction fee with fee deltas used for mining priority (DEPRECATED)
        "time" : n,             (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
        "height" : n,           (numeric) block height when transaction entered pool
        "descendantcount" : n,  (numeric) number of in-mempool descendant transactions (including this one)
        "descendantsize" : n,   (numeric) virtual transaction size of in-mempool descendants (including this one)
        "descendantfees" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one) (DEPRECATED)
        "ancestorcount" : n,    (numeric) number of in-mempool ancestor transactions (including this one)
        "ancestorsize" : n,     (numeric) virtual transaction size of in-mempool ancestors (including this one)
        "ancestorfees" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one) (DEPRECATED)
        "wtxid" : hash,         (string) hash of serialized transaction, including witness data
        "fees" : {
            "base" : n,         (numeric) transaction fee in QTUM
            "modified" : n,     (numeric) transaction fee with fee deltas used for mining priority in QTUM
            "ancestor" : n,     (numeric) modified fees (see above) of in-mempool ancestors (including this one) in QTUM
            "descendant" : n,   (numeric) modified fees (see above) of in-mempool descendants (including this one) in QTUM
        }
        "depends" : [           (array) unconfirmed transactions used as inputs for this transaction
            "transactionid",    (string) parent transaction id
           ... ]
        "spentby" : [           (array) unconfirmed transactions spending outputs from this transaction
            "transactionid",    (string) child transaction id
           ... ]
      }, ...
    }

**Examples:**

    > qtum-cli getrawmempool true
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawmempool", "params": [true] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:** 

    ./qtum-cli getrawmempool
    
**Test result:**
 
    [
      "d4e995b2e0b5ef44f90659323e662f408f7938b5b97c345a40192ca6d0b06704",
      "9e41daae52ece96732305cb0873b8528e7011c866eb7c3c9bee2c22c03e5bf65",
      "354297aef68f48044af17c3f01616597dad298304e34728fa9894b3ff73a0f33",
      "e2c407e5468a3e885b73760e3c6115d6d493786fff5ec070e91ad9b4db58b2ef",
      "15f9f80b536041ebf5c3958c7b7d9bab72c800882235fc782925137c2addbdd2",
      "109483b1b06746cf4215f3786907b26213adc71a14145acccbba4f0952a751a3",
      "b49e03dd14a242803bf8108a10a9f82120e21e7d4b0a9255c632e7b92d879136",
      "40a295fa44931750c048feb817fad96e079ce193c4eda0770d68be6c1f7241c3",
      "f1e4f8814a404adce808e9b0aed56f61ec151c745cba3a6ac1f0a917884adb59",
      "b6772f160e21c4633f95b1c5831c6d0451cab1501c375730ea32de64860f1809",
      "65894a5fcf0e19e13375ba0d0f2afa6e73f52512bc69cf8225c40af824f740d9",
      "8199c4f6c9f8be79fff4fc9664755bc0502de92d9856083112e55caaa2cb1974",
      "c3fb5ef13f87f2988c879c274cfbc1613240a12a66e9259388101d82364f1934",
      "ca78e53edcfba07d4eee2a1bbfc07e26e79e5677104399c794e51d098c735056",
      "7f66e7f6443ebd0d3a3a8e6bd83e3a5ffc6d32ef5a1ee6487c7abb5cfae7d409",
      "97966a9f3baeac334cb547d553baf71bf7c68720f350444d7411e0855f39a574",
      "78285303f6deef553cd5fcd5084db0bae3ccf504ac66f614cb29a5a6f6b5e815",
      "e5ae989b9782c1afd2c6f71379e46d162ffbe804c5b8db70b7bc85d939df2efe",
      "2f09732e25eab121a347471a91be55c798cde96aa7f8009da51c2a2d322e6410",
      "c302d3177a64a4a3c7f2ba1ea196b69754475192afa8249eb18f6f055556c8e1",
      "7f1de19f02347ea3744bcb11364c9883b91e4f4883b13f15e9e9f52595c1d3d6",
      "c241f5896723fec65b3af4f94491679ae8a79c434b2e0749651cf416952abac0",
      "4d8932af7a7073e2c4a5527767215f7bf5b8c7759a5b49d976f0031d5184fd18"
    ]


### getstorage

Get data stored by smart contracts

**Argument:**

     1. "address"  (string, required) The address to get the storage from
     2. "blockNum" (string, optional) Number of block to get state from,  "latest" keyword supported. Latest if not passed.
     3. "index"    (number, optional) Zero-based index position of the storage 

**Examples:**

    > qtum-cli getstorage “contract address”
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getstorage", "params": ["address"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    getstorage "fdb9d0873ba524ef3ea67c1719666968e1eeb110"

**Test result:**

    {
      "000756ed9982214a7ba55dbe32d0321f5891e75d3c3c467d4b575d55991e03b1": 
      {
        "52adc13b5e472402f13052709f282024cc52e564f96b2183a5737c545229228d": "0000000000000000000000000000000000000000000000000000000000000001"
      },
    }

### gettransactionreceipt

requires -logevents to be enabled

**Argument:**

    1. "hash" (string, required) The contract transaction hash

**Result:**
    
    {
      "blockHash":  "XXX"        (String), 32 bytes, the blockhash included this tx.
      "blockNumber": n           (Number), the blocknumber included this transaction.
      "transaction": "XXX":      (String), 32 bytes，the hash of this transaction.
      "transactionIndex": n      (numberic), the index in the block for this tx.
      "from": "XXX"              (String), 20 bytes，the sender address of this tx.
      "to"  : "XXXX"             (String), 20 bytes，the receiver address of this tx. if this  address is created by a contract,return null. 
      "cumulativeGasUsed": n     (numberic), The total amount of gas used after execution of the current transaction
      "gasUsed": n (numberic), The gas cost alone to execute the current transaction。
      "contractAddress": "XXX"   (String), 20 bytes，the created contract address.
       if this tx is created by the contract, return the contract address. else return null.
      "logs": []
    }

**Test result:**

    [
      {
        "blockHash": "1e34edb316f9c442d1db71ad5bd5376650387c6deb275c63c459b6624880180b",
        "blockNumber": 196529,
        "transactionHash": "acccfb57aaeb94127560f4762d5372af3dcb4faddf9de3b2ce6bde0fdd1d57d5",
        "transactionIndex": 2,
        "from": "83c2436854450b0895d4c1d965720ef5e6a125be",
        "to": "74045ec0dc26ec1861473828bc140ebc4c1f3eff",
        "cumulativeGasUsed": 23619,
        "gasUsed": 23619,
        "contractAddress": "74045ec0dc26ec1861473828bc140ebc4c1f3eff",
        "excepted": "None",
        "log": [
        ]
      }
    ]

### gettxout

Returns details about an unspent transaction output.

**Arguments:**

    1. "txid"            (string, required) The transaction id
    2. "n"               (numeric, required) vout number
    3. "include_mempool" (boolean, optional) Whether to include the mempool. Default: true. Note that an unspent output that is spent in the mempool won't appear.

**Result:**

    {
      "bestblock": "hash",    (string) The hash of the block at the tip of the chain
      "confirmations" : n,    (numeric) The number of confirmations
      "value" : x.xxx,        (numeric) The transaction value in QTUM
      "scriptPubKey" : 
      { 
        "asm" : "code",       (string)
        "hex" : "hex",        (string)
        "reqSigs" : n,        (numeric) Number of required signatures
        "type" : "pubkeyhash",(string) The type, eg pubkeyhash
        "addresses" : [ (array of string) array of qtum addresses
        "address"             (string) qtum address
        ,...
        ]
       },
      "coinbase" : true|false (boolean) Coinbase or not
    }

**Examples:**

Get unspent transactions

    > qtum-cli listunspent

View the details

    > qtum-cli gettxout "txid" 1

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxout", "params": ["txid", 1] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### gettxoutproof

Returns a hex-encoded proof that "txid" was included in a block.

NOTE: By default this function only works sometimes. This is when there is an
unspent output in the utxo for this transaction. To make it always work,
you need to maintain a transaction index, using the -txindex command line option or
specify the block in which the transaction is included manually (by blockhash).

**Arguments:**

    1. "txids" (string,required) A json array of txids to filter
      [
        "txid" (string) A transaction hash
        ,...
      ]
    2. "blockhash" (string, optional) If specified, looks for txid in the block with this hash

**Result:**

    "data" (string) A string that is a serialized, hex-encoded data for the proof.

**Test example:** 

    ./qtum-cli gettxoutproof [\"5caa24c8c78f441a5c37dff602cdacc27b4530b03c09569f62dc3cd20e674918\"]

**Test result:**

    0000002081d3145a457b724b725171603a991b8d8186f0506c65722e436a6a33d039690ed689a1e4bdea746f8a3c47d6856765282fb5f7f20c9c43cc9e0170b6ba1214076010135d8683001b0000000052ef386ec7ae80719e408c3ea4193583bd0665fffd633d5e10b19e26375ac9b6386faa7484bfd98fc4789fd584229d5c20f72f772a8b3024ea94d1563e84e964b7e989413b1f509a5c14f24dadcf6da7e4f9e8559e5f6ff185cbc978fa1693fc0100000046304402205c0fbeff48e49b24848fba7428ea1c821ef4942135d60f51f6a4260e76941ac5022012a051fc518ec6b684a49eaf75631cdfa5574b170ccab6a0612da44585eab5600300000002fc77727661996828f410e89871d981a1c37f951d35d4ed196745d348cc74ca611849670ed23cdc629f56093cb030457bc2accd02f6df375c1a448fc7c824aa5c010d

### gettxoutsetinfo

Returns statistics about the unspent transaction output set.
Note this call may take some time.

**Result:**

    {
      "height":n,                  (numeric) The current block height (index)
      "bestblock": "hex",          (string) The hash of the block at the tip of the chain
      "transactions": n,           (numeric) The number of transactions with unspent outputs
      "txouts": n,                 (numeric) The number of unspent transaction outputs
      "bogosize": n,               (numeric) A meaningless metric for UTXO set size
      "hash_serialized_2": "hash", (string) The serialized hash
      "disk_size": n,              (numeric) The estimated size of the chainstate on disk
      "total_amount": x.xxx        (numeric) The total amount
    }

**Examples:**

    > qtum-cli gettxoutsetinfo
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxoutsetinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### listcontracts 

list all the contracts and default accounts is 20

**Argument:**

    1. start (numeric or string, optional) The starting account index, default 1
    2. maxDisplay (numeric or string, optional) Max accounts to list, default 20

**Test example:**

    > ./qtum-cli listcontracts 1 5

**Result:**

     {
      "82155d35dc1e0b5dc3d6ca7e536af42394a7003c": 0.00000000,
      "c50116ca622b4dbd12205fb9cc61a64f7b63cb8a": 0.00000000,
      "28d1140499604664be0037272eb287e1742dcafe": 0.00000000,
      "b9fe4ba102c33ba078d90a2cb6fe8fa94fd114a1": 0.00000000,
      "954999d28fd46c6de806f9587a82321437771ab2": 0.00000000
    }

### preciousblock

Treats a block as if it were received before others with the same work.

A later preciousblock call can override the effect of an earlier one.

The effects of preciousblock are not retained across restarts.

**Arguments:**

    1. "blockhash" (string, required) the hash of the block to mark as precious
    
**Examples:**

    > qtum-cli preciousblock "blockhash"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "preciousblock", "params": ["blockhash"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### pruneblockchain

 prune the spend tx to reduce the size of the block
 
**Arguments:**

    1. "height" (numeric, required) The block height to prune up to. May be set to a discrete height, or a unix timestamp to prune blocks whose block time is at least 2 hours older than the provided timestamp.

**Result:**

    n (numeric) Height of the last block pruned.

**Examples:**

    > qtum-cli pruneblockchain 1000
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "pruneblockchain", "params": [1000] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### savemempool

Dumps the mempool to disk. It will fail until the previous dump is fully loaded.

**Examples:**

    > qtum-cli savemempool
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "savemempool", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
### scantxoutset

EXPERIMENTAL warning: this call may be removed or changed in future releases.

Scans the unspent transaction output set for entries that match certain output descriptors.
Examples of output descriptors are:
addr(<addess>) Outputs whose scriptPubKey corresponds to the specified address (does not include P2PK)
raw(<hex script>) Outputs whose scriptPubKey equals the specified hex scripts
combo(<pubkey>) P2PK, P2PKH, P2WPKH, and P2SH-P2WPKH outputs for the given pubkey pkh(<pubkey>) P2PKH outputs for the given pubkey
sh(multi(<n>,<pubkey>,<pubkey>,...)) P2SH-multisig outputs for the given threshold and pubkeys

In the above, <pubkey> either refers to a fixed public key in hexadecimal notation, or to an xpub/xprv optionally followed by one
or more path elements separated by "/", and optionally ending in "/*" (unhardened), or "/*'" or "/*h" (hardened) to specify all
unhardened or hardened child keys.
In the latter case, a range needs to be specified by below if different from 1000.
For more information on output descriptors, see the documentation in the doc/descriptors.md file.

**Arguments:**

    1. "action"                       (string, required) The action to execute
                                          "start" for starting a scan
                                          "abort" for aborting the current scan (returns true when abort was successful)
                                          "status" for progress report (in %) of the current scan
    2. "scanobjects"                  (array, required) Array of scan objects
        [                             Every scan object is either a string descriptor or an object:
            "descriptor",             (string, optional) An output descriptor
            {                         (object, optional) An object with output descriptor and metadata
              "desc": "descriptor",   (string, required) An output descriptor
              "range": n,             (numeric, optional) Up to what child index HD chains should be explored (default: 1000)
            },
            ...
        ]

**Result:**

     {
      "unspents": [
        {
        "txid" : "transactionid",     (string) The transaction id
        "vout": n,                    (numeric) the vout value
        "scriptPubKey" : "script",    (string) the script key
        "amount" : x.xxx,             (numeric) The total amount in QTUM of the unspent output
        "height" : n,                 (numeric) Height of the unspent transaction output
       }
       ,...], 
     "total_amount" : x.xxx,          (numeric) The total amount of all found unspent outputs in QTUM
    ] 

### searchlogs

requires -logevents to be enabled

**Arguments:**

    1. "fromBlock"        (numeric, required) The number of the earliest block (latest may be given to mean the most recent block).
    2. "toBlock"          (string, required) The number of the latest block (-1 may be given to mean the most recent block).
    3. "address"          (string, optional) An address or a list of addresses to only get logs from particular account(s).
    4. "topics"           (string, optional) An array of values from which at least one must appear in the log entries. The order is important, if you want to leave topics out use null, e.g. ["null", "0x00..."]. 
    5. "minconf"          (uint, optional, default=0) Minimal number of confirmations before a log is returned

**Examples:**

    > qtum-cli searchlogs 0 100 '{"addresses": ["12ae42729af478ca92c8c66773a3e32115717be4"]}' '{"topics": ["null","b436c2bf863ccd7b8f63171201efd4792066b4ce8e543dde9c3e9e9ab98e216c"]}'
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "searchlogs", "params": [0 100 {"addresses": ["12ae42729af478ca92c8c66773a3e32115717be4"]} {"topics": ["null","b436c2bf863ccd7b8f63171201efd4792066b4ce8e543dde9c3e9e9ab98e216c"]}] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### verifychain

Verifies blockchain database.

**Arguments:**

    1. checklevel (numeric, optional, 0-4, default=3) How thorough the block verification is.
    2. nblocks    (numeric, optional, default=6, 0=all) The number of blocks to check.

 **Result:**

    true|false (boolean) Verified or not

**Examples:**

    > qtum-cli verifychain
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifychain", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### verifytxoutproof 

Verifies that a proof points to a transaction in a block, returning the transaction it commits to and throwing an RPC error if the block is not in our best chain

**Arguments:**

    1. "proof" (string, required) The hex-encoded proof generated by gettxoutproof

**Result:**

    ["txid"] (array, strings) The txid(s) which the proof commits to, or empty array if the proof can not be validated.
    
**Test example:**

    verifytxoutproof "0000002081d3145a457b724b725171603a991b8d8186f0506c65722e436a6a33d039690ed689a1e4bdea746f8a3c47d6856765282fb5f7f20c9c43cc9e0170b6ba1214076010135d8683001b0000000052ef386ec7ae80719e408c3ea4193583bd0665fffd633d5e10b19e26375ac9b6386faa7484bfd98fc4789fd584229d5c20f72f772a8b3024ea94d1563e84e964b7e989413b1f509a5c14f24dadcf6da7e4f9e8559e5f6ff185cbc978fa1693fc0100000046304402205c0fbeff48e49b24848fba7428ea1c821ef4942135d60f51f6a4260e76941ac5022012a051fc518ec6b684a49eaf75631cdfa5574b170ccab6a0612da44585eab5600300000002fc77727661996828f410e89871d981a1c37f951d35d4ed196745d348cc74ca611849670ed23cdc629f56093cb030457bc2accd02f6df375c1a448fc7c824aa5c010d"

**Test result:**

    [
      "5caa24c8c78f441a5c37dff602cdacc27b4530b03c09569f62dc3cd20e674918"
    ]

###  waitforlogs 

waitforlogs (fromBlock) (toBlock) (filter) (minconf)
requires -logevents to be enabled

Waits for a new logs and return matching log entries. When the call returns, it also specifies the next block number to start waiting for new logs.
By calling waitforlogs repeatedly using the returned `nextBlock` number, a client can receive a stream of up-to-date log entires.

This call is different from the similarly named `waitforlogs`. This call returns individual matching log entries, `searchlogs` returns a transaction receipt if one of the log entries of that transaction matches the filter conditions.

**Arguments:**

    1. fromBlock (int | "latest", optional, default=null) The block number to start looking for logs. ()
    2. toBlock   (int | "latest", optional, default=null) The block number to stop looking for logs. If null, will wait indefinitely into the future.
    3. filter    ({ addresses?: Hex160String[], topics?: Hex256String[] }, optional default={}) Filter conditions for logs. Addresses and topics are specified as array of hexadecimal strings
    4. minconf   (uint, optional, default=6) Minimal number of confirmations before a log is returned

**Result:**

    An object with the following properties:
    1. logs (LogEntry[]) Array of matchiing log entries. This may be empty if `filter` removed all entries.2. count (int) How many log entries are returned.3. nextBlock (int) To wait for new log entries haven't seen before, use this number as `fromBlock`
    Usage:
    `waitforlogs` waits for new logs, starting from the tip of the chain.
    `waitforlogs 600` waits for new logs, but starting from block 600. If there are logs available, this call will return immediately.
    `waitforlogs 600 700` waits for new logs, but only up to 700th block
    `waitforlogs null null` this is equivalent to `waitforlogs`, using default parameter values
    `waitforlogs null null` { "addresses": [ "ff0011..." ], "topics": [ "c0fefe"] }` waits for logs in the future matching the specified conditions

**Sample Output:**

    {
      "entries": [
        {
          "blockHash": "56d5f1f5ec239ef9c822d9ed600fe9aa63727071770ac7c0eabfc903bf7316d4",
          "blockNumber": 3286,
          "transactionHash": "00aa0f041ce333bc3a855b2cba03c41427cda04f0334d7f6cb0acad62f338ddc",
          "transactionIndex": 2,
          "from": "3f6866e2b59121ada1ddfc8edc84a92d9655675f",
          "to": "8e1ee0b38b719abe8fa984c986eabb5bb5071b6b",
          "cumulativeGasUsed": 23709,
          "gasUsed": 23709,
          "contractAddress": "8e1ee0b38b719abe8fa984c986eabb5bb5071b6b",
          "topics": [
            "f0e1159fa6dc12bb31e0098b7a1270c2bd50e760522991c6f0119160028d9916",
            "0000000000000000000000000000000000000000000000000000000000000002"
          ],
          "data": "00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000003"
        }
      ],
    
      "count": 7,
      "nextblock": 801
    }

## Control 

###  echo

echo|echojson "message" ...

Simply echo back the input arguments. This command is for testing.

The difference between echo and echojson is that echojson has argument conversion enabled in the client-side table inqtum-cli and the GUI. There is no server-side difference.

### getmemoryinfo

Returns an object containing information about memory usage.

**Arguments:**

    1. "mode" determines what kind of information is returned. This argument is optional, the default mode is "stats".
      - "stats" returns general statistics about memory usage in the daemon.
      - "mallocinfo" returns an XML string describing low-level heap state (only available if compiled with glibc 2.10+).

**Result (mode "stats"):**

    {
      "locked": {               (json object) Information about locked memory manager
        "used": xxxxx,          (numeric) Number of bytes used
        "free": xxxxx,          (numeric) Number of bytes available in current arenas
        "total": xxxxxxx,       (numeric) Total number of bytes managed
        "locked": xxxxxx,       (numeric) Amount of bytes that succeeded locking. If this number is smaller than total, locking pages failed at some point and key data could be swapped to disk.
        "chunks_used": xxxxx,   (numeric) Number allocated chunks
        "chunks_free": xxxxx,   (numeric) Number unused chunks
      }
    }

**Result (mode "mallocinfo"):**

    "<malloc version="1">..."

**Examples:**

    > qtum-cli getmemoryinfo 
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmemoryinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### help

List all commands, or get help for a specified command.

**Arguments:**

    1. "command"     (string, optional) The command to get help on

**Result:**

    "text"     (string) The help text

### logging

Gets and sets the logging configuration.

When called without an argument, returns the list of categories with status that are currently being debug logged or not.

When called with arguments, adds or removes categories from debug logging and return the lists above.
The arguments are evaluated in order "include", "exclude".

If an item is both included and excluded, it will thus end up being excluded.

The valid logging categories are: net, tor, mempool, http, bench, zmq, db, rpc, estimatefee, addrman, selectcoins, reindex, cmpctblock, rand, prune, proxy, mempoolrej, libevent, coindb, qt, leveldb, coinstake, http-poll.

In addition, the following are available as category names with special meanings:
  - "all",  "1" : represent all logging categories.
  - "none", "0" : even if other logging categories are specified, ignore all of them.

**Arguments:**

    1. "include"        (array of strings, optional) A json array of categories to add debug logging
         [
           "category"   (string) the valid logging category
           ,...
         ]
    2. "exclude"        (array of strings, optional) A json array of categories to remove debug logging
         [
           "category"   (string) the valid logging category
           ,...
         ]

**Result:**

    {                  
      "category": 0|1,  (numeric) if being debug logged or not. 0:inactive, 1:active
      ...
    }

**Examples:**

    > qtum-cli logging "[\"all\"]" "[\"http\"]"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "logging", "params": [["all"], "[libevent]"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### stop

Stop Qtum server.

### uptime

Returns the total uptime of the server.

**Result:**

`ttt (numeric) The number of seconds that the server has been runnin`g

**Examples:**

    > qtum-cli uptime
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "uptime", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
## Generating

### generate 

Mine up to nblocks blocks immediately (before the RPC call returns) to an address in the wallet.

**Arguments:**

    1. nblocks  (numeric, required) How many blocks are generated immediately.
    2. maxtries (numeric, optional) How many iterations to try (default = 1000000).

**Result:**

    [ blockhashes ] (array) hashes of blocks generated

**Examples:**

 Generate 11 blocks
  
     > qtum-cli generate 11

### generatetoaddress

Mine blocks immediately to a specified address (before the RPC call returns)

**Arguments:**

    1. nblocks  (numeric, required) How many blocks are generated immediately.
    2. address  (string, required) The address to send the newly generated qtum to.
    3. maxtries (numeric, optional) How many iterations to try (default = 1000000).

**Result:**

    [ blockhashes ] (array) hashes of blocks generated

**Examples:**

    Generate 11 blocks to myaddress

    > qtum-cli generatetoaddress 11 "myaddress"

## Mining

### getblocktemplate 

If the request parameters include a 'mode' key, that is used to explicitly select between the default 'template' request or a 'proposal'.
It returns data needed to construct a block to work on.
For full specification, see BIPs 22, 23, 9, and 145:
https://github.com/bitcoin/bips/blob/master/bip-0022.mediawiki
https://github.com/bitcoin/bips/blob/master/bip-0023.mediawiki
https://github.com/bitcoin/bips/blob/master/bip-0009.mediawiki#getblocktemplate_changes
https://github.com/bitcoin/bips/blob/master/bip-0145.mediawiki

**Arguments:**

    1. template_request (json object, optional) A json object in the following spec
    {
      "mode":"template" (string, optional) This must be set to "template", "proposal" (see BIP 23), or omitted
      "capabilities":[ (array, optional) A list of strings
      "support" (string) client side supported feature, 'longpoll', 'coinbasetxn', 'coinbasevalue', 'proposal', 'serverlist', 'workid'
       ,...
        ],
      "rules":
     [ 
        (array, optional) A list of strings
        "support" (string) client side supported softfork deployment
        ,...
      ]
    }

**Result:**

    {
      "version" : n,                    (numeric) The preferred block version
      "rules" : [ "rulename", ... ],    (array of strings) specific block rules that are to be enforced
      "vbavailable" : {                 (json object) set of pending, supported versionbit (BIP 9) softfork deployments
          "rulename" : bitnumber          (numeric) identifies the bit number as indicating acceptance and readiness for the named softfork rule
          ,...
      },
      "vbrequired" : n,                 (numeric) bit mask of versionbits the server requires set in submissions
      "previousblockhash" : "xxxx",     (string) The hash of current highest block
      "transactions" : [                (array) contents of non-coinbase transactions that should be included in the next block
          {
             "data" : "xxxx",             (string) transaction data encoded in hexadecimal (byte-for-byte)
             "txid" : "xxxx",             (string) transaction id encoded in little-endian hexadecimal
             "hash" : "xxxx",             (string) hash encoded in little-endian hexadecimal (including witness data)
             "depends" : [                (array) array of numbers 
                 n                          (numeric) transactions before this one (by 1-based index in 'transactions' list) that must be present in the final block if this one is
                 ,...
             ],
             "fee": n,                    (numeric) difference in value between transaction inputs and outputs (in satoshis); for coinbase transactions, this is a negative Number of the total collected block fees (ie, not including the block subsidy); if key is not present, fee is unknown and clients MUST NOT assume there isn't one
             "sigops" : n,                (numeric) total SigOps cost, as counted for purposes of block limits; if key is not present, sigop cost is unknown and clients MUST NOT assume it is zero
             "weight" : n,                (numeric) total transaction weight, as counted for purposes of block limits
          }
          ,...
      ],
      "coinbaseaux" : {                 (json object) data that should be included in the coinbase's scriptSig content
          "flags" : "xx"                  (string) key name is to be ignored, and value included in scriptSig
      },
      "coinbasevalue" : n,              (numeric) maximum allowable input to coinbase transaction, including the generation award and transaction fees (in satoshis)
      "coinbasetxn" : { ... },          (json object) information for coinbase transaction
      "target" : "xxxx",                (string) The hash target
      "mintime" : xxx,                  (numeric) The minimum timestamp appropriate for next block time in seconds since epoch (Jan 1 1970 GMT)
      "mutable" : [                     (array of string) list of ways the block template may be changed 
         "value"                          (string) A way the block template may be changed, e.g. 'time', 'transactions', 'prevblock'
         ,...
      ],
      "noncerange" : "00000000ffffffff",(string) A range of valid nonces
      "sigoplimit" : n,                 (numeric) limit of sigops in blocks
      "sizelimit" : n,                  (numeric) limit of block size
      "weightlimit" : n,                (numeric) limit of block weight
      "curtime" : ttt,                  (numeric) current timestamp in seconds since epoch (Jan 1 1970 GMT)
      "bits" : "xxxxxxxx",              (string) compressed target of next block
      "height" : n                      (numeric) The height of the next block
    }    

### getmininginfo

Returns a json object containing mining-related information.

**Examples:**

     >qtum-cli getmininginfo  
     
     >curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmininginfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
     
**Result:**

    {
      "blocks": nnn,             (numeric) The current block
      "currentblockweight": nnn, (numeric) The last block weight
      "currentblocktx": nnn,     (numeric) The last block transaction
      "difficulty": xxx.xxxxx    (numeric) The current difficulty
      "networkhashps": nnn,      (numeric) The network hashes per second
      "pooledtx": n              (numeric) The size of the mempool
      "chain": "xxxx",           (string) current network name as defined in BIP70 (main, test, regtest)
      "warnings": "..."          (string) any network and blockchain warnings
    }
    
**Test example:**

    ./qtum-cli getmininginfo
    
**Test result:**
  
     {
      "blocks": 401661,
      "currentblockweight": 4000,
      "currentblocktx": 0,
      "difficulty": {
        "proof-of-work": 1.52587890625e-005,
        "proof-of-stake": 2798173.863126792,
        "search-interval": 0
      },
      "blockvalue": 400000000,
      "netmhashps": 0,
      "netstakeweight": 1335439448399970,
      "errors": "",
      "networkhashps": 76789015825010.86,
      "pooledtx": 2,
      "stakeweight": {
        "minimum": 568351000,
        "maximum": 0,
        "combined": 568351000
      },
      "chain": "main",
      "warnings": ""
    }

### getnetworkhashps

Returns the estimated network hashes per second based on the last n blocks (for PoW only).
Pass in [blocks] to override # of blocks, -1 specifies since last difficulty change.
Pass in [height] to estimate the network speed at the time when a certain block was found.

**Arguments:**

    1. nblocks (numeric, optional, default=120) The number of blocks, or -1 for blocks since last difficulty change.
    2. height  (numeric, optional, default=-1) To estimate at the time of the given height.

**Result:**

    x (numeric) Hashes per second estimated

**Examples:**

    > qtum-cli getnetworkhashps
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnetworkhashps", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
**Test result:**

    3.514351301619956e-008

### getstakinginfo

Returns an object containing staking-related information.

**Example:**

    ./qtum-cli getstakinginfo

**Result:**

    {
      "enabled": true or false,(bool),if HD key is enabled, the value if true,else is false.
      "staking": true or false,(bool),if wallet staking token or not.
      "errors": "XXX",         (string), any network and blockchain errors
      "currentblocktx": n,     (numberic),the last block transaction
      "pooledtx": n,           (numberic), The size of the mempool
      "difficulty": n,         (numberic),the current proof-of-work difficulty
      "search-interval": n,
      "weight": n,             (numberic), the total staking token number
      "netstakeweight": n,     (numberic), the total numbers of staking in the network
      "expectedtime": n,       (numberic), the time that to get the rights to cast the block
    }

**Test example:**

    ./qtum-cli getstakinginfo

**Test result:**

    {
      "enabled": true,
      "staking": false,
      "errors": "",
      "currentblocktx": 0,
      "pooledtx": 0,
      "difficulty": 4.656542373906925e-010,
      "search-interval": 0,
      "weight": 0,
      "netstakeweight": 0,
      "expectedtime": 0
    }

### getsubsidy 

Returns subsidy value for the specified value of target.

### prioritisetransaction

Accepts the transaction into mined blocks at a higher (or lower) priority

**Arguments:**

    1. "txid"         (string, required) The transaction id.
    2. dummy          (numeric, optional) API-Compatibility for previous API. Must be zero or null.
                      DEPRECATED. For forward compatibility use named arguments and omit this parameter.
    3. fee_delta      (numeric, required) The fee value (in satoshis) to add (or subtract, if negative).
                      Note, that this value is not a fee rate. It is a value to modify absolute fee of the TX.
                      The fee is not actually paid, only the algorithm for selecting transactions into a block
                      considers the transaction as it would have paid a higher (or lower) fee.

**Result:**

    true (boolean) Returns true

**Examples:**

    > qtum-cli prioritisetransaction "txid" 0.0 10000
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "prioritisetransaction", "params": ["txid", 0.0, 10000] }' -H 'content-type: text/plain;' http://127.0.0.1:3889

### submitblock

Attempts to submit new block to network.
See https://en.bitcoin.it/wiki/BIP_0022 for full specification.

**Arguments:**

    1. "hexdata" (string, required) the hex-encoded block data to submit
    2. "dummy" (optional) dummy value, for compatibility with BIP22. This value is ignored.
    
**Examples:**

    > qtum-cli submitblock "mydata"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "submitblock", "params": ["mydata"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
   
## Network

### addnode

Attempts to add or remove a node from the addnode list.
Or try a connection to a node once.
Nodes added using addnode (or -connect) are protected from DoS disconnection and are not required to be full nodes/support SegWit as other outbound peers are (though such peers will not be synced from).

**Arguments:**

    1. "node" (string, required) The node (see getpeerinfo for nodes)
    
    2. "command" (string, required) 'add' to add a node to the list, 'remove' to remove a node from the list, 'onetry' to try a connection to the node once

**Examples:**

    - Mainnet port 3888, Testnet port 13888, Regtest port 23888:
    
    > qtum-cli addnode "192.168.0.6:3888" "onetry"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "addnode", "params": ["192.168.0.6:3888", "onetry"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
### clearbanned

Clear all banned IPs.

**Examples:**

    > qtum-cli clearbanned
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "clearbanned", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### disconnectnode 

Immediately disconnects from the specified peer node.

Strictly one out of 'address' and 'nodeid' can be provided to identify the node.

To disconnect by nodeid, either set 'address' to the empty string, or call using the named 'nodeid' argument only.

**Arguments:**

    1. "address"     (string, optional) The IP address/port of the node
    2. "nodeid"      (number, optional) The node ID (see getpeerinfo for node IDs)

**Examples:** 

    - Mainnet port 3888, Testnet port 13888, Regtest port 23888:
    - 
    > qtum-cli disconnectnode "192.168.0.6:3888"
    
    > qtum-cli disconnectnode "" 1
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "disconnectnode", "params": ["192.168.0.6:3888"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "disconnectnode", "params": ["", 1] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### estimaterawfee

WARNING: This interface is unstable and may disappear or change!

WARNING: This is an advanced API call that is tightly coupled to the specific
implementation of fee estimation. The parameters it can be called with
and the results it returns will change if the internal implementation changes.

Estimates the approximate fee per kilobyte needed for a transaction to begin
confirmation within conf_target blocks if possible. Uses virtual transaction size as
defined in BIP 141 (witness data is discounted).

**Arguments:**

    1. conf_target (numeric) Confirmation target in blocks (1 - 1008)
    2. threshold   (numeric, optional) The proportion of transactions in a given feerate range that must have been
    confirmed within conf_target in order to consider those feerates as high enough and proceed to check
    lower buckets. Default: 0.95

**Result:**

    {
      "short" : {                 estimate for short time horizon
          "feerate" : x.x,        (numeric, optional) estimate fee rate in QTUM/kB
          "decay" : x.x,          (numeric) exponential decay (per block) for historical moving average of confirmation data
          "scale" : x,            (numeric) The resolution of confirmation targets at this time horizon
          "pass" : {              (json object, optional) information about the lowest range of feerates to succeed in meeting the threshold
              "startrange" : x.x,     (numeric) start of feerate range
              "endrange" : x.x,       (numeric) end of feerate range
              "withintarget" : x.x,   (numeric) number of txs over history horizon in the feerate range that were confirmed within target
              "totalconfirmed" : x.x, (numeric) number of txs over history horizon in the feerate range that were confirmed at any point
              "inmempool" : x.x,      (numeric) current number of txs in mempool in the feerate range unconfirmed for at least target blocks
              "leftmempool" : x.x,    (numeric) number of txs over history horizon in the feerate range that left mempool unconfirmed after target
          },
          "fail" : { ... },       (json object, optional) information about the highest range of feerates to fail to meet the threshold
          "errors":  [ str... ]   (json array of strings, optional) Errors encountered during processing
      },
      "medium" : { ... },    (json object, optional) estimate for medium time horizon
      "long" : { ... }       (json object) estimate for long time horizon
    }
    
    Results are returned for any horizon which tracks blocks up to the confirmation target.

**Example:**

    > qtum-cli estimaterawfee 6 0.9

### getaddednodeinfo

Returns information about the given added node, or all added nodes
(note that onetry addnodes are not listed here)

**Arguments:**

    1. "node" (string, optional) If provided, return information about this specific node, otherwise all nodes are returned.

**Result:**

     [
      {
        "addednode" : "192.168.0.201",          (string) The node IP address or name (as provided to addnode)
        "connected" : true|false,               (boolean) If connected
        "addresses" : [                         (list of objects) Only when connected = true
           {
             "address" : "192.168.0.201:3888",  (string) The qtum server IP and port we're connected to
             "connected" : "outbound"           (string) connection, inbound or outbound
           }
         ]
      }
      ,...
    ]
    
**Examples:**
 
    > qtum-cli getaddednodeinfo "192.168.0.201"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddednodeinfo", "params": ["192.168.0.201"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### getconnectioncount

Returns the number of connections to other nodes.

**Result:**

    n (numeric) The connection count

**Examples:**

    > qtum-cli getconnectioncount
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getconnectioncount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getconnectioncount

**Test result:**

    7

### getnettotals

Returns information about network traffic, including bytes in, bytes out,
and current time.

**Result:**

    {
      "totalbytesrecv": n,                     (numeric) Total bytes received
      "totalbytessent": n,                     (numeric) Total bytes sent
      "timemillis": t,                         (numeric) Current UNIX time in milliseconds
      "uploadtarget":
      {
        "timeframe": n,                        (numeric) Length of the measuring timeframe in seconds
        "target": n,                           (numeric) Target in bytes
        "target_reached": true|false,          (boolean) True if target is reached
        "serve_historical_blocks": true|false, (boolean) True if serving historical blocks
        "bytes_left_in_cycle": t,              (numeric) Bytes left in current time cycle
        "time_left_in_cycle": t                (numeric) Seconds left in current time cycle
      }
    }

**Examples:**

    > qtum-cli getnettotals
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnettotals", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### getnetworkinfo

Returns an object containing various state info regarding P2P networking.

**Result:**

    {
      "version": xxxxx,                      (numeric) the server version
      "subversion": "/Satoshi:x.x.x/",       (string) the server subversion string
      "protocolversion": xxxxx,              (numeric) the protocol version
      "localservices": "xxxxxxxxxxxxxxxx",   (string) the services we offer to the network
      "localrelay": true|false,              (bool) true if transaction relay is requested from peers
      "timeoffset": xxxxx,                   (numeric) the time offset
      "connections": xxxxx,                  (numeric) the number of connections
      "networkactive": true|false,           (bool) whether p2p networking is enabled
      "networks": [                          (array) information per network
      {
        "name": "xxx",                       (string) network (ipv4, ipv6 or onion)
        "limited": true|false,               (boolean) is the network limited using -onlynet?
        "reachable": true|false,             (boolean) is the network reachable?
        "proxy": "host:port"                 (string) the proxy that is used for this network, or empty if none
        "proxy_randomize_credentials": true|false,  (string) Whether randomized credentials are used
      }
      ,...
      ],
      "relayfee": x.xxxxxxxx,                (numeric) minimum relay fee for transactions in QTUM/kB
      "incrementalfee": x.xxxxxxxx,          (numeric) minimum fee increment for mempool limiting or BIP 125 replacement in QTUM/kB
      "localaddresses": [                    (array) list of local addresses
      {
        "address": "xxxx",                   (string) network address
        "port": xxx,                         (numeric) network port
        "score": xxx                         (numeric) relative score
      }
      ,...
      ]
      "warnings": "..."                      (string) any network and blockchain warnings
    }

**Examples:**

    > qtum-cli getnetworkinfo 
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnetworkinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### getpeerinfo

Returns data about each connected network node as a json array of objects.

**Result:**

    [
      {
        "id": n,                   (numeric) Peer index
        "addr":"host:port",        (string) The IP address and port of the peer
        "addrbind":"ip:port",      (string) Bind address of the connection to the peer
        "addrlocal":"ip:port",     (string) Local address as reported by the peer
        "services":"xxxxxxxxxxxxxxxx",   (string) The services offered
        "relaytxes":true|false,    (boolean) Whether peer has asked us to relay transactions to it
        "lastsend": ttt,           (numeric) The time in seconds since epoch (Jan 1 1970 GMT) of the last send
        "lastrecv": ttt,           (numeric) The time in seconds since epoch (Jan 1 1970 GMT) of the last receive
        "bytessent": n,            (numeric) The total bytes sent
        "bytesrecv": n,            (numeric) The total bytes received
        "conntime": ttt,           (numeric) The connection time in seconds since epoch (Jan 1 1970 GMT)
        "timeoffset": ttt,         (numeric) The time offset in seconds
        "pingtime": n,             (numeric) ping time (if available)
        "minping": n,              (numeric) minimum observed ping time (if any at all)
        "pingwait": n,             (numeric) ping wait (if non-zero)
        "version": v,              (numeric) The peer version, such as 70001
        "subver": "/Satoshi:0.8.5/",  (string) The string version
        "inbound": true|false,     (boolean) Inbound (true) or Outbound (false)
        "addnode": true|false,     (boolean) Whether connection was due to addnode/-connect or if it was an automatic/inbound connection
        "startingheight": n,       (numeric) The starting height (block) of the peer
        "banscore": n,             (numeric) The ban score
        "synced_headers": n,       (numeric) The last header we have in common with this peer
        "synced_blocks": n,        (numeric) The last block we have in common with this peer
        "inflight": [
           n,                      (numeric) The heights of blocks we're currently asking from this peer
           ...
        ],
        "whitelisted": true|false, (boolean) Whether the peer is whitelisted
        "bytessent_per_msg": {
           "addr": n,              (numeric) The total bytes sent aggregated by message type
           ...
        },
        "bytesrecv_per_msg": {
           "addr": n,              (numeric) The total bytes received aggregated by message type
           ...
        }
      }
      ,...
    ]

**Examples:**

    > qtum-cli getpeerinfo
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getpeerinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
**Test example:**

    ./qtum-cli getpeerinfo
    
**Test result:**：
  
     {
        "id": 1479,
        "addr": "171.96.72.225:63736",
        "addrlocal": "59.46.230.210:3888",
        "addrbind": "59.46.230.210:3888",
        "services": "000000000000000d",
        "relaytxes": true,
        "lastsend": 1562045310,
        "lastrecv": 1562045263,
        "bytessent": 405234,
        "bytesrecv": 404534,
        "conntime": 1561978028,
        "timeoffset": -2,
        "pingtime": 0.609372,
        "minping": 0.140614,
        "version": 70016,
        "subver": "/Satoshi:0.14.16/",
        "inbound": true,
        "addnode": false,
        "startingheight": 401184,
        "banscore": 0,
        "synced_headers": 401655,
        "synced_blocks": 401650,
        "inflight": [
        ],
        "whitelisted": false,
        "bytessent_per_msg": {
          "addr": 40437,
          "blocktxn": 21843,
          "cmpctblock": 77441,
          "feefilter": 32,
          "getblocktxn": 58,
          "getdata": 13753,
          "getheaders": 1021,
          "headers": 63150,
          "inv": 58072,
          "notfound": 61,
          "ping": 17952,
          "pong": 17952,
          "reject": 78,
          "sendcmpct": 132,
          "sendheaders": 24,
          "tx": 93042,
          "verack": 24,
          "version": 162
        },
        "bytesrecv_per_msg": {
          "addr": 11595,
          "blocktxn": 16722,
          "cmpctblock": 4544,
          "feefilter": 32,
          "getaddr": 24,
          "getblocktxn": 2146,
          "getdata": 14398,
          "getheaders": 1021,
          "headers": 101655,
          "inv": 97978,
          "notfound": 10071,
          "ping": 17952,
          "pong": 17952,
          "reject": 140,
          "sendcmpct": 1320,
          "sendheaders": 24,
          "tx": 106809,
          "verack": 24,
          "version": 127
        },...
      }

### listbanned

List all banned IPs/Subnets.

**Examples:**

    > qtum-cli listbanned
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listbanned", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### ping

Requests that a ping be sent to all other nodes, to measure ping time.
Results provided in getpeerinfo, pingtime and pingwait fields are decimal seconds.
Ping command is handled in queue with all other commands, so it measures processing backlog, not just network ping.

**Examples:**

    > qtum-cli ping
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "ping", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### setban

setban "subnet" "add|remove" (bantime) (absolute)

Attempts to add or remove an IP/Subnet from the banned list.

**Arguments:**

    1. "subnet"       (string, required) The IP/Subnet (see getpeerinfo for nodes IP) with an optional netmask (default is /32 = single IP)
    2. "command"      (string, required) 'add' to add an IP/Subnet to the list, 'remove' to remove an IP/Subnet from the list
    3. "bantime"      (numeric, optional) time in seconds how long (or until when if [absolute] is set) the IP is banned (0 or empty means using the default time of 24h which can also be overwritten by the -bantime startup argument)
    4. "absolute"     (boolean, optional) If set, the bantime must be an absolute timestamp in seconds since epoch (Jan 1 1970 GMT)

**Examples:**

    > qtum-cli setban "192.168.0.6" "add" 86400
    
    > qtum-cli setban "192.168.0.0/24" "add"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setban", "params": ["192.168.0.6", "add", 86400] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### setnetworkactive 

Disable/enable all p2p network activity.

**Arguments:**

    1. "state" (boolean, required) true to enable networking, false to disable

## Rawtransactions

### combinepsbt 

Combine multiple partially signed Qtum transactions into one transaction.
Implements the Combiner role.

**Arguments:**

    1. "txs" (string) A json array of base64 strings of partially signed transactions
    [
      "psbt" (string) A base64 string of a PSBT
      ,...
    ]

**Result:**

    "psbt" (string) The base64-encoded partially signed transaction

**Examples:**

    > qtum-cli combinepsbt ["mybase64_1", "mybase64_2", "mybase64_3"]

### combinerawtransaction 

Combine multiple partially signed transactions into one transaction.
The combined transaction may be another partially signed transaction or a
fully signed transaction.

**Arguments:**

    1. "txs" (string) A json array of hex strings of partially signed transactions
    [
      "hexstring" (string) A transaction hash
      ,...
    ]

**Result:**

    "hex" (string) The hex-encoded raw transaction with signature(s)

**Examples:**

    > qtum-cli combinerawtransaction ["myhex1", "myhex2", "myhex3"]

### converttopsbt 

Converts a network serialized transaction to a PSBT. This should be used only with createrawtransaction and fundrawtransaction
createpsbt and walletcreatefundedpsbt should be used for new applications.

**Arguments:**

    1. "hexstring"   (string, required) The hex string of a raw transaction
    2. permitsigdata (boolean, optional, default=false) If true, any signatures in the input will be discarded and conversion.
    will continue. If false, RPC will fail if any signatures are present.
    3. iswitness     (boolean, optional) Whether the transaction hex is a serialized witness transaction.
    If iswitness is not present, heuristic tests will be used in decoding. If true, only witness deserializaion
    will be tried. If false, only non-witness deserialization wil be tried. Only has an effect if
    permitsigdata is true.

**Result:**

    "psbt" (string) The resulting raw transaction (base64-encoded string)

**Examples:**

Create a transaction

    > qtum-cli createrawtransaction "[{\"txid\":\"myid\",\"vout\":0}]" "[{\"data\":\"00010203\"}]"

Convert the transaction to a PSBT

    > qtum-cli converttopsbt "rawtransaction"

### createpsbt 

Creates a transaction in the Partially Signed Transaction format.
Implements the Creator role.

**Arguments:**

    1. "inputs"           (array, required) A json array of json objects
    [
      {
        "txid":"id",      (string, required) The transaction id
        "vout":n,         (numeric, required) The output number
        "sequence":n      (numeric, optional) The sequence number
      }
      ,...
    ]
    2. "outputs"          (array, required) a json array with outputs (key-value pairs), where none of the keys are duplicated.
    That is, each address can only appear once and there can only be one 'data' object.
    [
      {
        "address": x.xxx, (obj, optional) A key-value pair. The key (string) is the qtum address, the value (float or string) is the amount in QTUM
      },
      {
        "data": "hex"     (obj, optional) A key-value pair. The key must be "data", the value is hex encoded data
      },... 
      More key-value pairs of the above form. For compatibility reasons, a dictionary, which holds the key-value pairs directly, is also
    accepted as second parameter.
    ]
    3. locktime           (numeric, optional, default=0) Raw locktime. Non-0 value also locktime-activates inputs
    4. replaceable        (boolean, optional, default=false) Marks this transaction as BIP125 replaceable.
    Allows this transaction to be replaced by a transaction with higher fees. If provided, it is an error if explicit sequence numbers are incompatible.

**Result:**

    "psbt" (string) The resulting raw transaction (base64-encoded string)

**Examples:**

    > qtum-cli createpsbt "[{\"txid\":\"myid\",\"vout\":0}]" "[{\"data\":\"00010203\"}]"

### createrawtransaction

createrawtransaction [{"txid":"id","vout":n},...] [{"address":amount},{"data":"hex"},...] ( locktime ) ( replaceable )

Create a transaction spending the given inputs and creating new outputs.
Outputs can be addresses or data.
Returns hex-encoded raw transaction.
Note that the transaction's inputs are not signed, and
it is not stored in the wallet or transmitted to the network.

**Arguments:**

     1. "inputs"               (array, required) A json array of json objects
         [
           {
             "txid":"id",      (string, required) The transaction id
             "vout":n,         (numeric, required) The output number
             "sequence":n      (numeric, optional) The sequence number
           } 
           ,...
         ]
    2. "outputs"               (array, required) a json array with outputs (key-value pairs), where none of the keys are duplicated.
    That is, each address can only appear once and there can only be one 'data' object.
       [
        {
          "address": x.xxx,    (obj, optional) A key-value pair. The key (string) is the qtum address, the value (float or string) is the amount in QTUM
        },
        {
          "data": "hex"        (obj, optional) A key-value pair. The key must be "data", the value is hex encoded data
        },
        {
          "contract":{
             "contractAddress":"address",   (string, required) Valid contract address (valid hash160 hex data)
             "data":"hex",                  (string, required) Hex data to add in the call output
             "amount":x.xxx,                (numeric, optional) Value in QTUM to send with the call, should be a valid amount, default 0
             "gasLimit":x,                  (numeric, optional) The gas limit for the transaction
             "gasPrice":x.xxx               (numeric, optional) The gas price for the transaction
           } 
        {
        ,...                     More key-value pairs of the above form. For compatibility reasons, a dictionary, which holds the key-value pairs directly, is also
                                 accepted as second parameter.
       ]
    3. locktime                  (numeric, optional, default=0) Raw locktime. Non-0 value also locktime-activates inputs
    4. replaceable               (boolean, optional, default=false) Marks this transaction as BIP125 replaceable.
                                 Allows this transaction to be replaced by a transaction with higher fees. If provided, it is an error if explicit sequence numbers are incompatible.

**Result:**

    "transaction" (string) hex string of the transaction

**Examples:**

    > qtum-cli createrawtransaction "[{\"txid\":\"myid\",\"vout\":0}]" "[{\"address\":0.01}]"
    
    > qtum-cli createrawtransaction "[{\"txid\":\"myid\",\"vout\":0}]" "[{\"data\":\"00010203\"}]"
    
    > qtum-cli createrawtransaction "[{\"txid\":\"myid\",\"vout\":0}]" "[{\"contract\":{\"contractAddress\":\"mycontract\",\"data\":\"00\", \"gasLimit\":250000, \"gasPrice\":0.00000040, \"amount\":0}}]"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": ["[{\"txid\":\"myid\",\"vout\":0}]", "[{\"address\":0.01}]"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": ["[{\"txid\":\"myid\",\"vout\":0}]", "[{\"data\":\"00010203\"}]"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": ["[{\"txid\":\"myid\",\"vout\":0}]", "[{\"contract\":{\"contractAddress\":\"mycontract\",\"data\":\"00\", \"gasLimit\":250000, \"gasPrice\":0.00000040, \"amount\":0}}]"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### decodepsbt

Return a JSON object representing the serialized, base64-encoded partially signed Qtum transaction.

**Arguments:**

    1. "psbt" (string, required) The PSBT base64 string

**Result:**
   
    {
      "tx" : {                   (json object) The decoded network-serialized unsigned transaction.
        ...                                      The layout is the same as the output of decoderawtransaction.
      },
      "unknown" : {                (json object) The unknown global fields
        "key" : "value"            (key-value pair) An unknown key-value pair
         ...
      },
      "inputs" : [                 (array of json objects)
        {
          "non_witness_utxo" : {   (json object, optional) Decoded network transaction for non-witness UTXOs
            ...
          },
          "witness_utxo" : {            (json object, optional) Transaction output for witness UTXOs
            "amount" : x.xxx,           (numeric) The value in QTUM
            "scriptPubKey" : {          (json object)
              "asm" : "asm",            (string) The asm
              "hex" : "hex",            (string) The hex
              "type" : "pubkeyhash",    (string) The type, eg 'pubkeyhash'
              "address" : "address"     (string) Qtum address if there is one
            }
          },
          "partial_signatures" : {             (json object, optional)
            "pubkey" : "signature",           (string) The public key and signature that corresponds to it.
            ,...
          }
          "sighash" : "type",                  (string, optional) The sighash type to be used
          "redeem_script" : {       (json object, optional)
              "asm" : "asm",            (string) The asm
              "hex" : "hex",            (string) The hex
              "type" : "pubkeyhash",    (string) The type, eg 'pubkeyhash'
            }
          "witness_script" : {       (json object, optional)
              "asm" : "asm",            (string) The asm
              "hex" : "hex",            (string) The hex
              "type" : "pubkeyhash",    (string) The type, eg 'pubkeyhash'
            }
          "bip32_derivs" : {          (json object, optional)
            "pubkey" : {                     (json object, optional) The public key with the derivation path as the value.
              "master_fingerprint" : "fingerprint"     (string) The fingerprint of the master key
              "path" : "path",                         (string) The path
            }
            ,...
          }
          "final_scriptsig" : {       (json object, optional)
              "asm" : "asm",            (string) The asm
              "hex" : "hex",            (string) The hex
            }
           "final_scriptwitness": ["hex", ...] (array of string) hex-encoded witness data (if any)
          "unknown" : {                (json object) The unknown global fields
            "key" : "value"            (key-value pair) An unknown key-value pair
             ...
          },
        }
        ,...
      ]
      "outputs" : [                 (array of json objects)
        {
          "redeem_script" : {       (json object, optional)
              "asm" : "asm",            (string) The asm
              "hex" : "hex",            (string) The hex
              "type" : "pubkeyhash",    (string) The type, eg 'pubkeyhash'
            }
          "witness_script" : {       (json object, optional)
              "asm" : "asm",            (string) The asm
              "hex" : "hex",            (string) The hex
              "type" : "pubkeyhash",    (string) The type, eg 'pubkeyhash'
          }
          "bip32_derivs" : [          (array of json objects, optional)
            {
              "pubkey" : "pubkey",                     (string) The public key this path corresponds to
              "master_fingerprint" : "fingerprint"     (string) The fingerprint of the master key
              "path" : "path",                         (string) The path
              }
            }
            ,...
          ],
          "unknown" : {                (json object) The unknown global fields
            "key" : "value"            (key-value pair) An unknown key-value pair
             ...
          },
        }
        ,...
      ]
      "fee" : fee                      (numeric, optional) The transaction fee paid if all UTXOs slots in the PSBT have been filled.
    }

**Examples:**

    > qtum-cli decodepsbt "psbt"

### decoderawtransaction 

Return a JSON object representing the serialized, hex-encoded transaction.

**Arguments:**

    1. "hexstring" (string, required) The transaction hex string
    2. iswitness   (boolean, optional) Whether the transaction hex is a serialized witness transaction
    If iswitness is not present, heuristic tests will be used in decoding

**Result:**
 
    {
      "txid" : "id",          (string) The transaction id
      "hash" : "id",          (string) The transaction hash (differs from txid for witness transactions)
      "size" : n,             (numeric) The transaction size
      "vsize" : n,            (numeric) The virtual transaction size (differs from size for witness transactions)
      "weight" : n,           (numeric) The transaction's weight (between vsize*4 - 3 and vsize*4)
      "version" : n,          (numeric) The version
      "locktime" : ttt,       (numeric) The lock time
      "vin" : [               (array of json objects)
         {
           "txid": "id",      (string) The transaction id
           "vout": n,         (numeric) The output number
           "scriptSig": {     (json object) The script
             "asm": "asm",  (string) asm
             "hex": "hex"   (string) hex
           },
           "txinwitness": ["hex", ...] (array of string) hex-encoded witness data (if any)
           "sequence": n     (numeric) The script sequence number
         }
         ,...
      ],
      "vout" : [             (array of json objects)
         {
           "value" : x.xxx,            (numeric) The value in QTUM
           "n" : n,                    (numeric) index
           "scriptPubKey" : {          (json object)
             "asm" : "asm",          (string) the asm
             "hex" : "hex",          (string) the hex
             "reqSigs" : n,            (numeric) The required sigs
             "type" : "pubkeyhash",  (string) The type, eg 'pubkeyhash'
             "addresses" : [           (json array of string)
               "Q2tvKAXCxZjSmdNbao16dKXC8tRWfcF5oc"   (string) qtum address
               ,...
             ]
           }
         }
         ,...
      ],
    }

**Examples:**

    > qtum-cli decoderawtransaction "hexstring"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decoderawtransaction", "params": ["hexstring"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:** 

    ./qtum-cli decoderawtransaction "0100000001697f98c004bbb7d184119a31b2b8c96683fa8c7ca0d7755c6196888fb6ba046e010000006a473044022077de54191ae91b502d03a83bd1d580a8b4467fc3d205c7bce169f13e6abc1c91022064f759845c960b04ddf9dd5a635da5f8b990fc934fced06747d52f2658603735012103c426034f05b3b66700f151991e6e45f2d63545a73b36c0a8e8c4200c53f7fd2cfeffffff02a0f53813000000001976a914e85324d4402d9758122c5498de80d1cfcc6330cb88aca09f6636000000001976a914093f4c533deb449f6bd0a427bddb0f02c297101388ac5dad0700"
    
**Test result:**

    {
      "txid": "27f5f35b447e219d0b3a3ac55f9dc6aacf2d4145fbd930207ef5b7710c47d883",
      "hash": "27f5f35b447e219d0b3a3ac55f9dc6aacf2d4145fbd930207ef5b7710c47d883",
      "version": 1,
      "size": 225,
      "vsize": 225,
      "weight": 900,
      "locktime": 503133,
      "vin": [
        {
          "txid": "6e04bab68f8896615c75d7a07c8cfa8366c9b8b2319a1184d1b7bb04c0987f69",
          "vout": 1,
          "scriptSig": {
            "asm": "3044022077de54191ae91b502d03a83bd1d580a8b4467fc3d205c7bce169f13e6abc1c91022064f759845c960b04ddf9dd5a635da5f8b990fc934fced06747d52f2658603735[ALL] 03c426034f05b3b66700f151991e6e45f2d63545a73b36c0a8e8c4200c53f7fd2c",
            "hex": "473044022077de54191ae91b502d03a83bd1d580a8b4467fc3d205c7bce169f13e6abc1c91022064f759845c960b04ddf9dd5a635da5f8b990fc934fced06747d52f2658603735012103c426034f05b3b66700f151991e6e45f2d63545a73b36c0a8e8c4200c53f7fd2c"
          },
          "sequence": 4294967294
        }
      ],
      "vout": [
        {
          "value": 3.22500000,
          "n": 0,
          "scriptPubKey": {
            "asm": "OP_DUP OP_HASH160 e85324d4402d9758122c5498de80d1cfcc6330cb OP_EQUALVERIFY OP_CHECKSIG",
            "hex": "76a914e85324d4402d9758122c5498de80d1cfcc6330cb88ac",
            "reqSigs": 1,
            "type": "pubkeyhash",
            "addresses": [
              "QhnQUjuCK7PANDqE7tCdf5DVjKmHoykeSY"
            ]
          }
        },
        {
          "value": 9.12695200,
          "n": 1,
          "scriptPubKey": {
            "asm": "OP_DUP OP_HASH160 093f4c533deb449f6bd0a427bddb0f02c2971013 OP_EQUALVERIFY OP_CHECKSIG",
            "hex": "76a914093f4c533deb449f6bd0a427bddb0f02c297101388ac",
            "reqSigs": 1,
            "type": "pubkeyhash",
            "addresses": [
              "QMSt24HzDcBQmsqCybzYQmfVPQFvNjK6ax"
            ]
          }
        }
      ]
    }

### decodescript 

Decode a hex-encoded script.

**Arguments:**

    1. "hexstring" (string) the hex encoded script

**Result:**

    {
      "asm":"asm",   (string) Script public key
      "hex":"hex",   (string) hex encoded public key
      "type":"type", (string) The output type
      "reqSigs": n,  (numeric) The required signatures
      "addresses": [ (json array of string)
      "address"      (string) qtum address
      ,...
      ],
      "p2sh","address" (string) address of P2SH script wrapping this redeem script (not returned if the script is already a P2SH).
    }
    
**Examples:**

    > qtum-cli decodescript "hexstring"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decodescript", "params": ["hexstring"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
    ### finalizepsbt

Finalize the inputs of a PSBT. If the transaction is fully signed, it will produce a network serialized transaction which can be broadcast with sendrawtransaction. Otherwise a PSBT will be created which has the final_scriptSig and final_scriptWitness fields filled for inputs that are complete. Implements the Finalizer and Extractor roles.

**Arguments:**

    1. "psbt"    (string) A base64 string of a PSBT
    2. "extract" (boolean, optional, default=true) If true and the transaction is complete, extract and return the complete transaction in normal network serialization instead of the PSBT.

**Result:**

    {
      "psbt" : "value",           (string) The base64-encoded partially signed transaction if not extracted
      "hex"  : "value",           (string) The hex-encoded network transaction if extracted
      "complete" : true|false,    (boolean) If the transaction has a complete set of signatures
    }

**Examples:**

    > qtum-cli finalizepsbt "psbt"

### fromhexaddress

Converts a raw hex address to a base58 pubkeyhash address

**Arguments:**

    1. "hexaddress" (string, required) The raw hex address

**Result:**

    "address" (string) The base58 pubkeyhash address

**Examples:**

    > qtum-cli fromhexaddress "hexaddress"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "fromhexaddress", "params": ["hexaddress"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    fromhexaddress "6c89a1a6ca2ae7c00b248bb2832d6f480f27da68"
    
**Test result:**

    qTTH1Yr2eKCuDLqfxUyBLCAjmomQ8pyrBt

### fundrawtransaction

Add inputs to a transaction until it has enough in value to meet its out value.
This will not modify existing inputs, and will add at most one change output to the outputs.
No existing outputs will be modified unless "subtractFeeFromOutputs" is specified.
Note that inputs which were signed may need to be resigned after completion since in/outputs have been added.
The inputs added will not be signed, use signrawtransaction for that.
Note that all existing inputs must have their previous output transaction be in the wallet.
Note that all inputs selected must be of standard form and P2SH scripts must be
in the wallet using importaddress or addmultisigaddress (to calculate fees).
You can see whether this is the case by checking the "solvable" field in the listunspent output.
Only pay-to-pubkey, multisig, and P2SH versions thereof are currently supported for watch-only

**Arguments:**

    1. "hexstring"                (string, required) The hex string of the raw transaction
    2. options                    (object, optional)
       {
         "changeAddress"          (string, optional, default pool address) The qtum address to receive the change
         "changePosition"         (numeric, optional, default random) The index of the change output
         "change_type"            (string, optional) The output type to use. Only valid if changeAddress is not specified. Options are "legacy", "p2sh-segwit", and "bech32". Default is set by -changetype.
         "includeWatching"        (boolean, optional, default false) Also select inputs which are watch only
         "lockUnspents"           (boolean, optional, default false) Lock selected unspent outputs
         "feeRate"                (numeric, optional, default not set: makes wallet determine the fee) Set a specific fee rate in QTUM/kB
         "subtractFeeFromOutputs" (array, optional) A json array of integers.
                                  The fee will be equally deducted from the amount of each specified output.
                                  The outputs are specified by their zero-based index, before any change output is added.
                                  Those recipients will receive less qtums than you enter in their corresponding amount field.
                                  If no outputs are specified here, the sender pays the fee.
                                      [vout_index,...]
         "replaceable"            (boolean, optional) Marks this transaction as BIP125 replaceable.
                                  Allows this transaction to be replaced by a transaction with higher fees
         "conf_target"            (numeric, optional) Confirmation target (in blocks)
         "estimate_mode"          (string, optional, default=UNSET) The fee estimate mode, must be one of:
             "UNSET"
             "ECONOMICAL"
             "CONSERVATIVE"
       }
                                  for backward compatibility: passing in a true instead of an object will result in {"includeWatching":true}
    3. iswitness                  (boolean, optional) Whether the transaction hex is a serialized witness transaction 
                                  If iswitness is not present, heuristic tests will be used in decoding


**Result:**

    {
      "hex": "value", (string) The resulting raw transaction (hex-encoded string)
      "fee": n,       (numeric) Fee in QTUM the resulting transaction pays
      "changepos": n  (numeric) The position of the added change output, or -1
    }

**Examples:**

Create a transaction with no inputs

    > qtum-cli createrawtransaction "[]" "{\"myaddress\":0.01}"

Add sufficient unsigned inputs to meet the output value

    > qtum-cli fundrawtransaction "rawtransactionhex"

Sign the transaction

    > qtum-cli signrawtransaction "fundedtransactionhex"

Send the transaction

    > qtum-cli sendrawtransaction "signedtransactionhex"

### gethexaddress

Converts a base58 pubkeyhash address to a hex address for use in smart contracts.

**Arguments:**

    1. "address" (string, required) The base58 address

**Result:**

    "hexaddress" (string) The raw hex pubkeyhash address for use in smart contracts

**Examples:**

    > qtum-cli gethexaddress "address"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gethexaddress", "params": ["address"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
**Test example:**

    gethexaddress "qTTH1Yr2eKCuDLqfxUyBLCAjmomQ8pyrBt"
    
**Test result:**

    6c89a1a6ca2ae7c00b248bb2832d6f480f27da68

### getrawtransaction 

NOTE: By default this function only works for mempool transactions. If the -txindex option is
enabled, it also works for blockchain transactions. If the block which contains the transaction
is known, its hash can be provided even for nodes without -txindex. Note that if a blockhash is
provided, only that block will be searched and if the transaction is in the mempool or other
blocks, or if this node does not have the given block available, the transaction will not be found.
**DEPRECATED**: for now, it also works for transactions with unspent outputs.

Return the raw transaction data.

If verbose is 'true', returns an Object with information about 'txid'.
If verbose is 'false' or omitted, returns a string that is serialized, hex-encoded data for 'txid'.

**Arguments:**

    1. "txid"      (string, required) The transaction id
    2. verbose     (bool, optional, default=false) If false, return a string, otherwise return a json object
    3. "blockhash" (string, optional) The block in which to look for the transaction
    
    Result (if verbose is not set or set to false):
    "data"         (string) The serialized, hex-encoded data for 'txid'
    
    Result (if verbose is set to true):
    {
      "in_active_chain": b,   (bool) Whether specified block is in the active chain or not (only present with explicit "blockhash" argument)
      "hex" : "data",         (string) The serialized, hex-encoded data for 'txid'
      "txid" : "id",          (string) The transaction id (same as provided)
      "hash" : "id",          (string) The transaction hash (differs from txid for witness transactions)
      "size" : n,             (numeric) The serialized transaction size
      "vsize" : n,            (numeric) The virtual transaction size (differs from size for witness transactions)
      "weight" : n,           (numeric) The transaction's weight (between vsize*4-3 and vsize*4)
      "version" : n,          (numeric) The version
      "locktime" : ttt,       (numeric) The lock time
      "vin" : [               (array of json objects)
         {
           "txid": "id",      (string) The transaction id
           "vout": n,         (numeric) 
           "scriptSig": {     (json object) The script
             "asm": "asm",    (string) asm
             "hex": "hex"     (string) hex
           },
           "sequence": n      (numeric) The script sequence number
           "txinwitness": ["hex", ...] (array of string) hex-encoded witness data (if any)
         }
         ,...
      ],
      "vout" : [              
         {
           "value" : x.xxx,            (numeric) The value in QTUM
           "n" : n,                    (numeric) index
           "scriptPubKey" : {          (json object)
             "asm" : "asm",            (string) the asm
             "hex" : "hex",            (string) the hex
             "reqSigs" : n,            (numeric) The required sigs
             "type" : "pubkeyhash",    (string) The type, eg 'pubkeyhash'
             "addresses" : [           (json array of string)
               "address"               (string) qtum address
               ,...
             ]
           }
         }
         ,...
      ],
      "blockhash" : "hash",     (string) the block hash
      "confirmations" : n,      (numeric) The confirmations
      "time" : ttt,             (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT)
      "blocktime" : ttt         (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
    }

**Examples:**

    > qtum-cli getrawtransaction "mytxid"
    
    > qtum-cli getrawtransaction "mytxid" true
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawtransaction", "params": ["mytxid", true] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
    > qtum-cli getrawtransaction "mytxid" false "myblockhash"
    
    > qtum-cli getrawtransaction "mytxid" true "myblockhash"

### sendrawtransaction

Submits raw transaction (serialized, hex-encoded) to local node and network.

Also see createrawtransaction and signrawtransaction calls.

**Arguments:**

    1. "hexstring" (string, required) The hex string of the raw transaction)
    2. allowhighfees (boolean, optional, default=false) Allow high fees

**Result:**

    "hex" (string) The transaction hash in hex

**Examples:**

Create a transaction

    > qtum-cli createrawtransaction "[{\"txid\" : \"mytxid\",\"vout\":0}]" "{\"myaddress\":0.01}"
    
 Sign the transaction, and get back the hex
    
    > qtum-cli signrawtransaction "myhex"

Send the transaction (signed hex)

    > qtum-cli sendrawtransaction "signedhex"

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendrawtransaction", "params": ["signedhex"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### signrawtransaction

**DEPRECATED**. Sign inputs for raw transaction (serialized, hex-encoded).
The second optional argument (may be null) is an array of previous transaction outputs that this transaction depends on but may not yet be in the block chain.
The third optional argument (may be null) is an array of base58-encoded private
keys that, if given, will be the only keys used to sign the transaction.

**Arguments:**

    1. "hexstring"                      (string, required) The transaction hex string
    2. "prevtxs"       (string, optional) An json array of previous dependent transaction outputs
         [                              (json array of json objects, or 'null' if none provided)
           {
             "txid":"id",               (string, required) The transaction id
             "vout":n,                  (numeric, required) The output number
             "scriptPubKey": "hex",     (string, required) script key
             "redeemScript": "hex",     (string, required for P2SH or P2WSH) redeem script
             "amount": value            (numeric, required) The amount spent
           }
           ,...
        ]
    3. "privkeys"                       (string, optional) A json array of base58-encoded private keys for signing
        [                               (json array of strings, or 'null' if none provided)
          "privatekey"                  (string) private key in base58-encoding
          ,...
        ]
    4. "sighashtype"                    (string, optional, default=ALL) The signature hash type. Must be one of
           "ALL"
           "NONE"
           "SINGLE"
           "ALL|ANYONECANPAY"
           "NONE|ANYONECANPAY"
           "SINGLE|ANYONECANPAY"

**Result:**

    {
      "hex" : "value",               (string) The hex-encoded raw transaction with signature(s)
      "complete" : true|false,       (boolean) If the transaction has a complete set of signatures
      "errors" : [                   (json array of objects) Script verification errors (if there are any)
        {
          "txid" : "hash",           (string) The hash of the referenced, previous transaction
          "vout" : n,                (numeric) The index of the output to spent and used as input
          "scriptSig" : "hex",       (string) The hex-encoded signature script
          "sequence" : n,            (numeric) Script sequence number
          "error" : "text"           (string) Verification or signing error related to the input
        }
        ,...
      ]
    }

### signrawtransactionwithkey

Sign inputs for raw transaction (serialized, hex-encoded).
The second argument is an array of base58-encoded private
keys that will be the only keys used to sign the transaction.
The third optional argument (may be null) is an array of previous transaction outputs that
this transaction depends on but may not yet be in the block chain.

**Arguments:**

    1. "hexstring"                      (string, required) The transaction hex string
    2. "privkeys"                       (string, required) A json array of base58-encoded private keys for signing
        [                               (json array of strings)
          "privatekey"                  (string) private key in base58-encoding
          ,...
        ]
    3. "prevtxs"                        (string, optional) An json array of previous dependent transaction outputs
        [                               (json array of json objects, or 'null' if none provided)
           {
             "txid":"id",               (string, required) The transaction id
             "vout":n,                  (numeric, required) The output number
             "scriptPubKey": "hex",     (string, required) script key
             "redeemScript": "hex",     (string, required for P2SH or P2WSH) redeem script
             "amount": value            (numeric, required) The amount spent
           }
           ,...
        ]
    4. "sighashtype"                    (string, optional, default=ALL) The signature hash type. Must be one of
           "ALL"
           "NONE"
           "SINGLE"
           "ALL|ANYONECANPAY"
           "NONE|ANYONECANPAY"
           "SINGLE|ANYONECANPAY"

**Result:**

    {
      "hex" : "value",                  (string) The hex-encoded raw transaction with signature(s)
      "complete" : true|false,          (boolean) If the transaction has a complete set of signatures
      "errors" : [                      (json array of objects) Script verification errors (if there are any)
        {
          "txid" : "hash",              (string) The hash of the referenced, previous transaction
          "vout" : n,                   (numeric) The index of the output to spent and used as input
          "scriptSig" : "hex",          (string) The hex-encoded signature script
          "sequence" : n,               (numeric) Script sequence number
          "error" : "text"              (string) Verification or signing error related to the input
        }
        ,...
      ]
    }

**Examples:**

    > qtum-cli signrawtransactionwithkey "myhex"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signrawtransactionwithkey", "params": ["myhex"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### testmempoolaccept 

Returns if raw transaction (serialized, hex-encoded) would be accepted by mempool.

This checks if the transaction violates the consensus or policy rules.

See sendrawtransaction call.

**Arguments:**

    1. ["rawtxs"] (array, required) An array of hex strings of raw transactions. Length must be one for now.
    2. allowhighfees (boolean, optional, default=false) Allow high fees

**Result:**

    [                  (array) The result of the mempool acceptance test for each raw transaction in the input array.
                                Length is exactly one for now.
     {
      "txid"           (string) The transaction hash in hex
      "allowed"        (boolean) If the mempool allows this tx to be inserted
      "reject-reason"  (string) Rejection string (only present when 'allowed' is false)
     }
    ]

**Examples:**

Create a transaction

    > qtum-cli createrawtransaction "[{\"txid\" : \"mytxid\",\"vout\":0}]" "{\"myaddress\":0.01}" Sign the transaction, and get back the hex
    
    > qtum-cli signrawtransaction "myhex"

Test acceptance of the transaction (signed hex)

    > qtum-cli testmempoolaccept ["signedhex"]

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "testmempoolaccept", "params": [["signedhex"]] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

## Util

### createmultisig 

Creates a multi-signature address with n signature of m keys required.
It returns a json object with the address and redeemScript.

**Arguments:**

    1. nrequired                    (numeric, required) The number of required signatures out of the n keys.
    2. "keys"                       (string, required) A json array of keys which are qtum addresses or hex-encoded public keys
         [
           "key"                    (string) qtum address or hex-encoded public key
           ,...
         ]
    3. "address_type"               (string, optional) The address type to use. Options are "legacy", "p2sh-segwit", and "bech32". Default is legacy.

**Result:**

    {
      "address":"multisigaddress",  (string) The value of the new multisig address.
      "redeemScript":"script"       (string) The string value of the hex-encoded redemption script.
    }

**Examples:**

Create a multisig address from 2 public keys

    > qtum-cli createmultisig 2 "[\"QjWnDZxwLhrJDcp4Hisse8RfBo2jRDZY5Z\",\"Q6sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\"]"

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createmultisig", "params": [2, "[\"QjWnDZxwLhrJDcp4Hisse8RfBo2jRDZY5Z\",\"Q6sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### estimatesmartfee

Estimates the approximate fee per kilobyte needed for a transaction to begin
confirmation within conf_target blocks if possible and return the number of blocks
for which the estimate is valid. Uses virtual transaction size as defined
in BIP 141 (witness data is discounted).

**Arguments:**

   

    1. conf_target     (numeric) Confirmation target in blocks (1 - 1008)
    2. "estimate_mode" (string, optional, default=CONSERVATIVE) The fee estimate mode.
                       Whether to return a more conservative estimate which also satisfies
                       a longer history. A conservative estimate potentially returns a
                       higher feerate and is more likely to be sufficient for the desired
                       target, but is not as responsive to short term drops in the
                       prevailing fee market.  Must be one of:
           "UNSET" (defaults to CONSERVATIVE)
           "ECONOMICAL"
           "CONSERVATIVE"

**Result:**

    {
      "feerate" : x.x,     (numeric, optional) estimate fee-per-kilobyte (in QTUM)
      "errors": [ str... ] (json array of strings, optional) Errors encountered during processing
      "blocks" : n         (numeric) block number where estimate was found
    }

The request target will be clamped between 2 and the highest target
fee estimation is able to return based on how long it has been running.
An error is returned if not enough transactions and blocks
have been observed to make an estimate for any number of blocks.

**Example:**

    > qtum-cli estimatesmartfee 6

### signmessagewithprivkey

Sign a message with the private key of an address

**Arguments:**

    1. "privkey"         (string, required) The private key to sign the message with.
    2. "message"         (string, required) The message to create a signature of.

**Result:**

    "signature"          (string) The signature of the message encoded in base 64

**Examples:**

Create the signature

    > qtum-cli signmessagewithprivkey "privkey" "my message"

Verify the signature

    > qtum-cli verifymessage "QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "signature" "my message"

As json rpc

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signmessagewithprivkey", "params": ["privkey", "my message"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### validateaddress

Return information about the given qtum address.

**DEPRECATION WARNING:** 
Parts of this command have been deprecated and moved to getaddressinfo. Clients must transition to using getaddressinfo to access this information before upgrading to v0.18. 
The following deprecated fields have moved to getaddressinfo and will only be shown here with -deprecatedrpc=validateaddress: ismine, iswatchonly, script, hex, pubkeys, sigsrequired, pubkey, addresses, embedded, iscompressed, account, timestamp, hdkeypath, kdmasterkeyid.

**Arguments:**

    1. "address" (string, required) The qtum address to validate

**Result:**

    {
      "isvalid" : true|false,       (boolean) If the address is valid or not. If not, this is the only property returned.
      "address" : "address",        (string) The qtum address validated
      "scriptPubKey" : "hex",       (string) The hex encoded scriptPubKey generated by the address
      "isscript" : true|false,      (boolean) If the key is a script
      "iswitness" : true|false,     (boolean) If the address is a witness address
      "witness_version" : version   (numeric, optional) The version number of the witness program
      "witness_program" : "hex"     (string, optional) The hex value of the witness program
    }

**Examples:**

    > qtum-cli validateaddress "QPSSGeFHDnKNxiEyFrD1wcEaHr9hrQDDWc"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "validateaddress", "params": ["QPSSGeFHDnKNxiEyFrD1wcEaHr9hrQDDWc"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### verifymessage

Verify a signed message

**Arguments:**

    1. "address" (string, required) The qtum address to use for the signature.
    2. "signature" (string, required) The signature provided by the signer in base 64 encoding (see signmessage).
    3. "message" (string, required) The message that was signed.

**Result:**

    true|false (boolean) If the signature is verified or not.
    
**Examples:**

Unlock the wallet for 30 seconds

    > qtum-cli walletpassphrase "mypassphrase" 30

Create the signature

    > qtum-cli signmessage "QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "my message"

Verify the signature

    > qtum-cli verifymessage "QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "signature" "my message"

As json rpc

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifymessage", "params": ["QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX", "signature", "my message"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

## Wallet

### abandontransaction

Mark in-wallet transaction <txid> as abandoned
This will mark this transaction and all its in-wallet descendants as abandoned which will allow
for their inputs to be respent. It can be used to replace "stuck" or evicted transactions.
It only works on transactions which are not included in a block and are not currently in the mempool.
It has no effect on transactions which are already abandoned.

**Arguments:**

    1. "txid" (string, required) The transaction id

**Examples:**

    > qtum-cli abandontransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "abandontransaction", "params": ["1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### abortrescan

Stops current wallet rescan triggered by an RPC call, e.g. by an importprivkey call.

**Examples:**

Import a private key

    > qtum-cli importprivkey "mykey"

Abort the running wallet rescan

    > qtum-cli abortrescan

As a JSON-RPC call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "abortrescan", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli abortrescan
    
**Test result:**

    false

### addmultisigaddress

Add a nrequired-to-sign multisignature address to the wallet. Requires a new wallet backup.
Each key is a Qtum address or hex-encoded public key.
This functionality is only intended for use with non-watchonly addresses.
See importaddress for watchonly p2sh address support.
If 'label' is specified, assign address to that label.

**Arguments:**

    1. nrequired                      (numeric, required) The number of required signatures out of the n keys or addresses.
    2. "keys"                         (string, required) A json array of qtum addresses or hex-encoded public keys
         [
           "address"                  (string) qtum address or hex-encoded public key
           ...,
         ]
    3. "label"                        (string, optional) A label to assign the addresses to.
    4. "address_type"                 (string, optional) The address type to use. Options are "legacy", "p2sh-segwit", and "bech32". Default is set by -addresstype
    
**Result:**

    {
      "address":"multisigaddress", (string) The value of the new multisig address.
      "redeemScript":"script"      (string) The string value of the hex-encoded redemption script.
    }

**Examples:**

Add a multisig address from 2 addresses

    > qtum-cli addmultisigaddress 2 "[\"QjWnDZxwLhrJDcp4Hisse8RfBo2jRDZY5Z\",\"Q6sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\"]"

As json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "addmultisigaddress", "params": [2, "[\"QjWnDZxwLhrJDcp4Hisse8RfBo2jRDZY5Z\",\"Q6sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
### backupwallet 

Safely copies current wallet file to destination, which can be a directory or a path with filename.

**Arguments:**

    1. "destination" (string) The destination directory or file

**Examples:**

    > qtum-cli backupwallet "backup.dat"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "backupwallet", "params": ["backup.dat"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### bumpfee

Bumps the fee of an opt-in-RBF transaction T, replacing it with a new transaction B.
An opt-in RBF transaction with the given txid must be in the wallet.
The command will pay the additional fee by decreasing (or perhaps removing) its change output.
If the change output is not big enough to cover the increased fee, the command will currently fail
instead of adding new inputs to compensate. (A future implementation could improve this.)
The command will fail if the wallet or mempool contains a transaction that spends one of T's outputs.
By default, the new fee will be calculated automatically using estimatesmartfee.
The user can specify a confirmation target for estimatesmartfee.
Alternatively, the user can specify totalFee, or use RPC settxfee to set a higher fee rate.
At a minimum, the new fee rate must be high enough to pay an additional new relay fee (incrementalfee returned by getnetworkinfo) to enter the node's mempool.

**Arguments:**

    1. txid                  (string, required) The txid to be bumped
    2. options               (object, optional)
       {
         "confTarget"        (numeric, optional) Confirmation target (in blocks)
         "totalFee"          (numeric, optional) Total fee (NOT feerate) to pay, in satoshis.
                             In rare cases, the actual fee paid might be slightly higher than the specified
                             totalFee if the tx change output has to be removed because it is too close to
                             the dust threshold.
         "replaceable"       (boolean, optional, default true) Whether the new transaction should still be
                             marked bip-125 replaceable. If true, the sequence numbers in the transaction will
                             be left unchanged from the original. If false, any input sequence numbers in the
                             original transaction that were less than 0xfffffffe will be increased to 0xfffffffe
                             so the new transaction will not be explicitly bip-125 replaceable (though it may
                             still be replaceable in practice, for example if it has unconfirmed ancestors which
                             are replaceable).
         "estimate_mode"     (string, optional, default=UNSET) The fee estimate mode, must be one of:
             "UNSET"
             "ECONOMICAL"
             "CONSERVATIVE"
       }

**Result:**

    {
      "txid": "value",     (string) The id of the new transaction
      "origfee": n,        (numeric) Fee of the replaced transaction
      "fee": n,            (numeric) Fee of the new transaction
      "errors": [ str... ] (json array of strings) Errors encountered during processing (may be empty)
    }

**Examples:**

    Bump the fee, get the new transaction's txid

    > qtum-cli bumpfee <txid>

### createcontract

Create a contract with bytcode.

**Arguments:**

    1. "bytecode"       (string, required) contract bytcode.
    2. gasLimit         (numeric or string, optional) gasLimit, default: 2500000, max: 40000000
    3. gasPrice         (numeric or string, optional) gasPrice QTUM price per gas unit, default: 0.0000004, min:0.0000004
    4. "senderaddress"  (string, optional) The quantum address that will be used to create the contract.
    5. "broadcast"      (bool, optional, default=true) Whether to broadcast the transaction or not.
    6. "changeToSender" (bool, optional, default=true) Return the change to the sender.

**Result:**

    [
      {
        "txid" :    (string) The transaction id.
        "sender" :  (string) QTUM address of the sender.
        "hash160" : (string) ripemd-160 hash of the sender.
        "address" : (string) expected contract address.
    }
    ]

**Examples:**

    > qtum-cli createcontract "60606040525b33600060006101000a81548173ffffffffffffffffffffffffffffffffffffffff02191690836c010000000000000000000000009081020402179055506103786001600050819055505b600c80605b6000396000f360606040526008565b600256"
    
    > qtum-cli createcontract "60606040525b33600060006101000a81548173ffffffffffffffffffffffffffffffffffffffff02191690836c010000000000000000000000009081020402179055506103786001600050819055505b600c80605b6000396000f360606040526008565b600256" 6000000 0.0000004 "QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" true
    
### createwallet

Creates and loads a new wallet.

**Arguments:**

    1. "wallet_name"        (string, required) The name for the new wallet. If this is a path, the wallet will be created at the path location.
    2. disable_private_keys (boolean, optional, default: false) Disable the possibility of private keys (only watchonlys are possible in this mode).

**Result:**

    {
      "name" :    <wallet_name>, (string) The wallet name if created successfully. If the wallet was created using a full path, the wallet_name will be the full path.
      "warning" : <warning>,     (string) Warning message if wallet was not loaded cleanly.
    }

**Examples:**

    > qtum-cli createwallet "testwallet"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createwallet", "params": ["testwallet"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:** 

    createwallet “ancd”
    
**Test result:**

      {
        "name": "ancd",
        "warning": ""
      }

### dumpprivkey 

Reveals the private key corresponding to 'address'.
Then the importprivkey can be used with this output

**Arguments:**

    1. "address"   (string, required) The qtum address for the private key

**Result:**

    "key"                (string) The private key

**Examples:**

    > qtum-cli dumpprivkey "myaddress"
    
    > qtum-cli importprivkey "mykey"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpprivkey", "params": ["myaddress"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### dumpwallet 

Dumps all wallet keys in a human-readable format to a server-side file. This does not allow overwriting existing files.

**Arguments:**

    1. "filename"    (string, required) The filename with path (either absolute or relative to qtumd)

**Result:**
  
    { 
    
      "filename" :  (string) The filename with full absolute path
    
    }

**Examples:**

    > qtum-cli dumpwallet "test"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpwallet", "params": ["test"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### encryptwallet 

Encrypts the wallet with 'passphrase'. This is for first time encryption.
After this, any calls that interact with private keys such as sending or signing
will require the passphrase to be set prior the making these calls.
Use the walletpassphrase call for this, and then walletlock call.
If the wallet is already encrypted, use the wallet passphrase change call.
Note that this will shutdown the server.

**Arguments:**

    1. "passphrase" (string) The pass phrase to encrypt the wallet with. It must be at least 1 character, but should be long.

**Examples:**

Encrypt your wallet

    > qtum-cli encryptwallet "my pass phrase"

Now set the passphrase to use the wallet, such as for signing or sending qtum

    > qtum-cli walletpassphrase "my pass phrase"

Now we can do something like sign

    > qtum-cli signmessage "address" "test message"

Now lock the wallet again by removing the passphrase

    > qtum-cli walletlock

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "encryptwallet", "params": ["my pass phrase"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
### getaddressesbylabel

Returns the list of addresses assigned the specified label.

**Arguments:**

    1. "label" (string, required) The label.

**Result:**

    { 
      "address": 
      { 
        "purpose": "string" (string) Purpose of address ("send" for sending address, "receive" for receiving address)
      },...
    }

**Examples:**

    > qtum-cli getaddressesbylabel "tabby"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressesbylabel", "params": ["tabby"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getaddressesbylabel ""
    
**Test result:**

    {
        "QUTYNrXYMQUzZyUekmfakR8bzTuLqYcLtf": 
        {
          "purpose": "receive"
        },
        "QZmURd7wViLVKjUu8b3mvdXeSJjFmH7hf2": 
        {
          "purpose": "receive"
        }
    }

### getaddressinfo 

Return information about the given qtum address. Some information requires the address to be in the wallet.

**Arguments:**

    1. "address"                    (string, required) The qtum address to get the information of.

**Result:**

    {
      "address" : "address",        (string) The qtum address validated
      "scriptPubKey" : "hex",       (string) The hex encoded scriptPubKey generated by the address
      "ismine" : true|false,        (boolean) If the address is yours or not
      "iswatchonly" : true|false,   (boolean) If the address is watchonly
      "isscript" : true|false,      (boolean) If the key is a script
      "iswitness" : true|false,     (boolean) If the address is a witness address
      "witness_version" : version   (numeric, optional) The version number of the witness program
      "witness_program" : "hex"     (string, optional) The hex value of the witness program
      "script" : "type"             (string, optional) The output script type. Only if "isscript" is true and the redeemscript is known. Possible types: nonstandard, pubkey, pubkeyhash, scripthash, multisig, nulldata, witness_v0_keyhash, witness_v0_scripthash, witness_unknown
      "hex" : "hex",                (string, optional) The redeemscript for the p2sh address
      "pubkeys"                     (string, optional) Array of pubkeys associated with the known redeemscript (only if "script" is "multisig")
        [
          "pubkey"
          ,...
        ]
      "sigsrequired" : xxxxx        (numeric, optional) Number of signatures required to spend multisig output (only if "script" is "multisig")
      "pubkey" : "publickeyhex",    (string, optional) The hex value of the raw public key, for single-key addresses (possibly embedded in P2SH or P2WSH)
      "embedded" : {...},           (object, optional) Information about the address embedded in P2SH or P2WSH, if relevant and known. It includes all getaddressinfo output fields for the embedded address, excluding metadata ("timestamp", "hdkeypath", "hdseedid") and relation to the wallet ("ismine", "iswatchonly", "account").
      "iscompressed" : true|false,  (boolean) If the address is compressed
      "label" :  "label"            (string) The label associated with the address, "" is the default account
      "account" : "account"         (string) DEPRECATED. This field will be removed in V0.18. To see this deprecated field, start qtumd with -deprecatedrpc=accounts. The account associated with the address, "" is the default account
      "timestamp" : timestamp,      (number, optional) The creation time of the key if available in seconds since epoch (Jan 1 1970 GMT)
      "hdkeypath" : "keypath"       (string, optional) The HD keypath if the key is HD and available
      "hdseedid" : "<hash160>"      (string, optional) The Hash160 of the HD seed
      "hdmasterkeyid" : "<hash160>" (string, optional) alias for hdseedid maintained for backwards compatibility. Will be removed in V0.18.
      "labels"                      (object) Array of labels associated with the address.
        [
          { (json object of label data)
            "name": "labelname"     (string) The label
            "purpose": "string"     (string) Purpose of address ("send" for sending address, "receive" for receiving address)
          },...
        ]
    }

**Examples:**

    > qtum-cli getaddressinfo "QZCAJ4qLJpNW74Cbgtnav18wYxQ9wX4V3h"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressinfo", "params": ["QZCAJ4qLJpNW74Cbgtnav18wYxQ9wX4V3h"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getaddressinfo "QZCAJ4qLJpNW74Cbgtnav18wYxQ9wX4V3h"

**Test result:**

    {
      "address": "QZCAJ4qLJpNW74Cbgtnav18wYxQ9wX4V3h",
      "scriptPubKey": "76a9148a1827980248580e401055e52c9617cfbbe7efbf88ac",
      "ismine": true,
      "iswatchonly": false,
      "isscript": false,
      "iswitness": false,
      "pubkey": "0397a9f2710a0ac5a1ee1345893be6d903fc9e7c79479ab6a4067064731d009a73",
      "iscompressed": true,
      "label": "",
      "timestamp": 1562060128,
      "hdkeypath": "m/88'/0'/0'",
      "hdseedid": "96d04ecdab5e6ddeb20b8c62c98cf3a7548ab07d",
      "hdmasterkeyid": "96d04ecdab5e6ddeb20b8c62c98cf3a7548ab07d",
      "labels": [
        {
          "name": "",
          "purpose": "receive"
        }
      ]
    }

### getbalance 

Returns the total available balance.
The available balance is what the wallet considers currently spendable, and is
thus affected by options which limit spendability such as -spendzeroconfchange.

**Arguments:**

    1. (dummy)           (string, optional) Remains for backward compatibility. Must be excluded or set to "*".
    2. minconf           (numeric, optional, default=0) Only include transactions confirmed at least this many times.
    3. include_watchonly (bool, optional, default=false) Also include balance in watch-only addresses (see 'importaddress')

**Result:**

    amount              (numeric) The total amount in QTUM received for this account.

**Examples:**

The total amount in the wallet with 1 or more confirmations

    > qtum-cli getbalance 

The total amount in the wallet at least 6 blocks confirmed

    > qtum-cli getbalance "*" 6

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbalance", "params": ["*", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getbalance

**Test result:**

    5.683000

### getnewaddress

Returns a new Qtum address for receiving payments.
If 'label' is specified, it is added to the address book
so payments received with the address will be associated with 'label'.

**Arguments:**

    1. "label" (string, optional) The label name for the address to be linked to. If not provided, the default label "" is used. It can also be set to the empty string "" to represent the default label. The label does not need to exist, it will be created if there is no label by the given name.
    2. "address_type" (string, optional) The address type to use. Options are "legacy", "p2sh-segwit", and "bech32". Default is set by -addresstype.

**Result:**

    "address" (string) The new qtum address

**Examples:**

    > qtum-cli getnewaddress
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnewaddress", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getnewaddress
        
**Test result:**

    QcMKCuHMFwwGNBdYYes8vKN1Qm1MJkwsQf

### getrawchangeaddress 

Returns a new Qtum address, for receiving change.
This is for use with raw transactions, NOT normal use.

**Arguments:**

    1. "address_type"           (string, optional) The address type to use. Options are "legacy", "p2sh-segwit", and "bech32". Default is set by -changetype.

**Result:**

    "address"    (string) The address

**Examples:**

    > qtum-cli getrawchangeaddress 
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawchangeaddress", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Test example:**

    ./qtum-cli getrawchangeaddress 

**Test result:**

    QhPwqZNWgcgJRZpRH21hs3b2g8PooeaoPt
    
### getreceivedbyaddress

Returns the total amount received by the given address in transactions with at least minconf confirmations.

**Arguments:**

    1. "address"         (string, required) The qtum address for transactions.
    2. minconf             (numeric, optional, default=1) Only include transactions confirmed at least this many times.

**Result:**

amount   (numeric) The total amount in QTUM received at this address.

**Examples:**

The amount from transactions with at least 1 confirmation

    > qtum-cli getreceivedbyaddress "QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX"

The amount including unconfirmed transactions, zero confirmations

    > qtum-cli getreceivedbyaddress "QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" 0

The amount with at least 6 confirmations, very safe

    > qtum-cli getreceivedbyaddress "QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" 6

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getreceivedbyaddress", "params": ["QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### gettransaction 

Get detailed information about in-wallet transaction <txid>

**Arguments:**

    1. "txid"                  (string, required) The transaction id
    2. "include_watchonly"     (bool, optional, default=false) Whether to include watch-only addresses in balance calculation and details[]
    3. "waitconf"              (int, optional, default=0) Wait for enough confirmations before returning

**Result:**

    {
      "amount" : x.xxx,        (numeric) The transaction amount in QTUM
      "fee": x.xxx,            (numeric) The amount of the fee in QTUM. This is negative and only available for the 
                                  'send' category of transactions.
      "confirmations" : n,     (numeric) The number of confirmations
      "blockhash" : "hash",    (string) The block hash
      "blockindex" : xx,       (numeric) The index of the transaction in the block that includes it
      "blocktime" : ttt,       (numeric) The time in seconds since epoch (1 Jan 1970 GMT)
      "txid" : "transactionid",   (string) The transaction id.
      "time" : ttt,            (numeric) The transaction time in seconds since epoch (1 Jan 1970 GMT)
      "timereceived" : ttt,    (numeric) The time received in seconds since epoch (1 Jan 1970 GMT)
      "bip125-replaceable": "yes|no|unknown",  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                       may be unknown for unconfirmed transactions not in the mempool
      "details" : [
        {
          "account" : "accountname",        (string) DEPRECATED. This field will be removed in a V0.18. To see this deprecated field, start qtumd with -deprecatedrpc=accounts. The account name involved in the transaction, can be "" for the default account.
          "address" : "address",            (string) The qtum address involved in the transaction
          "category" : "send|receive",      (string) The category, either 'send' or 'receive'
          "amount" : x.xxx,                 (numeric) The amount in QTUM
          "label" : "label",                (string) A comment for the address/transaction, if any
          "vout" : n,                       (numeric) the vout value
          "fee": x.xxx,                     (numeric) The amount of the fee in QTUM. This is negative and only available for the 
                                               'send' category of transactions.
          "abandoned": xxx                  (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the 
                                               'send' category of transactions.
        }
        ,...
      ],
      "hex" : "data"                        (string) Raw data for transaction
    }

**Examples:**

    > qtum-cli gettransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"
    
    > qtum-cli gettransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d" true
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettransaction", "params": ["1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### getunconfirmedbalance

Returns the server's total unconfirmed balance

### getwalletinfo

Returns an object containing various wallet state info.

**Result:**

    {
      "walletname": xxxxx,               (string) the wallet name
      "walletversion": xxxxx,            (numeric) the wallet version
      "balance": xxxxxxx,                (numeric) the total confirmed balance of the wallet in QTUM
      "stake": xxxxxxx,                  (numeric) the total stake balance of the wallet in QTUM
      "unconfirmed_balance": xxx,        (numeric) the total unconfirmed balance of the wallet in QTUM
      "immature_balance": xxxxxx,        (numeric) the total immature balance of the wallet in QTUM
      "txcount": xxxxxxx,                (numeric) the total number of transactions in the wallet
      "keypoololdest": xxxxxx,           (numeric) the timestamp (seconds since Unix epoch) of the oldest pre-generated key in the key pool
      "keypoolsize": xxxx,               (numeric) how many new keys are pre-generated (only counts external keys)
      "keypoolsize_hd_internal": xxxx,   (numeric) how many new keys are pre-generated for internal use (used for change outputs, only appears if the wallet is using this feature, otherwise external keys are used)
      "unlocked_until": ttt,             (numeric) the timestamp in seconds since epoch (midnight Jan 1 1970 GMT) that the wallet is unlocked for transfers, or 0 if the wallet is locked
      "paytxfee": x.xxxx,                (numeric) the transaction fee configuration, set in QTUM/kB
      "hdseedid": "<hash160>"            (string, optional) the Hash160 of the HD seed (only present when HD is enabled)
      "hdmasterkeyid": "<hash160>"       (string, optional) alias for hdseedid retained for backwards-compatibility. Will be removed in V0.18.
      "private_keys_enabled": true|false (boolean) false if privatekeys are disabled for this wallet (enforced watch-only wallet)
    }
    
**Examples:**
  
      > qtum-cli getwalletinfo
      
      > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getwalletinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### importaddress 

Adds an address or script (in hex) that can be watched as if it were in your wallet but cannot be used to spend. Requires a new wallet backup.

**Arguments:**

    1. "address"            (string, required) The Bitcoin address (or hex-encoded script)
    2. "label"              (string, optional, default="") An optional label
    3. rescan               (boolean, optional, default=true) Rescan the wallet for transactions
    4. p2sh                 (boolean, optional, default=false) Add the P2SH version of the script as well

Note: This call can take over an hour to complete if rescan is true, during that time, other rpc calls
may report that the imported address exists but related transactions are still missing, leading to temporarily incorrect/bogus balances and unspent outputs until rescan completes.
If you have the full public key, you should call importpubkey instead of this.

Note: If you import a non-standard raw script in hex form, outputs sending to it will be treated
as change, and not show up in many RPCs.

**Examples:**

Import an address with rescan

    > qtum-cli importaddress "myaddress"

Import using a label without rescan

    > qtum-cli importaddress "myaddress" "testing" false

As a JSON-RPC call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importaddress", "params": ["myaddress", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### importmulti

Import addresses/scripts (with private or public keys, redeem script (P2SH)), rescanning all addresses in one-shot-only (rescan can be disabled via options). Requires a new wallet backup.

**Arguments:**

    1. requests                                                   (array, required) Data to be imported
      [     
        {
          "scriptPubKey": "<script>" | { "address":"<address>" }, (string / json, required) Type of scriptPubKey (string for script, json for address)
          "timestamp": timestamp | "now"                        , (integer / string, required) Creation time of the key in seconds since epoch (Jan 1 1970 GMT),
                                                                  or the string "now" to substitute the current synced blockchain time. The timestamp of the oldest
                                                                  key will determine how far back blockchain rescans need to begin for missing wallet transactions.
                                                                  "now" can be specified to bypass scanning, for keys which are known to never have been used, and
                                                                  0 can be specified to scan the entire blockchain. Blocks up to 2 hours before the earliest key
                                                                  creation time of all keys being imported by the importmulti call will be scanned.
          "redeemscript": "<script>"                            , (string, optional) Allowed only if the scriptPubKey is a P2SH address or a P2SH scriptPubKey
          "pubkeys": ["<pubKey>", ... ]                         , (array, optional) Array of strings giving pubkeys that must occur in the output or redeemscript
          "keys": ["<key>", ... ]                               , (array, optional) Array of strings giving private keys whose corresponding public keys must occur in the output or redeemscript
          "internal": <true>                                    , (boolean, optional, default: false) Stating whether matching outputs should be treated as not incoming payments aka change
          "watchonly": <true>                                   , (boolean, optional, default: false) Stating whether matching outputs should be considered watched even when they're not spendable, only allowed if keys are empty
          "label": <label>                                      , (string, optional, default: '') Label to assign to the address (aka account name, for now), only allowed with internal=false
        }
      ,...
      ]
    2. options                 (json, optional)
      {
         "rescan": <false>,         (boolean, optional, default: true) Stating if should rescan the blockchain after all imports
      }
    
    Note: This call can take over an hour to complete if rescan is true, during that time, other rpc calls
    may report that the imported keys, addresses or scripts exists but related transactions are still missing.

**Examples:**

    > qtum-cli importmulti '[{ "scriptPubKey": { "address": "<my address>" }, "timestamp":1455191478 }, { "scriptPubKey": { "address": "<my 2nd address>" }, "label": "example 2", "timestamp": 1455191480 }]'
    
    > qtum-cli importmulti '[{ "scriptPubKey": { "address": "<my address>" }, "timestamp":1455191478 }]' '{ "rescan": false}'
    
    Response is an array with the same size as the input that has the execution result :
    [{ "success": true } , { "success": false, "error": { "code": -1, "message": "Internal Server Error"} }, ... ]

### importprivkey

Adds a private key (as returned by dumpprivkey) to your wallet. Requires a new wallet backup.
Hint: use importmulti to import more than one private key.

**Arguments:**

    1. "qtumprivkey" (string, required) The private key (see dumpprivkey)
    2. "label"       (string, optional, default="") An optional label
    3. rescan        (boolean, optional, default=true) Rescan the wallet for transactions

Note: This call can take over an hour to complete if rescan is true, during that time, other rpc calls
may report that the imported key exists but related transactions are still missing, leading to temporarily incorrect/bogus balances and unspent outputs until rescan completes.

**Examples:**

Dump a private key

    > qtum-cli dumpprivkey "myaddress"

Import the private key with rescan

    > qtum-cli importprivkey "mykey"

Import using a label and without rescan

    > qtum-cli importprivkey "mykey" "testing" false

Import using default blank label and without rescan

    > qtum-cli importprivkey "mykey" "" false

As a JSON-RPC call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importprivkey", "params": ["mykey", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### importprunedfunds

Imports funds without rescan. Corresponding address or script must previously be included in wallet. Aimed towards pruned wallets. The end-user is responsible to import additional transactions that subsequently spend the imported outputs or rescan after the point in the blockchain the transaction is included.

**Arguments:**

    1. "rawtransaction" (string, required) A raw transaction in hex funding an already-existing address in wallet
    2. "txoutproof" (string, required) The hex output from gettxoutproof that contains the transaction

### listreceivedbyaddress

List balances by receiving address.

**Arguments:**

    1. minconf (numeric, optional, default=1) The minimum number of confirmations before payments are included.
    2. include_empty (bool, optional, default=false) Whether to include addresses that haven't received any payments.
    3. include_watchonly (bool, optional, default=false) Whether to include watch-only addresses (see 'importaddress').
    4. address_filter (string, optional) If present, only return information on this address.

**Result:**

     [
      {
        "involvesWatchonly" : true,        (bool) Only returned if imported addresses were involved in transaction
        "address" : "receivingaddress",    (string) The receiving address
        "account" : "accountname",         (string) DEPRECATED. Backwards compatible alias for label.
        "amount" : x.xxx,                  (numeric) The total amount in QTUM received by the address
        "confirmations" : n,               (numeric) The number of confirmations of the most recent transaction included
        "label" : "label",                 (string) The label of the receiving address. The default label is "".
        "txids": [
           "txid",                         (string) The ids of transactions received with the address 
           ...
        ]
      }
      ,...
    ]

### importpubkey

Adds a public key (in hex) that can be watched as if it were in your wallet but cannot be used to spend. Requires a new wallet backup.

**Arguments:**

    1. "pubkey" (string, required) The hex-encoded public key
    2. "label"  (string, optional, default="") An optional label
    3. rescan   (boolean, optional, default=true) Rescan the wallet for transactions
    
    Note: This call can take over an hour to complete if rescan is true, during that time, other rpc calls
    may report that the imported pubkey exists but related transactions are still missing, leading to temporarily incorrect/bogus balances and unspent outputs until rescan completes.

**Examples:**

Import a public key with rescan

    > qtum-cli importpubkey "mypubkey"

Import using a label without rescan

    > qtum-cli importpubkey "mypubkey" "testing" false

As a JSON-RPC call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importpubkey", "params": ["mypubkey", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### importwallet

Imports keys from a wallet dump file (see dumpwallet). Requires a new wallet backup to include imported keys.

**Arguments:**

    1. "filename" (string, required) The wallet file

**Examples:**

Dump the wallet

    > qtum-cli dumpwallet "test"

Import the wallet

    > qtum-cli importwallet "test"

Import using the json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importwallet", "params": ["test"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/


### keypoolrefill

Fills the keypool.

**Arguments:**

    1. newsize (numeric, optional, default=100) The new keypool size

**Examples:**

    > qtum-cli keypoolrefill
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "keypoolrefill", "params": [] }' -H 'con

### listaddressgroupings

Lists groups of addresses which have had their common ownership
made public by common use as inputs or as the resulting change
in past transactions

**Result:**

    [
      [
        [
          "address", (string) The qtum address
           amount,   (numeric) The amount in QTUM
          "label"    (string, optional) The label
        ]
        ,...
      ]
      ,...
    ]

**Examples:**

    > qtum-cli listaddressgroupings
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaddressgroupings", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
       

### listlabels

Returns the list of all labels, or labels that are assigned to addresses with a specific purpose.

**Arguments:**

    1. "purpose" (string, optional) Address purpose to list labels for ('send','receive'). An empty string is the same as not providing this argument.

**Result:**

    [ 
      "label", (string) Label name
      ...
    ]

**Examples:**

List all labels

    > qtum-cli listlabels

List labels that have receiving addresses

    > qtum-cli listlabels receive

List labels that have sending addresses

    > qtum-cli listlabels send

As json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listlabels", "params": [receive] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### listlockunspent

Returns list of temporarily unspendable outputs.
See the lockunspent call to lock and unlock transactions for spending.

**Result:**

    [
      {
        "txid" : "transactionid", (string) The transaction id locked
        "vout" : n ,              (numeric) The vout value
      }
      ,...
    ]

**Examples:**

List the unspent transactions

    > qtum-cli listunspent

Lock an unspent transaction

    > qtum-cli lockunspent false "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"

List the locked transactions

    > qtum-cli listlockunspent

Unlock the transaction again

    > qtum-cli lockunspent true "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listlockunspent", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

**Examples:**

    > qtum-cli listreceivedbyaddress
    
    > qtum-cli listreceivedbyaddress 6 true
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaddress", "params": [6, true, true] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaddress", "params": [6, true, true, "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### listsinceblock

Get all transactions in blocks since block [blockhash], or all transactions if omitted.
If "blockhash" is no longer a part of the main chain, transactions from the fork point onward are included.
Additionally, if include_removed is set, transactions affecting the wallet which were removed are returned in the "removed" array.

**Arguments:**

    1. "blockhash" (string, optional) The block hash to list transactions since
    2. target_confirmations: (numeric, optional, default=1) Return the nth block hash from the main chain. e.g. 1 would mean the best block hash. Note: this is not used as a filter, but only affects [lastblock] in the return value
    3. include_watchonly: (bool, optional, default=false) Include transactions to watch-only addresses (see 'importaddress')
    4. include_removed: (bool, optional, default=true) Show transactions that were removed due to a reorg in the "removed" array
    (not guaranteed to work on pruned nodes)

**Result:**

    {
      "transactions": 
      [
        "account":"accountname",       (string) DEPRECATED. This field will be removed in V0.18. To see this deprecated field, start qtumd with -deprecatedrpc=accounts. The account name associated with the transaction. Will be "" for the default account.
        "address":"address",           (string) The qtum address of the transaction. Not present for move transactions (category = move).
        "category":"send|receive",     (string) The transaction category. 'send' has negative amounts, 'receive' has positive amounts.
        "amount": x.xxx,               (numeric) The amount in QTUM. This is negative for the 'send' category, and for the 'move' category for moves 
                                               outbound. It is positive for the 'receive' category, and for the 'move' category for inbound funds.
        "vout" : n,                    (numeric) the vout value
        "fee": x.xxx,                  (numeric) The amount of the fee in QTUM. This is negative and only available for the 'send' category of transactions.
        "confirmations": n,            (numeric) The number of confirmations for the transaction. Available for 'send' and 'receive' category of transactions.
                                              When it's < 0, it means the transaction conflicted that many blocks ago.
        "blockhash": "hashvalue",      (string) The block hash containing the transaction. Available for 'send' and 'receive' category of transactions.
        "blockindex": n,               (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive' category of transactions.
        "blocktime": xxx,              (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
        "txid": "transactionid",       (string) The transaction id. Available for 'send' and 'receive' category of transactions.
        "time": xxx,                   (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT).
        "timereceived": xxx,           (numeric) The time received in seconds since epoch (Jan 1 1970 GMT). Available for 'send' and 'receive' category of transactions.
        "bip125-replaceable": "yes|no|unknown",  
                                       (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                              may be unknown for unconfirmed transactions not in the mempool
        "abandoned": xxx,              (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the 'send' category of transactions.
        "comment": "...",              (string) If a comment is associated with the transaction.
        "label" : "label"              (string) A comment for the address/transaction, if any
        "to": "...",                   (string) If a comment to is associated with the transaction.
      ],
      "removed": [
        <structure is the same as "transactions" above, only present if include_removed=true>
        Note: transactions that were re-added in the active chain will appear as-is in this array, and may thus have a positive confirmation count.
      ],
      "lastblock": "lastblockhash"     (string) The hash of the block (target_confirmations-1) from the best block on the main chain. This is typically used to feed back into listsinceblock the next time you call it. So you would generally use a target_confirmations of say 6, so you will be continually re-notified of transactions until they've reached 6 confirmations plus any new ones
    }

**Examples:**

    > qtum-cli listsinceblock
    
    > qtum-cli listsinceblock "000000000000000bacf66f7497b7dc45ef753ee9a7d38571037cdb1a57f663ad" 6
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listsinceblock", "params": ["000000000000000bacf66f7497b7dc45ef753ee9a7d38571037cdb1a57f663ad", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### listtransactions

If a label name is provided, this will return only incoming transactions paying to addresses with the specified label.

Returns up to 'count' most recent transactions skipping the first 'from' transactions.

Note that the "account" argument and "otheraccount" return value have been removed in V0.17. To use this RPC with an "account" argument, restart
qtumd with -deprecatedrpc=accounts

**Arguments:**

    1. "label"           (string, optional) If set, should be a valid label name to return only incoming transactions
                  with the specified label, or "*" to disable filtering and return all transactions.
    2. count             (numeric, optional, default=10) The number of transactions to return
    3. skip              (numeric, optional, default=0) The number of transactions to skip
    4. include_watchonly (bool, optional, default=false) Include transactions to watch-only addresses (see 'importaddress')
  
  **Result:**

    [
      {
        "address":"address",      (string) The qtum address of the transaction.
        "category":"send|receive", (string) The transaction category.
        "amount": x.xxx,          (numeric) The amount in QTUM. This is negative for the 'send' category, and is positive
                                            for the 'receive' category,
        "label": "label",         (string) A comment for the address/transaction, if any
        "vout": n,                (numeric) the vout value
        "fee": x.xxx,             (numeric) The amount of the fee in QTUM. This is negative and only available for the 
                                             'send' category of transactions.
        "confirmations": n,       (numeric) The number of confirmations for the transaction. Negative confirmations indicate the
                                             transaction conflicts with the block chain
        "trusted": xxx,           (bool) Whether we consider the outputs of this unconfirmed transaction safe to spend.
        "blockhash": "hashvalue", (string) The block hash containing the transaction.
        "blockindex": n,          (numeric) The index of the transaction in the block that includes it.
        "blocktime": xxx,         (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
        "txid": "transactionid",  (string) The transaction id.
        "time": xxx,              (numeric) The transaction time in seconds since epoch (midnight Jan 1 1970 GMT).
        "timereceived": xxx,      (numeric) The time received in seconds since epoch (midnight Jan 1 1970 GMT).
        "comment": "...",         (string) If a comment is associated with the transaction. 
        "bip125-replaceable": "yes|no|unknown",  (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
                                                         may be unknown for unconfirmed transactions not in the mempool
        "abandoned": xxx          (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the 
                                             'send' category of transactions.
      }
    ]

**Examples:**

List the most recent 10 transactions in the systems

    > qtum-cli listtransactions 

List transactions 100 to 120

    > qtum-cli listtransactions "*" 20 100

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listtransactions", "params": ["*", 20, 100] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### listreceivedbylabel

List received transactions by label.

**Arguments:**

    1. minconf           (numeric, optional, default=1) The minimum number of confirmations before payments are included.
    2. include_empty     (bool, optional, default=false) Whether to include labels that haven't received any payments.
    3. include_watchonly (bool, optional, default=false) Whether to include watch-only addresses (see 'importaddress').

**Result:**

    [
      {
        "involvesWatchonly" : true, (bool) Only returned if imported addresses were involved in transaction
        "account" : "accountname",  (string) DEPRECATED. Backwards compatible alias for label.
        "amount" : x.xxx,           (numeric) The total amount received by addresses with this label
        "confirmations" : n,        (numeric) The number of confirmations of the most recent transaction included
        "label" : "label"           (string) The label of the receiving address. The default label is "".
      }
      ,...
    ]

**Examples:**

    > qtum-cli listreceivedbylabel
    
    > qtum-cli listreceivedbylabel 6 true
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbylabel", "params": [6, true, true] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### listunspent 

Returns array of unspent transaction outputs with between minconf and maxconf (inclusive) confirmations.

Optionally filter to only include txouts paid to specified addresses.

**Arguments:**

    1. minconf               (numeric, optional, default=1) The minimum confirmations to filter
    2. maxconf               (numeric, optional, default=9999999) The maximum confirmations to filter
    3. "addresses"           (string) A json array of qtum addresses to filter
        [
          "address"          (string) qtum address
          ,...
        ]
    4. include_unsafe        (bool, optional, default=true) Include outputs that are not safe to spend See description of "safe" attribute below.
    5. query_options         (json, optional) JSON with query options
        {
          "minimumAmount"    (numeric or string, default=0) Minimum value of each UTXO in QTUM
          "maximumAmount"    (numeric or string, default=unlimited) Maximum value of each UTXO in QTUM
          "maximumCount"     (numeric or string, default=unlimited) Maximum number of UTXOs
          "minimumSumAmount" (numeric or string, default=unlimited) Minimum sum value of all UTXOs in QTUM
        }

**Result：**

    [                
      {
        "txid" : "txid",          (string) the transaction id 
        "vout" : n,               (numeric) the vout value
        "address" : "address",    (string) the qtum address
        "label" : "label",        (string) The associated label, or "" for the default label
        "account" : "account",    (string) DEPRECATED. This field will be removed in V0.18. To see this deprecated field, start qtumd with -deprecatedrpc=accounts. The associated account, or "" for the default account
        "scriptPubKey" : "key",   (string) the script key
        "amount" : x.xxx,         (numeric) the transaction output amount in QTUM
        "confirmations" : n,      (numeric) The number of confirmations
        "redeemScript" : n        (string) The redeemScript if scriptPubKey is P2SH
        "spendable" : xxx,        (bool) Whether we have the private keys to spend this output
        "solvable" : xxx,         (bool) Whether we know how to spend this output, ignoring the lack of keys
        "safe" : xxx              (bool) Whether this output is considered safe to spend. Unconfirmed transactions
                                  from outside keys and unconfirmed replacement transactions are considered unsafe
                                  and are not eligible for spending by fundrawtransaction and sendtoaddress.
      }
      ,...
    ]

**Examples：**

    > qtum-cli listunspent 
    
    > qtum-cli listunspent 6 9999999 "[\"QjWnDZxwLhrJDcp4Hisse8RfBo2jRDZY5Z\",\"Q6sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\"]"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [6, 9999999 "[\"QjWnDZxwLhrJDcp4Hisse8RfBo2jRDZY5Z\",\"Q6sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
    > qtum-cli listunspent 6 9999999 '[]' true '{ "minimumAmount": 0.005 }'
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [6, 9999999, [] , true, { "minimumAmount": 0.005 } ] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### listwallets

Returns a list of currently loaded wallets.
For full information on the wallet, use "getwalletinfo"

**Result:**

    [                         
      "walletname"            (string) the wallet name
       ...
    ]

**Examples:**

    > qtum-cli listwallets 
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listwallets", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### loadwallet

loadwallet "filename"

Loads a wallet from a wallet file or directory.
Note that all wallet command-line options used when starting qtumd will be
applied to the new wallet (eg -zapwallettxes, upgradewallet, rescan, etc).

**Arguments:**

    1. "filename"    (string, required) The wallet directory or .dat file.

**Result:**

    {
      "name" :    <wallet_name>,        (string) The wallet name if loaded successfully.
      "warning" : <warning>,            (string) Warning message if wallet was not loaded cleanly.
    }

**Examples:**

    > qtum-cli loadwallet "test.dat"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "loadwallet", "params": ["test.dat"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### lockunspent

Updates list of temporarily unspendable outputs.

Temporarily lock (unlock=false) or unlock (unlock=true) specified transaction outputs.

If no transaction outputs are specified when unlocking then all current locked transaction outputs are unlocked.

A locked transaction output will not be chosen by automatic coin selection, when spending qtums.

Locks are stored in memory only. Nodes start with zero locked outputs, and the locked output list is always cleared (by virtue of process exit) when a node stops or fails. Also see the listunspent call.

**Arguments:**

    1. unlock            (boolean, required) Whether to unlock (true) or lock (false) the specified transactions
    2. "transactions"  (string, optional) A json array of objects. Each object the txid (string) vout (numeric)
         [           (json array of json objects)
           {
             "txid":"id",    (string) The transaction id
             "vout": n         (numeric) The output number
           }
           ,...
         ]
     
**Result:**

    true|false (boolean) Whether the command was successful or not

**Examples:**

List the unspent transactions

    > qtum-cli listunspent

Lock an unspent transaction

    > qtum-cli lockunspent false "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"

List the locked transactions

    > qtum-cli listlockunspent

Unlock the transaction again

    > qtum-cli lockunspent true "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "lockunspent", "params": [false, "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### removeprunedfunds

Deletes the specified transaction from the wallet. Meant for use with pruned wallets and as a companion to importprunedfunds. This will affect wallet balances.

**Arguments:**

    1. "txid" (string, required) The hex-encoded id of the transaction you are deleting

**Examples:**

    > qtum-cli removeprunedfunds "a8d0c0184dde994a09ec054286f1ce581bebf46446a512166eae7628734ea0a5"

As a JSON-RPC call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "removeprunedfunds", "params": ["a8d0c0184dde994a09ec054286f1ce581bebf46446a512166eae7628734ea0a5"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### rescanblockchain

Rescan the local blockchain for wallet related transactions.

**Arguments:**

    1. "start_height" (numeric, optional) block height where the rescan should start
    2. "stop_height" (numeric, optional) the last block height that should be scanned
    
**Result:**

    {
      "start_height" (numeric) The block height where the rescan has started. If omitted, rescan started from the genesis block.
      "stop_height" (numeric) The height of the last rescanned block. If omitted, rescan stopped at the chain tip.
    }

**Examples:**

    > qtum-cli rescanblockchain 100000 120000
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "rescanblockchain", "params": [100000, 120000] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### reservebalance 

Set reserve amount not participating in network protection.
If no parameters provided current setting is printed.

### sendmany

Send multiple times. Amounts are double-precision floating point numbers.
Note that the "fromaccount" argument has been removed in V0.17. To use this RPC with a "fromaccount" argument, restart
qtumd with -deprecatedrpc=accounts

Requires wallet passphrase to be set with walletpassphrase call.

**Arguments:**

    1. "dummy"               (string, required) Must be set to "" for backwards compatibility.
    2. "amounts"             (string, required) A json object with addresses and amounts
        {
          "address":amount   (numeric or string) The qtum address is the key, the numeric amount (can be string) in QTUM is the value
          ,...
        }
    3. minconf               (numeric, optional, default=1) Only use the balance confirmed at least this many times.
    4. "comment"             (string, optional) A comment
    5. subtractfeefrom       (array, optional) A json array with addresses.
                               The fee will be equally deducted from the amount of each selected address.
                               Those recipients will receive less qtums than you enter in their corresponding amount field.
                               If no addresses are specified here, the sender pays the fee.
        [
          "address"          (string) Subtract fee from this address
          ,...
        ]
    6. replaceable           (boolean, optional) Allow this transaction to be replaced by a transaction with higher fees via BIP 125
    7. conf_target           (numeric, optional) Confirmation target (in blocks)
    8. "estimate_mode"       (string, optional, default=UNSET) The fee estimate mode, must be one of:
           "UNSET"
           "ECONOMICAL"
           "CONSERVATIVE"

**Result:**

    "txid" (string) The transaction id for the send. Only 1 transaction is created regardless of the number of addresses.

**Examples:**

Send two amounts to two different addresses:

    > qtum-cli sendmany "" "{\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}"

Send two amounts to two different addresses setting the confirmation and comment:

    > qtum-cli sendmany "" "{\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}" 6 "testing"

Send two amounts to two different addresses, subtract fee from amount:

    > qtum-cli sendmany "" "{\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}" 1 "" "[\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\",\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\"]"

As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendmany", "params": ["", {"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX":0.01,"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz":0.02}, 6, "testing"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### sendmanywithdupes

Send multiple times. Amounts are double-precision floating point numbers. Supports duplicate addresses
Requires wallet passphrase to be set with walletpassphrase call.

**Arguments:**

    1. "fromaccount"         (string, required) DEPRECATED. The account to send the funds from. Should be "" for the default account
    2. "amounts"             (string, required) A json object with addresses and amounts
        {
          "address":amount   (numeric or string) The qtum address is the key, the numeric amount (can be string) in QTUM is the value
          ,...
        }
    3. minconf               (numeric, optional, default=1) Only use the balance confirmed at least this many times.
    4. "comment"             (string, optional) A comment
    5. subtractfeefrom       (array, optional) A json array with addresses.
                               The fee will be equally deducted from the amount of each selected address.
                               Those recipients will receive less qtums than you enter in their corresponding amount field.
                               If no addresses are specified here, the sender pays the fee.
        [
          "address"          (string) Subtract fee from this address
          ,...
        ]

**Result:**

    "txid" (string) The transaction id for the send. Only 1 transaction is created regardless of the number of addresses.
    
**Examples:**

Send two amounts to two different addresses:

    > qtum-cli sendmanywithdupes "" "{\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}"

Send two amounts to two different addresses setting the confirmation and comment:

    > qtum-cli sendmanywithdupes "" "{\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}" 6 "testing"

Send two amounts to two different addresses, subtract fee from amount:

    > qtum-cli sendmanywithdupes "" "{\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}" 1 "" "[\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\",\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\"]"
    
As a json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendmanywithdupes", "params": ["", "{\"QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"Q353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}", 6, "testing"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### sendtoaddress

Send an amount to a given address.

Requires wallet passphrase to be set with walletpassphrase call.

**Arguments:**

      1. "address"            (string, required) The qtum address to send to.
    2. "amount"               (numeric or string, required) The amount in QTUM to send. eg 0.1
    3. "comment"              (string, optional) A comment used to store what the transaction is for. 
                                 This is not part of the transaction, just kept in your wallet.
    4. "comment_to"           (string, optional) A comment to store the name of the person or organization 
                                 to which you're sending the transaction. This is not part of the 
                                 transaction, just kept in your wallet.
    5. subtractfeefromamount  (boolean, optional, default=false) The fee will be deducted from the amount being sent.
                                 The recipient will receive less qtums than you enter in the amount field.
    6. replaceable            (boolean, optional) Allow this transaction to be replaced by a transaction with higher fees via BIP 125
    7. conf_target            (numeric, optional) Confirmation target (in blocks)
    8. "estimate_mode"        (string, optional, default=UNSET) The fee estimate mode, must be one of:
           "UNSET"
           "ECONOMICAL"
           "CONSERVATIVE"
    9. "senderaddress"        (string, optional) The quantum address that will be used to send money from.
    10."changeToSender"       (bool, optional, default=false) Return the change to the sender.

**Result:**

    "txid" (string) The transaction id.

**Examples:**

    > qtum-cli sendtoaddress "QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.1
    
    > qtum-cli sendtoaddress "QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.1 "donation" "seans outpost"
    
    > qtum-cli sendtoaddress "QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.1 "" "" true
    
    > qtum-cli sendtoaddress "QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd", 0.1, "donation", "seans outpost", false, null, null, "", "QX1GkJdye9WoUnrE2v6ZQhQ72EUVDtGXQX", true
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendtoaddress", "params": ["QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd", 0.1, "donation", "seans outpost"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendtoaddress", "params": ["QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd", 0.1, "donation", "seans outpost", false, null, null, "", "QX1GkJdye9WoUnrE2v6ZQhQ72EUVDtGXQX", true] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### sendtocontract

Send funds and data to a contract.

Requires wallet passphrase to be set with walletpassphrase call.

**Arguments:**

    1. "contractaddress" (string, required) The contract address that will receive the funds and data.
    2. "datahex"         (string, required) data to send.
    3. "amount"          (numeric or string, optional) The amount in QTUM to send. eg 0.1, default: 0
    4. gasLimit          (numeric or string, optional) gasLimit, default: 250000, max: 40000000
    5. gasPrice          (numeric or string, optional) gasPrice Qtum price per gas unit, default: 0.0000004, min:0.0000004
    6. "senderaddress"   (string, optional) The quantum address that will be used as sender.
    7. "broadcast"       (bool, optional, default=true) Whether to broadcast the transaction or not.
    8. "changeToSender"  (bool, optional, default=true) Return the change to the sender.

**Result:**

    [
      {
        "txid" :    (string) The transaction id.
        "sender" :  (string) QTUM address of the sender.
        "hash160" : (string) ripemd-160 hash of the sender.
      }
    ]

**Examples:**

    > qtum-cli sendtocontract "c6ca2697719d00446d4ea51f6fac8fd1e9310214" "54f6127f"
    
    > qtum-cli sendtocontract "c6ca2697719d00446d4ea51f6fac8fd1e9310214" "54f6127f" 12.0015 6000000 0.0000004 "QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd"

### sethdseed

Set or generate a new HD wallet seed. Non-HD wallets will not be upgraded to being a HD wallet. Wallets that are already HD will have a new HD seed set so that new keys added to the keypool will be derived from this new seed.

Note that you will need to MAKE A NEW BACKUP of your wallet after setting the HD wallet seed.

Requires wallet passphrase to be set with walletpassphrase call.

**Arguments:**

    1. "newkeypool" (boolean, optional, default=true) Whether to flush old unused addresses, including change addresses, from the keypool and regenerate it.
    If true, the next address from getnewaddress and change address from getrawchangeaddress will be from this new seed.
    If false, addresses (including change addresses if the wallet already had HD Chain Split enabled) from the existing
    keypool will be used until it has been depleted.
    2. "seed" (string, optional) The WIF private key to use as the new HD seed; if not provided a random seed will be used.
    The seed value can be retrieved using the command. It is the private key marked hdseed=1
    
**Examples:**

    > qtum-cli sethdseed
    
    > qtum-cli sethdseed false
    
    > qtum-cli sethdseed true "wifkey"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sethdseed", "params": [true, "wifkey"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### settxfee

settxfee amount

Set the transaction fee per kB for this wallet. Overrides the global -paytxfee command line parameter.

**Arguments:**

    1. amount (numeric or string, required) The transaction fee in QTUM/kB

**Results:**

    true|false (boolean) Returns true if successful

**Examples:**

    > qtum-cli settxfee 0.00001
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "settxfee", "params": [0.00001] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### signmessage

Sign a message with the private key of an address

**Arguments:**

    1. "address" (string, required) The qtum address to use for the private key.
    
    2. "message" (string, required) The message to create a signature of.

**Result:**

    "signature" (string) The signature of the message encoded in base 64

**Examples:**

Unlock the wallet for 30 seconds

    > qtum-cli walletpassphrase "mypassphrase" 30

Create the signature

    > qtum-cli signmessage "QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "my message"

Verify the signature

    > qtum-cli verifymessage "QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "signature" "my message"

As json rpc

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signmessage", "params": ["QD1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX", "my message"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### signrawtransactionwithwallet

Sign inputs for raw transaction (serialized, hex-encoded).
The second optional argument (may be null) is an array of previous transaction outputs that
this transaction depends on but may not yet be in the block chain.

**Arguments:**

    1. "hexstring"                      (string, required) The transaction hex string
    2. "prevtxs"                        (string, optional) An json array of previous dependent transaction outputs
         [                              (json array of json objects, or 'null' if none provided)
           {
             "txid":"id",               (string, required) The transaction id
             "vout":n,                  (numeric, required) The output number
             "scriptPubKey": "hex",     (string, required) script key
             "redeemScript": "hex",     (string, required for P2SH or P2WSH) redeem script
             "amount": value            (numeric, required) The amount spent
           }
           ,...
        ]
    3. "sighashtype"                    (string, optional, default=ALL) The signature hash type. Must be one of
           "ALL"
           "NONE"
           "SINGLE"
           "ALL|ANYONECANPAY"
           "NONE|ANYONECANPAY"
           "SINGLE|ANYONECANPAY"

**Result:**

    {
      "hex" : "value",                  (string) The hex-encoded raw transaction with signature(s)
      "complete" : true|false,          (boolean) If the transaction has a complete set of signatures
      "errors" : [                      (json array of objects) Script verification errors (if there are any)
        {
          "txid" : "hash",              (string) The hash of the referenced, previous transaction
          "vout" : n,                   (numeric) The index of the output to spent and used as input
          "scriptSig" : "hex",          (string) The hex-encoded signature script
          "sequence" : n,               (numeric) Script sequence number
          "error" : "text"              (string) Verification or signing error related to the input
        }
        ,...
      ]
    }

**Examples:**

    > qtum-cli signrawtransactionwithwallet "myhex"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signrawtransactionwithwallet", "params": ["myhex"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### unloadwallet

Unloads the wallet referenced by the request endpoint otherwise unloads the wallet specified in the argument.
Specifying the wallet name on a wallet endpoint is invalid.

**Arguments:**

    1. "wallet_name" (string, optional) The name of the wallet to unload.

**Examples:**

    > qtum-cli unloadwallet wallet_name
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "unloadwallet", "params": [wallet_name] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
    
### walletcreatefundedpsbt

Creates and funds a transaction in the Partially Signed Transaction format. Inputs will be added if supplied inputs are not enough
Implements the Creator and Updater roles.

**Arguments:**

    1. "inputs"                (array, required) A json array of json objects
         [
           {
             "txid":"id",      (string, required) The transaction id
             "vout":n,         (numeric, required) The output number
             "sequence":n      (numeric, optional) The sequence number
           } 
           ,...
         ]
    2. "outputs"               (array, required) a json array with outputs (key-value pairs), where none of the keys are duplicated.
    That is, each address can only appear once and there can only be one 'data' object.
       [
        {
          "address": x.xxx,    (obj, optional) A key-value pair. The key (string) is the qtum address, the value (float or string) is the amount in QTUM
        },
        {
          "data": "hex"        (obj, optional) A key-value pair. The key must be "data", the value is hex encoded data
        }
        ,...                     More key-value pairs of the above form. For compatibility reasons, a dictionary, which holds the key-value pairs directly, is also
                                 accepted as second parameter.
       ]
    3. locktime                  (numeric, optional, default=0) Raw locktime. Non-0 value also locktime-activates inputs
                                 Allows this transaction to be replaced by a transaction with higher fees. If provided, it is an error if explicit sequence numbers are incompatible.
    4. options                 (object, optional)
       {
         "changeAddress"          (string, optional, default pool address) The qtum address to receive the change
         "changePosition"         (numeric, optional, default random) The index of the change output
         "change_type"            (string, optional) The output type to use. Only valid if changeAddress is not specified. Options are "legacy", "p2sh-segwit", and "bech32". Default is set by -changetype.
         "includeWatching"        (boolean, optional, default false) Also select inputs which are watch only
         "lockUnspents"           (boolean, optional, default false) Lock selected unspent outputs
         "feeRate"                (numeric, optional, default not set: makes wallet determine the fee) Set a specific fee rate in QTUM/kB
         "subtractFeeFromOutputs" (array, optional) A json array of integers.
                                  The fee will be equally deducted from the amount of each specified output.
                                  The outputs are specified by their zero-based index, before any change output is added.
                                  Those recipients will receive less qtums than you enter in their corresponding amount field.
                                  If no outputs are specified here, the sender pays the fee.
                                      [vout_index,...]
         "replaceable"            (boolean, optional) Marks this transaction as BIP125 replaceable.
                                  Allows this transaction to be replaced by a transaction with higher fees
         "conf_target"            (numeric, optional) Confirmation target (in blocks)
         "estimate_mode"          (string, optional, default=UNSET) The fee estimate mode, must be one of:
             "UNSET"
             "ECONOMICAL"
             "CONSERVATIVE"
       }
    5. bip32derivs                    (boolean, optional, default=false) If true, includes the BIP 32 derivation paths for public keys if we know them

**Result:**

    {
      "psbt": "value",         (string)  The resulting raw transaction (base64-encoded string)
      "fee":        n,         (numeric) Fee in QTUM the resulting transaction pays
      "changepos":  n,         (numeric) The position of the added change output, or -1
    }

**Examples:**

Create a transaction with no inputs

    > qtum-cli walletcreatefundedpsbt "[{\"txid\":\"myid\",\"vout\":0}]" "[{\"data\":\"00010203\"}]"

### walletlock

Removes the wallet encryption key from memory, locking the wallet.

After calling this method, you will need to call walletpassphrase again

before being able to call any methods which require the wallet to be unlocked.

**Examples:**

Set the passphrase for 2 minutes to perform a transaction

    > qtum-cli walletpassphrase "my pass phrase" 120

Perform a send (requires passphrase set)

    > qtum-cli sendtoaddress "QM72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 1.0

Clear the passphrase since we are done before 2 minutes is up

    > qtum-cli walletlock

As json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "walletlock", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### walletpassphrase 

Stores the wallet decryption key in memory for 'timeout' seconds.

This is needed prior to performing transactions related to private keys such as sending QTUM and staking

**Arguments:**

    1. "passphrase" (string, required) The wallet passphrase
    
    2. timeout      (numeric, required) The time to keep the decryption key in seconds; capped at 100000000 (~3 years).
    
    3. staking only (bool, optional, omitted=false, enabled=true) Unlock wallet for staking only.
    
    Note:
    
    Issuing the walletpassphrase command while the wallet is already unlocked will set a new unlock
    
    time that overrides the old one.

**Examples:**

Unlock the wallet for 60 seconds

    > qtum-cli walletpassphrase "my pass phrase" 60

Lock the wallet again (before 60 seconds)

    > qtum-cli walletlock

Unlock the wallet for staking only, for a long time

    > qtum-cli walletpassphrase "my pass phrase" 99999999 true

As json rpc call

    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "walletpassphrase", "params": ["my pass phrase", 60] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### walletpassphrasechange 

Changes the wallet passphrase from 'oldpassphrase' to 'newpassphrase'.

**Arguments:**

    1. "oldpassphrase"      (string) The current passphrase
    2. "newpassphrase"      (string) The new passphrase

**Examples:**

    > qtum-cli walletpassphrasechange "old one" "new one"
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "walletpassphrasechange", "params": ["old one", "new one"] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

### walletprocesspsbt

Update a PSBT with input information from our wallet and then sign inputs

that we can sign for.

**Arguments:**

    1. "psbt"                         (string, required) The transaction base64 string
    2. sign                           (boolean, optional, default=true) Also sign the transaction when updating
    3. "sighashtype"                  (string, optional, default=ALL) The signature hash type to sign with if not specified by the PSBT. Must be one of
           "ALL"
           "NONE"
           "SINGLE"
           "ALL|ANYONECANPAY"
           "NONE|ANYONECANPAY"
           "SINGLE|ANYONECANPAY"
    4. bip32derivs                    (boolean, optional, default=false) If true, includes the BIP 32 derivation paths for public keys if we know them

**Result:**

    {
      "psbt" : "value",          (string) The base64-encoded partially signed transaction
      "complete" : true|false,   (boolean) If the transaction has a complete set of signatures
      ]
    }

**Examples:**

    > qtum-cli walletprocesspsbt "psbt"

## zmq

### getzmqnotifications

Returns information about the active ZeroMQ notifications.

**Result:**

    [
      { 
        "type": "pubhashtx", (string) Type of notification
        "address": "..."     (string) Address of the publisher
      },
      ...
    ]

**Examples:**

    > qtum-cli getzmqnotifications
    
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getzmqnotifications", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/

