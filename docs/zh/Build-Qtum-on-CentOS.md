# 在CentOS 7上编译Qtum

在CentOS上编译Qtum是一件非常麻烦的事情，因为CentOS提供的`boost`库过于老旧。而我们需要自己去手动编译`boost`库。

## 准备工作

添加`epel-release`仓库，然后安装一些编译工具：

```bash
sudo yum install epel-release gcc-c++ git
```

## 编译Boost

我们需要至少`1.58.0`版本的`boost`库来编译Qtum，但是CentOS 7上只提供了`1.53.0`版本以下的`boost`，我们可以选择手动编译。

首先我们需要安装一些依赖:

```bash
sudo yum install python-devel bzip2-devel
```

然后我们从GitHub上克隆`boost`库：

```bash
git clone https://github.com/boostorg/boost.git
cd boost
```

检出一个发布版本并且初始化子模块：

```bash
git checkout boost-1.58.0
git submodule update --init --recursive
```

编译Boost：
你可以把`--prefix`和`--libdir`设置为任意你想要的位置，或者保持默认。但是你需要在编译和运行Qtum的时候把*libdir* 添加到`LD_LIBRARY_PATH`环境变量中，多少有些麻烦。

```bash
# omit the --libdir option for 32-bit systems
./bootstrap.sh --prefix=/usr --libdir=/usr/lib64
./b2 headers
# 你可以设置-j<N>，其中N是你的电脑的CPU的核心数或线程数。
sudo ./b2 -j4 install
```

## 编译Qtum

安装依赖：

```bash
sudo yum install libtool libdb4-cxx-devel openssl-devel libevent-devel
```

如果你需要编译Qtum图形化界面`qtum-qt`，你还需要安装这些依赖：

```bash
sudo yum install qt5-qttools-devel protobuf-devel qrencode-devel
```

克隆仓库并且初始化子模块：

```bash
git clone https://github.com/qtumproject/qtum.git
cd qtum
git submodule update --init --recursive
```

配置参数以及编译：  
如果你把boost安装到了`/`, `/usr`, `/usr/local`以外的路径，你需要在`configure`的时候指定`--with-boost=/path/to/your/boost`，以及把`/path/to/your/boost/lib`添加到`LD_LIBRARY_PATH`环境变量。

```bash
./autogen.sh
./configure
make -j4
```

