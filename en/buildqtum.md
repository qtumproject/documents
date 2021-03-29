# Building Qtum Core

### Installing dependencies (This will work for Ubuntu and Debian)

```bash
sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git cmake libboost-all-dev libgmp3-dev
```

## Compiling Qtum Core from source

### From Github source:



```bash
git clone https://github.com/qtumproject/qtum --recursive
cd qtum && make -C depends/
DEPENDS="$(pwd)/depends/x86_64-pc-linux-gnu"
./autogen.sh
./configure --prefix=$DEPENDS
make
make install
```

This will install all the Qtum binaries on `depends/x86_64-pc-linux-gnu`

### From a release file:

```bash
wget https://github.com/qtumproject/qtum/archive/refs/tags/mainnet-fastlane-v0.20.2.tar.gz
tar -xpf mainnet-fastlane-v0.20.2.tar.gz && cd qtum-mainnet-fastlane-v0.20.2 
git clone --recursive https://github.com/qtumproject/cpp-eth-qtum.git src/cpp-ethereum
make -C depends/
DEPENDS="$(pwd)/depends/x86_64-pc-linux-gnu"
./autogen.sh
./configure --prefix=$DEPENDS
make
make install
```

This will install all the Qtum binaries on `depends/x86_64-pc-linux-gnu`

## Running Qtum Core

Type from a terminal: 

`qtumd -daemon`

Also, make sure to create a qtum.conf with your credentials if needed for accessing RPC calls.

This is a sample qtum.conf file

```bash
rpcuser=qtum
rpcassword=coin
server=1
rpcallowip=127.0.0.1
logevents=1
daemon=1
```


# QRC20 Tokens on Qtum Core

## Enabling Log events

add `logevents=1` to the qtum.conf file before launching the daemon

Run Qtum like this:

`qtumd -daemon -logevents -txindex=1`

If Qtum has already synced, you'll need to reindex blocks:

`qtumd -daemon -reindex` 

## QRC20 token deep dive

https://docs.qtum.site/en/Raw-QRC20-Transaction-implementation-guide

https://docs.qtum.site/en/QRC20-integration.html

