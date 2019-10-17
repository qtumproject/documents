# QRC20 Integration Technical Guide

This document explains the basics of interacting with an QRC20 contract with the `qtumd` CLI command tool.

The full example in PHP: [Qrc20.php](https://github.com/qtumproject/qrc20-wrapper/blob/master/Qrc20.php) .

# Intro

We recommend that an exchange use one main address to store tokens for all users. Below `MAIN_QRC_ADDRESS` is the main address.

The address of the QRC20 token contract is `TOKEN_CONTRACT_ADDRESS`.

* gas limit is `DEFAULT_GAS_LIMIT`, recommended value is `250000`
* gas price is `DEFAULT_GAS_PRICE`，recommended value is `0.00000040`

`TOKEN_DECIMALS` is the decimals of the token, which varies per token. Here we set it 8.

We'll use the following utility functions:

+ [addressToHash160](https://github.com/qtumproject/qrc20-wrapper/blob/480a34b38f0224967fe6ff521539ca7e321a826e/Qrc20.php#L190) - Convert base58 address to hash160 address.
+ [to32bytesArg](https://github.com/qtumproject/qrc20-wrapper/blob/480a34b38f0224967fe6ff521539ca7e321a826e/Qrc20.php#L186) left-pad hex data to 32 bytes with 0.
+ [addDecimals](https://github.com/qtumproject/qrc20-wrapper/blob/480a34b38f0224967fe6ff521539ca7e321a826e/Qrc20.php#L214:10) multiply the nominal token amount by the number of decimal places.


## Running QTUMD

You should remember to enable the indexing service when starting `qtumd`, using the flags `-logevents -txindex`.

# Interacting With QRC20

In the CLI examples below, please substitute `{}` with actual addresses and values.

## Getting Token Balance

+ `$userAddress` is the deposit address

```
qtum-cli callcontract \
    {TOKEN_CONTRACT_ADDRESS} \
    70a08231{to32bytesArg(addressToHash160($userAddress))}
```

In the JSON output look for `executionResult.output`. This is the token balance.

## Withdraw

+ `$userAddress` is the withdraw address
+ `$amount` the withdraw amount in unit token

```
qtum-cli sendtocontract \
    {TOKEN_CONTRACT_ADDRESS} \
    a9059cbb{to32bytesArg(addressToHash160($userAddress))}{to32bytesArg(addDecimals($amount)) \
    0 \
    {DEFAULT_GAS_LIMIT} \
    {DEFAULT_GAS_PRICE} \
    {MAIN_QRC_ADDRESS}
```

The command returns the `txid` of this transaction. You may use it to find information about this transaction (e.g. number of confirmations).

## Generate a deposit address

For an exchange, a user may use the same address for both QTUM and other QRC20 tokens.

Use this command to generate a deposit address:

```
qtum-cli getnewaddress
```

## Deposit and Witdraw Logs

+ `$startingBlock` is where you want to start looking (inclursive)
  + You can start looking from 0, but for better efficiency, you should remember where to start looking.

```
qtum-cli searchlogs \
    STARTING_BLOCK \
    999999999 \
    '{ "addresses": ["TOKEN_CONTRACT_ADDRESS"]}' \
    '{"topics": ["ddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef"]}'
```

The event type filtered is the `Transfer` event:

```
event Transfer(address indexed _from, address indexed _to, uint256 _value)
```

Look through the logs to filter by `to` or `from` addresses.

## Checking Confirmations

Given a transaction id `$txid`:

```
qtum-cli gettransaction $txid
```

Use the property `confirmations` from output.
