# Build Qtum on CentOS 7

It is quite a pain to build Qtum on CentOS because CentOS provides quite old versions of the `boost` library. Actually We need to build the `boost` library manually.

## General Prerequisites

Add `epel-release` repo and install some utils:

```bash
sudo yum install epel-release gcc-c++ git
```

## Building Boost

We need `boost >= 1.58.0` for qtum but CentOS 7 only provides `boost <= 1.53.0`, one way is to build it manually.

First we install some dependencies:

```bash
sudo yum install python-devel bzip2-devel
```

Then we clone the boost library from github:

```bash
git clone https://github.com/boostorg/boost.git
cd boost
```

Checking out a release version and init submodules:

```bash
git checkout boost-1.58.0
git submodule update --init --recursive
```

Building boost:  
You may set the `--prefix` and `--libdir` to anywhere you like or even leave it by default, but then you have to add the *libdir* into `LD_LIBRARY_PATH` env when building and running Qtum, which is annoying somehow.

```bash
# omit the --libdir option for 32-bit systems
./bootstrap.sh --prefix=/usr --libdir=/usr/lib64
./b2 headers
# you may set -j<N> where N is the core number or thread number of your CPU.
sudo ./b2 -j4 install
```

## Building Qtum

Install dependencies:

```bash
sudo yum install libtool libdb4-cxx-devel openssl-devel libevent-devel
```

If you need to build the `qtum-qt` GUI, install these:

```bash
sudo yum install qt5-qttools-devel protobuf-devel qrencode-devel
```

Cloning the project and init submodules:

```bash
git clone https://github.com/qtumproject/qtum.git
cd qtum
git submodule update --init --recursive
```

Configuring and building:  
If you have installed boost to any location other than `/`, `/usr`, `/usr/local`, you need to indicate the location with `--with-boost=/path/to/your/boost`, and add `/path/to/your/boost/lib` into `LD_LIBRARY_PATH` env

```bash
./autogen.sh
./configure
make -j4
```

