# Build Qtum on CentOS 7

CentOS is an enterprise-oriented Linux distribution, that means it's focused for stability and security but not necessarily the latest software. With that being said, you *cannot* currently build Qtum in CentOS 7 following the steps that other more recent distributions can use. 

In this document we'll show how to build Qtum in CentOS 7 and produce a **static binary** which can then be executed on any other Linux distribution, even if it's more recent. 

## General Prerequisites

Update Yum repositories 

```bash
	sudo yum update 
```

## Install development tools and libraries

Getting ready:

```bash
sudo yum install -y tar unzip git which wget patch make autoconf automake libtool \
	epel-release centos-release-scl centos-release-scl-rh finduitls vim mc openssl-devel \
	file
```

Enable Devtoolset-7

```bash
yum install -y devtoolset-7-gcc* && \
	echo "source scl_source enable devtoolset-7" >> /root/.bashrc
source scl_source enable devtoolset-7
```

Clone Qtum Github source:

```bash
git clone --recurse-submodules --depth 1 https://github.com/qtumproject/qtum
```

## Building Qtum

```bash
cd qtum && make -C depends/
DEPENDS="$(pwd)/depends/x86_64-pc-linux-gnu"
./autogen.sh
./configure --prefix=$DEPENDS
make
```

Please keep in mind, this will produce a **static build** and it will take longer than a normal build. 