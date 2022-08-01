# Truffle

Truffle is supported via [Janus](https://github.com/qtumproject/janus) and there are two ways to get it working.

* By loading private keys into Janus/Qtum
* Using `@qtumproject/hdwallet-provider`

Lets unbox an [example truffle box](https://github.com/qtumproject/react-box) and walk through running a migration

First, go to an empty directory and create a new directory and unbox
```bash
mkdir react-box
cd react-box
truffle unbox qtumproject/react-box
```

Output should look like this

```
Starting unbox...
=================

✔ Preparing to download box
✔ Downloading
✔ Cleaning up temporary files
✔ Setting up box

Unbox successful, sweet!

Commands:

  Compile:              truffle compile
  Migrate:              truffle migrate
  Test contracts:       truffle test
  Test dapp:            cd client && npm test
  Run dev server:       cd client && npm run start
  Build for production: cd client && npm run build
```

Next, install dependencies

```bash
npm install
```

# Generating a BIP44 mnemonic to use with truffle

You can use [Mnemonic Code Converter](https://iancoleman.io/bip39/) to generate a mnemonic for local development
 - if you plan on using this tool for mainnet, you can [download a release](https://github.com/iancoleman/bip39/releases/latest/) and run it completely offline.

And then lets take a look at the [truffle-config.js](https://github.com/qtumproject/react-box/blob/master/truffle-config.js) file

Here, you will need to copy your mnemonic into the regtest mnemonic space

```javascript
const HDWalletProvider = require("@qtumproject/hdwallet-provider");

module.exports = {
  // See <http://truffleframework.com/docs/advanced/configuration>
  // for more about customizing your Truffle configuration!
  networks: {
    // The Janus node has private keys hosted
    janus: {
      host: "127.0.0.1",
      port: 23889,
      network_id: "*",
    },
    regtest: {
      provider: () => new HDWalletProvider({
        mnemonic: "erode phrase labor rack surge risk armor uniform together prevent crack alley",
        providerOrUrl: "http://localhost:23889",
      }),
      gasPrice: "0x5d21dba000"
    },
    testnet: {
      provider: () => new HDWalletProvider({
        mnemonic: "",
        providerOrUrl: "https://testnet-janus.qiswap.com/api/",
      }),
      gasPrice: "0x5d21dba000"
    },
    mainnet: {
      provider: () => new HDWalletProvider({
        mnemonic: "",
        providerOrUrl: "https://janus.qiswap.com/api/",
      }),
      gasPrice: "0x5d21dba000"
    },
  },
  compilers: {
    solc: {
      version: "^0.8.0",
      settings: {
        optimizer: {
          enabled: true,
          runs: 1,
        },
      },
    },
  },
};
```

# Launching Janus/Qtum

```bash
# Configure Docker networking (only need be done once)
docker network create --driver bridge qtum

# Launch Qtum regtest
docker run --network=qtum -it --rm \
  --name qtumd_regtest \
  -v `pwd`:/root \
  -p 23888:23888 \
  -p 3889:3889 \
  qtum/qtum \
  qtumd -regtest -txindex -addrindex=1 -logevents \
  -rpcbind=0.0.0.0:3889 -rpcallowip=0.0.0.0/0 -rpcuser=qtum -rpcpassword=testpasswd

# Launch Janus
docker run --network=qtum -it --rm \
  --name janus_regtest \
  -v `pwd`:/root \
  -p 23889:23889 \
  ripply/janus:0.2.0 \
  --bind 0.0.0.0 --dev --qtum-rpc=http://qtum:testpasswd@qtumd_regtest:3889
```

# Seeding regtest with Qtum

You can get your address from the truffle console once Qtum is running.

```bash
truffle console --network regtest

truffle(regtest)> accounts
[
  '0x63c4953002B935C3CA925af419DFCE86C057AB95',
  '0xEccAAa32664B8499931DFB4aFD076a61e01C12F8',
  '0xB118812cCb1C79a6d0849D5393Ee6475Da5b8bdE',
  '0x733722f989763E4243D82FB8667d6DEB08BEC2A8',
  '0xe2ce59EBaC7c1B129c5623B105D62aD64eDDe645',
  '0x2974BE44127169546fC09E7C251C757892C0E990',
  '0x26c0573F40B575F663CD846Fc2D811C13a61866d',
  '0x175eE832683EbE001f01C7c944e585cD799FacB6',
  '0xC76e10C8B54e942a5b9C6E024571D4A2A9fd4a4B',
  '0x9014cedEDF69C02b43a46e414Ac643281A14acd3'
]
```

Then you can seed regtest using either qtum-cli or Janus
  - note that fromhexaddress requires dropping the hex prefix 0x
  - Qtum block rewards need to be at least 2000 blocks old to be used

```bash
# Get base58 address from hex
docker exec qtumd_regtest \
  qtum-cli \
  -rpcuser=qtum \
  -rpcpassword=testpasswd \
  fromhexaddress 63c4953002B935C3CA925af419DFCE86C057AB95

> qSeuYqETzKqcVn3seaTRQ1U8jcaR1QHYQj

# Seed regtest with Qtum
docker exec qtumd_regtest \
  qtum-cli \
  -rpcuser=qtum \
  -rpcpassword=testpasswd \
  generatetoaddress 2005 qSeuYqETzKqcVn3seaTRQ1U8jcaR1QHYQj

# Or do it in one command
docker exec qtumd_regtest \
  qtum-cli \
  -rpcuser=qtum \
  -rpcpassword=testpasswd \
  generatetoaddress 2005 `\
    docker exec qtumd_regtest \
      qtum-cli \
      -rpcuser=qtum \
      -rpcpassword=testpasswd \
      fromhexaddress 63c4953002B935C3CA925af419DFCE86C057AB95`
```

Or you can use `dev_generatetoaddress` Janus RPC call to do this
 - note that generating this many blocks will cause Janus to timeout waiting for a response from Qtum, but Qtum will still generate the blocks

```bash
# Directly calling dev_generatetoaddress via Curl
curl --location --request POST 'http://localhost:23889' \
  --header 'Content-Type: text/plain' \
  --data-raw '{
    "method": "dev_generatetoaddress",
    "params": [
      2005,
      "63c4953002B935C3CA925af419DFCE86C057AB95"
    ]
  }'

# response
{"jsonrpc":"2.0","result":["1369920b45f482096b2159788c2f1cd576b0e37affc176df07904d8a841f8590", ...]}
```

# truffle migrate

Now that your local regtest environment has Qtum we can deploy code with truffle

```bash
truffle migrate --network regtest

Compiling your contracts...
===========================
✔ Fetching solc version list from solc-bin. Attempt #1
> Everything is up to date, there is nothing to compile.



Starting migrations...
======================
> Network name:    'regtest'
> Network id:      8890
> Block gas limit: 40000000 (0x2625a00)


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x867d80074f084e27ae2828dea3bd6384d18d4dd3e8a20bafefa1578dff38a726
   > Blocks: 0            Seconds: 0
   > contract address:    0x676BC04885F727b393b7d8788E54f0BC47888b0c
   > block number:        2008
   > block timestamp:     1657302875
   > account:             0x63c4953002B935C3CA925af419DFCE86C057AB95
   > balance:             40099999.836968
   > gas used:            130690 (0x1fe82)
   > gas price:           400 gwei
   > value sent:          2.690858 ETH
   > total cost:          2.743134 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:            2.743134 ETH


2_deploy_contracts.js
=====================

   Deploying 'SimpleStorage'
   -------------------------
   > transaction hash:    0x7e3fa9e99d9954820bf2f12f4335b5dbf19a1bab409a096de61e526225ca60d2
   > Blocks: 0            Seconds: 0
   > contract address:    0xa9052BAfE2d784990F8a99ED69dcB11c147B084C
   > block number:        2010
   > block timestamp:     1657302877
   > account:             0x63c4953002B935C3CA925af419DFCE86C057AB95
   > balance:             40099999.779758
   > gas used:            90527 (0x1619f)
   > gas price:           400 gwei
   > value sent:          2.690442 ETH
   > total cost:          2.7266528 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:           2.7266528 ETH


Summary
=======
> Total deployments:   2
> Final cost:          5.4697868 ETH
```

Artifacts will be in `build/contracts/*.json`

```
tail -n 22 build/contracts/*.json            
==> build/contracts/Migrations.json <==
  "networks": {
    "8890": {
      "events": {},
      "links": {},
      "address": "0x676BC04885F727b393b7d8788E54f0BC47888b0c",
      "transactionHash": "0x867d80074f084e27ae2828dea3bd6384d18d4dd3e8a20bafefa1578dff38a726"
    }
  },
  "schemaVersion": "3.3.4",
  "updatedAt": "2022-07-08T17:54:38.284Z",
  "networkType": "ethereum",
  "devdoc": {
    "kind": "dev",
    "methods": {},
    "version": 1
  },
  "userdoc": {
    "kind": "user",
    "methods": {},
    "version": 1
  }
}
==> build/contracts/SimpleStorage.json <==
  "networks": {
    "8890": {
      "events": {},
      "links": {},
      "address": "0xa9052BAfE2d784990F8a99ED69dcB11c147B084C",
      "transactionHash": "0x7e3fa9e99d9954820bf2f12f4335b5dbf19a1bab409a096de61e526225ca60d2"
    }
  },
  "schemaVersion": "3.3.4",
  "updatedAt": "2022-07-08T17:54:38.282Z",
  "networkType": "ethereum",
  "devdoc": {
    "kind": "dev",
    "methods": {},
    "version": 1
  },
  "userdoc": {
    "kind": "user",
    "methods": {},
    "version": 1
  }
}%
```