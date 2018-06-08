# QTUM 区块链测试网络使用指南

## 1. 下载安装主网钱包
请参考 [Guidance-of-Qtum-Deployment-and-RPC-settings](https://github.com/qtumproject/documents/blob/master/zh/Guidance-of-Qtum-Deployment-and-RPC-settings.md) 中“获取Qtum节点”的部分。

## 2. 启动测试网络
使用命令 `./qtumd --testnet` 或者 `./qtum-qt --testnet` 启动程序即可进入测试网络模式。

## 3. 获取测试币
访问 [测试网络水龙头](https://testnet-faucet.qtum.info/)，输入钱包地址领取测试币。

## 4. 测试网络浏览器
[https://testnet.qtum.org/](https://testnet.qtum.org/)  
[https://testnet.qtum.info/](https://testnet.qtum.info/)

## 5. 回归测试模式
使用命令 `./qtumd --regtest ` 或者 `./qtum-qt --regtest` 启动程序即可进入回归测试模式。

通过运行 `./qtum-cli --regtest generate [num]` 可以生成新的区块。





