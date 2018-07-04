# Qtum如何添加运行选项（或配置文件）

Qtum钱包程序除默认设置外，还可以通过添加运行选项或配置文件实现特定的功能或运行模式。

## PC版钱包用户（Qtum Core钱包）

大多数用户最常用的钱包是Qtum Core钱包，即Qtum官方的PC版钱包。（还未下载钱包？可从[https://qtumeco.io/wallet](https://qtumeco.io/wallet)下载最新版钱包）

PC版钱包用户可以通过配置文件修改钱包配置。方法如下：

### 1. 创建`qtum.conf`文件

在datadir路径下创建名为`qtum.conf`的文件，不同系统的默认的datadir路径稍有不同：

* Linux: ~/.qtum
* OSX: ~/Library/Application Support/Qtum
* Windows: %APPDATA%\Qtum (把这个路径复制粘贴到浏览器地址栏，会自动解析出路径所在，之后再打开这个路径即可)

（注：datadir路径也可以设置，但默认为上述路径。如果你设置了datadir路径，请在你设置的路径下进行以下操作）

### 2. 写入所需配置信息

在上述创建的新文件`qtum.conf`中写入配置信息。

例如，如果需要配置rpc调用信息，可以在文件中写入：

```
rpcuser=test
rpcpassword=test1234
server=1
```

上述配置设置rpc调用的用户名为test，密码为test1234，并开启了server功能。

### 3. 重新启动钱包

重启钱包，配置文件即可生效。

### 其他选项

感兴趣的读者如果想了解其他所有可用的配置信息及其含义，可以通过钱包查看：

打开钱包菜单栏的`Help->Command-line Options`，即可查看所有可用配置选项。

![Help Command-line Options](./Help-Comman-line-options.jpg)

![Command-line Options](./Command-line-options.jpg)

## 命令行钱包`qtumd`

不使用命令行模式的用户请忽略本小节内容。

对于熟悉命令行模式的用户或开发者，除上述添加配置文件的方式外，还可以直接通过命令行选项实现配置。

例如：

```
./qtumd -rpcuser=test -rpcpassword=test1234
```

该例子中的选项`-rpcuser=test -rpcpassword=test1234`实现了与上面提到的配置文件相同的配置。

需要注意的是，如果采用命令行选项运行Qtum节点（`qtumd`），则在运行`qtum-cli`时也需要添加相同的选项，例如对于上述的`qtumd`，对应的`qtum-cli`命令为：

```
./qtum-cli -rpcuser=test -rpcpassword=test1234 getinfo
```

### 命令行模式查看所有选项

用户可以通过一下命令查看所有可用选项：

```
./qtumd -help
```




