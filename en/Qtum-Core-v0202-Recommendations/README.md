## Qtum Core v0.20.2 Recommendations – 2021-04-05

#### Intended Audience

The intended audience for these recommendations is users of Qtum Core, the qtumd and Qtum-Qt full node wallets, who are using the Qtum node for staking or staking services (super staker), or other high-performance applications such as hot wallets or nodes supporting light wallets.

#### Qtum Core version 0.20.2

Qtum Core version 0.20.2 “FastLane” was released on March 20, 2012, and is available for download at https://github.com/qtumproject/qtum/releases. Version 0.20.2 is a **MANDITORY UPDATE** with a hard fork to implement new features, primarily 32-second block spacing:

* Testnet block 806,600 on March 26, 2021

* Mainnet block 845,000 approximately April 30, 2021

Any Qtum Core wallets that do not update before the hard fork will be disconnected from the Qtum network and unable to make transactions or staking with Qtum mainnet. There is no new coin created by the hard fork and this update only applies to the Qtum Core wallets qtumd and Qtum-Qt.

#### Update Now

Aside from the mandatory update before the hard fork, users should update as soon as possible to gain the advantages of the more efficient multi-threaded staker in version 0.20.2. Efficiency improvements and the multi-thread staker can give reductions in CPU utilization by an order of magnitude, or more. This new staker is especially beneficial to large wallets that are staking with UTXO sets > 5,000.

With the hard fork, average block spacing will be reduced from 128 seconds to 32 seconds, meaning the blockchain will be running four times faster. Even with the new staker, we recommend the following minimum specs for stakers:

* **Staking > 4,000 UTXOs** (own UTXOs or delegated UTXOs) at least 4 cores and 8 GB RAM
* **Staking > 8,000 UTXOs** (own UTXOs or delegated UTXOs) at least 8 cores and 24 GB RAM
* **Smaller stakers** may use 1 or 2 cores and 4 GB RAM. Under 1 GB RAM must use swap file.

#### 2,000 Block Maturity

With the hard fork to 32-second blocks, maturity for staking will change from 500 blocks – about 18 hours (currently) to 2,000 blocks – about 18 hours. Commercial applications (exchanges and wallets) should make a similar adjustment in “confirmations”, for example, if a service currently requires 20 confirmations for receiving QTUM in an account, after the hard fork this should change to 80 confirmations (e.g., 4 times the current confirmations). This will keep the time required for confirmations the same. Sometime after the mainnet hard fork, Qtum will report if it is allowable to reduce the number of confirmations.

#### Same Configuration and Startup Parameters

Core wallets should startup for v0.20.1 with the same configuration file or startup parameters as version 0.20.1. For example, and standard super staker startup command would be 

```
./qtumd -superstaking -stakingminfee=10 -stakingminutxovalue=100
```

#### Implications for Super Stakers

After the hard fork staking maturity will change to 2,000 blocks. This means that staked UTXOs will mature after 2001 blocks. Some mid-sized super stakers may need to add UTXOs for staking as follows. The staked amount compared to the total amount for a super staker should not rise higher than 65% to 70% (except for highly-controlled cases). After the hard fork, with blocks (and block rewards) arriving 4 times faster this means a staker that is averaging many stakes during the maturity period will see their number of stakes increase 4 times. If this would push their percent of staked to total beyond the 65% to 70% range, they should add 100 QTUM-sized UTXOs. Here are some examples:

![](https://qtum.s3.amazonaws.com/UTXOrequirements.jpg)

#### Qtum v0.20.2 New PRC Calls and Startup Parameters

There are some new PRC calls and startup parameters for v0.20.2.

**listconf**

Returns the options that Qtum Core was started with, for example, a qtumd super staker:

```
./qtum-cli -testnet listconf

{
  "addrindex": "1",
  "logevents": "1",
  "server": "1",
  "staking": "1",
  "stakingminfee": "10",
  "stakingminutxovalue": "100",
  "superstaking": "",
  "wallet": ""
}
```

**gettransactionreceipt** – adds bloom filter data

Adds bloom filter to the gettransactionreceipt response, for light clients to quickly retrieve related logs.

Typical bloom data for a QRC20 token transfer:

```
  "bloom": "00040000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000008000000000000000000000000000000000008000000000008000002000000000000000000000008000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000040000000000000002000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000",
```

**stakerthreads**

This startup parameter can limit the number of cores used by the staker (-stakerthreads=n) vs. the default is for the staker to use all available cores. We recommend that Qtum Core be run on a dedicated system and use all available cores.


**forceinitialblocksdownloadmode**

This startup parameter (-forceinitialblocksdownloadmode) should be used in the corner case when a node with an existing local blockchain is restarted after being offline more than 18 hours (staking maturity) because there is a slight chance the node could attempt to sync blocks starting with an orphan block (e.g., operating on an individual split chain). Alternatively, users in this situation could delete the local blockchain before restart the wallet to resync the whole blockchain.