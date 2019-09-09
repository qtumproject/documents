# How To Build Qtum On Raspbian

Qtum is capable to run on small devices, it requires quite few CPU power, memory and storage to mine coins. But the binaries released by Qtum official are not suitable for Raspberry Pi Zero or First Generations. Here is a tutorial on how to build Qtum on a raspi. In this tutorial, we assume that you are using a raspbian system.

## System Requirements

Generally, a raspi is capable to build qtum, but we need:

 - an SD card with at least 8G space and at least 6G available;
 - Internet connection is also required.

## Memory Requirements

Qtum requires quite few memory to run. However it is not true for building Qtum. It requires over 1.5G memory to build, which is much more than a raspi has. So we have to set the swap space to 2G:

```bash
# modify swap size to at least 2GB
sudo sed -ri 's/CONF_SWAPSIZE=[0-9]+/CONF_SWAPSIZE=2048/' /etc/dphys-swapfile
sudo systemctl restart dphys-swapfile
```

## Build Process

### Install Dependencies

We cat install building tools and most dependencies with apt:

```
# install dependencies
sudo apt-get install git autoconf libtool libboost-dev libboost-system-dev libboost-filesystem-dev libboost-thread-dev libboost-chrono-dev libboost-random-dev libssl-dev libevent-dev libboost-test-dev
```

If you need the Qt GUI, additionally run:

```
sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler qrencode
```

### Prepare Building Folder

```
mkdir build_qtum
cd build_qtum
```

### Build Berkeley DB Dependency

Unfortunately we can't install Berkeley DB 4.8 dependency on a raspbian via apt, so we need to build it ourselves:

```
# to build berkeley db 4.8
wget http://download.oracle.com/berkeley-db/db-4.8.30.tar.gz
tar -xzf db-4.8.30.tar.gz
pushd db-4.8.30/build_unix
../dist/configure --prefix=/usr/local --enable-cxx
make # this would take around 50 minutes on a raspi 0 W
sudo make install
popd
```

### Build Qtum

First we have to get the source:

```
git clone https://github.com/qtumproject/qtum.git
cd qtum
```

Then we should switch to a stable release tag, for now the latest release for Qtum is `mainnet-ignition-v0.17.5`, but you should always build a latest one.

```
git checkout mainnet-ignition-v0.17.5
```

Then init submodules:

```
git submodule update --init --recursive
```

Finally the most common way to build and install a software:

```
./autogen.sh
./configure
make
sudo make install
```

It is highly recommended that you run the `make` step inside a virtual console like `screen` or `tmux` because the step takes more than 20 HOURS. By using a virtual console, you don't need to keep the ssh session during its building. To do this, run these commands before `make`:

```
sudo apt-get install screen
screen -S build
```

And when you started making, you may leave the screen by pressing <kbd>Ctrl</kbd> + <kbd>A</kbd> then <kbd>D</kbd>, and you may go back to it with this command:

```
screen -R
```

Boom! Now you have Qtum installed on your raspi!
