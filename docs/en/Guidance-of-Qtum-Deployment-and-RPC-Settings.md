# How to deploy a Qtum node

This guidance includes how to deploy, run and make RPC calls.

Suppose the readers are able to use Linux,Mac or Windows command line. If you are not familiar with command line, or just interested in using GUI wallet, please refer to another document about [Qtum Wallet Tutorial](Qtum-Wallet-Tutorial.md).

## Get Qtum Node

There are at least 4 ways to get a Qtum node, you can choose any way：

**1. Download the binaries**

If you do not care much about Qtum's source code, the easiest way to abtain Qtum node is to download the latest binaries on the [Qtum release page](https://github.com/qtumproject/qtum/releases). Currently it supports Linux, Window, OSX. It is highly recommanded to download the latest version. In this guidance, we will use v0.14.13 version as an example。

（Note: the version number you see might be different, here is v0.14.13, but other key words except for version are the same.）

* For **Mac** user：`qtum-0.14.13-osx64.tar.gz`
* For **Linux** users： `qtum-0.14.13-i686-pc-linux-gnu.tar.gz`(32bit) or `qtum-0.14.13-x86_64-linux-gnu.tar.gz`(64bit)
* For **Windows** users：`qtum-0.14.13-win32.zip`(32bit) or `qtum-0.14.13-win64.zip`（64bit）
* For **Raspberry Pi**：`qtum-0.14.13-arm-linux-gnueabihf.tar.gz`

Decompress after downloading, then you will get `qtumd` and `qtum-cli` under the path `<your path>/bin`.


**2. apt install for Linux users**

Please refer to [https://github.com/qtumproject/qtum/wiki/Setting-up-QTUM-Ubuntu,-Debian-and-Mint-repository](https://github.com/qtumproject/qtum/wiki/Setting-up-QTUM-Ubuntu,-Debian-and-Mint-repository)，Current support Ubuntu，Debian and Mint。

Raspberry Pi users can also use apt，please refer to [https://github.com/qtumproject/qtum/wiki/Installing-Qtum-on-Raspberry-Pi](https://github.com/qtumproject/qtum/wiki/Installing-Qtum-on-Raspberry-Pi)。

After installation, you should be able to run `qtumd` and `qtum-cli`directly in the terminal。

**3. Compiler from source code**

If you want to compile latest Qtum from source code, please pull the latest source from github : [https://github.com/qtumproject/qtum](https://github.com/qtumproject/qtum)。

The instruction for compilation : [https://github.com/qtumproject/qtum/blob/master/README.md](https://github.com/qtumproject/qtum/blob/master/README.md)。Currently we recommand to compile on Linux or OSX, while other platforms might need more configuration.

After compilation, you also get `qtumd` and `qtum-cli` under the path `<your path>/src/`

**4. Get Qtum node docker image**

Suppose user has docker environment installed correctly. ([what is docker?]())

The Qtum official docker image on docker hub is `qtum/qtum`, you can pull it by docker command ：

```
docker pull qtum/qtum:latest
```

All the four ways above cand get Qtum nodes. There are two important binaries which are related to deployment and RPC calls:

* `qtumd`：Qtum core program, i.e. Qtum fullnode program.
* `qtum-cli`：Qtum command line interface，interact with qtumd, achieve RPC calls.

## Deploy Qtum node

For the instruction for Qtum docker images, please refer to "[How to launch Qtum with docker](https://github.com/qtumproject/documents/blob/master/zh/Launch-Qtum-with-Docker.md)".

Other normal deployment methods are almost the same, here we take Ubuntu as an example. The commands in Mac and windows are exactly the same.


Run Qtum fullnode with `./qtumd`：

```
./qtumd -daemon
```

This with launch a qtumd daemon with the option `-daemon`. If user are interested in the event logs about smart contract, please add one more option `-logevents`. 

 More options can be found：

```
./qtumd -help
```

To stop running：

```
./qtum-cli stop
```

The default data path for different platforms:

* Linux：`~/.qtum/`
* Mac OSX：`~/Library/Application Support/Qtum`
* Windows:`%APPDATA%\Qtum`

You can also use `-datadir` to set your own data path。

Qtum node will sync all the historical block data for first launch, and saves to datadir. It might take some time. Then diagnostics for the node can be found under the data path `~/.qtum/debug.log`。

## Local RPC call

When the qtum node is running, we can use qtum command line interface `qtum-cli` to interact with `qtumd`, and make local RPC calls.

e.g.：

```
oldclock@raven:~/qtum-0.14.3/bin$ ./qtum-cli getinfo
{
  "version": 140300,
  "protocolversion": 70016,
  "walletversion": 130000,
  "balance": 0.00000000,
  "stake": 0.00000000,
  "blocks": 12126,
  "timeoffset": 0,
  "connections": 8,
  "proxy": "",
  "difficulty": {
    "proof-of-work": 1.52587890625e-05,
    "proof-of-stake": 886731.5868738915
  },
  "testnet": false,
  "moneysupply": 100028504,
  "keypoololdest": 1505186997,
  "keypoolsize": 100,
  "paytxfee": 0.00000000,
  "relayfee": 0.00400000,
  "errors": ""
}

```

To get all RPC command list:

```
./qtum-cli help
```

To get help for specific RPC command, use `./qtum-cli help <RPCcmd>`，e.g.：

```
./qtum-cli help getinfo
```
## JsonRPC settings

You can get the jsonrpc example by using (here we use `getinfo` as an example): `./qtum-cli help getinfo`

```
Examples:
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:3889/
```

The example shows detailed format for jsonrpc content. However, it can only be called after setting `rpcuser` and `rpcpassword`. There are two ways to set the parameters, you can choose either.

Method 1：Create config file `~/.qtum/qtum.conf`，which should include:

```
rpcuser=test  #rpc user name, (necessary)
rpcpassword=test1234  #rpc password, (necessary)
# By default, only local jsonrpc is allowed
# Remote connection is allowed only when setting rpcallowip as following:
# both ipv4 and ipv6 can be set, e.g.:
#rpcallowip=192.168.77.51/255.255.255.0
#rpcallowip=1.2.3.4/24
#rpcallowip=2001:db8:85a3:0:0:8a2e:370:7334/96
```

For more config settings, please refer to ：[qtum.conf example](https://github.com/qtumproject/qtum/blob/1a926b980f03e97322c7dd787835bec1730f35d2/contrib/debian/examples/qtum.conf)

After creating the config file, please restart the node to finish settings.

Method 2：Restart Qtum node with following options:

```
./qtumd -daemon -rpcuser=test -rpcpassword=test1234 -rpcallowip=192.168.77.51/255.255.255.0
```

The meaning of options `rpcuser`, `rpcpassword` and `rpcallowip` are all the same with the config file above. 

## RPC call example

You can make remote RPC calls after the settings above. Here is an example: Suppose the qtum node is running on an Ubuntu machine, whose ip is 192.168.77.188, default port=3889. Now we try to make jsonrpc call in a remote macbook:

```
zhongwenbins-MacBook-Pro:~ zhongwenbin$ curl --user test:test1234 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo", "params": [] }' -H 'content-type: text/plain;' http://192.168.77.188:3889/
{"result":{"version":140300,"protocolversion":70016,"walletversion":130000,"balance":0.00000000,"stake":0.00000000,"blocks":12197,"timeoffset":0,"connections":8,"proxy":"","difficulty":{"proof-of-work":1.52587890625e-05,"proof-of-stake":650787.7561123729},"testnet":false,"moneysupply":100028788,"keypoololdest":1505186997,"keypoolsize":100,"paytxfee":0.00000000,"relayfee":0.00400000,"errors":""},"error":null,"id":"curltest"}
```

The result is identical with local call.


You can also use tools like postman to get the same result：

![postman截图](https://s.qtum.site/uploads/e7398325af231cf42a708303af2a5098.png)


## Nginx settings（optional）

As the example above, you might find that it is quite complicated to make remote  jsonrpc, since you must include rpcuser, rpcpassword, as well as port in the command. If you don't want users to provide these parameters, we recommand using Nginx. The benefits for Nginx is not only about simplification, but also a good way to hide rpcuser, rpcpassword and port number. And you can filter some RPCs for security. Here we suppose the reader have installed Nginx and have basic knowledges about how to use it.

example:

* Qtum node is running on `192.168.77.188`,
* api proxy ip `192.168.77.51`, with Nginx installed

Instructions：

1.Set the `qtum.conf` of qtum node, remember to add the proxy ip to rpcallowip e.g.：

```
rpcuser=test
rpcpassword=test1234
rpcallowip=192.168.77.51/255.255.255.0
```

2.Setup Nginx ：

```
    server {
        listen       80;
        server_name  localhost;

        location / {
            proxy_pass http://192.168.77.188:3889;  #to port 3889
            proxy_set_header Authorization "Basic dGVzdDp0ZXN0MTIzNA==";  # its the base64 encode of test:test1234
        }
    }
```

3.Then you can make remote rpc call through proxy, without rpcuser or rpcpassword. e.g.：

```
zhongwenbins-MacBook-Pro:~ zhongwenbin$ curl  --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo", "params": [] }' -H 'content-type: text/plain;' http://192.168.77.51/
{"result":{"version":140300,"protocolversion":70016,"walletversion":130000,"balance":0.00000000,"stake":0.00000000,"blocks":12250,"timeoffset":0,"connections":8,"proxy":"","difficulty":{"proof-of-work":1.52587890625e-05,"proof-of-stake":651324.7815933984},"testnet":false,"moneysupply":100029000,"keypoololdest":1505186997,"keypoolsize":100,"paytxfee":0.00000000,"relayfee":0.00400000,"errors":""},"error":null,"id":"curltest"}
```

This is only a simple example. You might have different settings or tools instead.

## Useful commands and documents

If you have any questions during node deployment and RPC calls, here are some useful documents to refer to:

* For source code compilation issues： [https://github.com/qtumproject/qtum/blob/master/README.md](https://github.com/qtumproject/qtum/blob/master/README.md)。
* Command to check all qtumd options：`./qtumd -help`
* Command to get all RPC list： `./qtum-cli help`
* Get RPC help（like getinfo）： `./qtum-cli help getinfo`
* qtum.conf file example：[qtum.conf](https://github.com/qtumproject/qtum/blob/1a926b980f03e97322c7dd787835bec1730f35d2/contrib/debian/examples/qtum.conf)
