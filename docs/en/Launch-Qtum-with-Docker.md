# How to run Qtum node with docker

## Quick start

This tutorial use Linux Ubuntu as example, OSX and windows platform are almost the same.

Suppose the reader has basic command line knowledge, and also have docker correctly installed and configured. If not, please learn about command line and Docker first.

For more details, please refer to [github](https://github.com/qtumproject/qtum-docker.git)

## Get docker image

You might take either way:

### Pull a image from Public Docker hub

```
$ docker pull qtum/qtum
```

### Or, build qtum image with provided Dockerfile

The Dockerfile can be downloaded on github: [Dockerfile](https://github.com/qtumproject/qtum-docker/blob/master/release/Dockerfile)

```
$docker build --rm -t qtum/qtum .
```

For historical versions, please visit [docker hub](https://hub.docker.com/r/qtum/qtum/)

## Prepare data path and qtum.conf

In order to use user-defined config file, as well as save block chain data, -v option for docker is recommended.

First chose a path to save qtum block chain data:

```
sudo rm -rf /data/qtum-data
sudo mkdir -p /data/qtum-data
sudo chmod a+w /data/qtum-data
```

Create your config file, refer to the example [qtum.conf]!(https://github.com/qtumproject/qtum/blob/1a926b980f03e97322c7dd787835bec1730f35d2/contrib/debian/examples/qtum.conf). Note rpcuser and rpcpassword to required for later `qtum-cli` usage for docker, so it is better to set those two options. Then please create the file ${PWD}/qtum.conf with content:

```
rpcuser=qtum
rpcpassword=qtumtest
```
## Launch qtumd

To launch qtum node:

```
## to launch qtumd
$ docker run -d --rm --name qtum_node \
             -v ${PWD}/qtum.conf:/root/.qtum/qtum.conf \
             -v /data/qtum-data/:/root/.qtum/ \
             qtum/qtum qtumd

## check docker processed
$ docker ps

## to stop qtumd
$ docker run -i --network container:qtum_node \
             -v ${PWD}/qtum.conf:/root/.qtum/qtum.conf \
             -v /data/qtum-data/:/root/.qtum/ \
             qtum/qtum qtum-cli stop
```

`${PWD}/qtum.conf` will be used, and blockchain data saved under /data/qtum-data/

## Interact with `qtumd` using `qtum-cli`

Use following docker command to interact with your qtum node with `qtum-cli`:

```
$ docker run -i --network container:qtum_node \
             -v ${PWD}/qtum.conf:/root/.qtum/qtum.conf \
             -v /data/qtum-data/:/root/.qtum/ \
             qtum/qtum qtum-cli getinfo
```

For more qtum-cli commands, use:

```
$ docker run -i --network container:qtum_node \
             -v ${PWD}/qtum.conf:/root/.qtum/qtum.conf \
             -v /data/qtum-data/:/root/.qtum/ \
             qtum/qtum qtum-cli help
```
