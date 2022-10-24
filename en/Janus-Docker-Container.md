# Janus Docker Container

First, download the Janus docker image

```
docker pull qtum/janus:latest
```

To setup a Janus docker container we need to configure a network bridge for it to talk to the Qtum blockchain

```
docker network create --driver bridge qtum
```

Then we need to startup the Qtum blockchain and configure it to use the network

```
docker run --network=qtum -it --rm \
  --name qtumd_regtest \
  -v `pwd`:/root \
  -p 23888:23888 \
  -p 3889:3889 \
  qtum/qtum \
  qtumd -regtest -txindex -addrindex=1 -logevents \
  -rpcbind=0.0.0.0:3889 -rpcallowip=0.0.0.0/0 -rpcuser=qtum -rpcpassword=testpasswd
```

And finally, launch Janus configured to use the network as well

```
docker run --network=qtum -it --rm \
  --name janus_regtest \
  -v `pwd`:/root \
  -p 23889:23889 \
  qtum/janus:latest \
  --bind 0.0.0.0 --dev --qtum-rpc=http://qtum:testpasswd@qtumd_regtest:3889
```


