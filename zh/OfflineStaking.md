# Offline Staking

* [将地址委托给Super Staker](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#将地址委托给super-staker)
* [委托地址操作](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#委托地址操作)
* [配置Super Staker](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#配置super-staker)
* [以Super Staker身份登录Qtum Core](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#以super-staker身份登录qtum-core)
* [qtumd Super Staker](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#qtumd-super-staker)
* [Super Staker操作](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#super-staker操作)
* [恢复](https://github.com/qtumproject/documents/tree/master/zh/Qtum-Wallet-Tutorial#恢复)

# 将地址委托给Super Staker

Qtum Offline Staking允许未staking的钱包地址（可以进行委托任务转账）被委托给Super Staker。Offline Staking无需托管，委托用户对自己的资产和私钥有完全的控制权。地址委托通过一次来自委托用户钱包的智能合约转账实现，在这个过程中委托者的地址、Super Staker的地址和委托者同意支付的费用都在转账中有所体现。如果Super Staker接受该费率，它将会开始为委托地址的UTXO进行staking。

委托的UTXO遵循与普通stakingUTXO同样的规则：

* UTXO只有在成熟（达到500个区块的确认）之后才能被用于staking。
* Super Staker将会设置一个stake的最小UTXO限制，默认为100 QTUM。低于该值的委托UTXO将被忽略。
* 从回报角度来看，委托UTXO的最佳值在100-200 QTUM之间。对于Qtum Core钱包的用户来说，可以通过`splitutxosforaddress`命令实现UTXO的拆分。细节请见下文。

如果想从Qtum Core钱包进行委托操作，您可以在"Stake"中选择"委托"，然后点击右上角的"+"按钮添加委托。之后，输入Staker名（为了方便辨识）、Staker地址、想要支付的费用比例和您想要委托的地址。如果您对Gas费用没有特别要求，请使用默认设置。委托转账需要至少0.9QTUM作为费用，多余的费用将被退还。

![1  Add Delegation Assignment - CN](https://user-images.githubusercontent.com/29760787/85623682-ca7e8580-b636-11ea-8b92-2fd1fe735897.jpg)

点击"确认"和"是"发送委托转账。

委托也可以通过Qtum Electrum钱包完成，同时支持Ledger硬件钱包地址。

# 委托地址操作

委托地址转账会被发送到一个智能合约中，该合约将记录委托任务，Super Staker也将从合约处领取任务。您将可以在钱包或浏览器[qtum.info](https://qtum.info/)中查看委托地址的区块奖励转账。

如果一个钱包的QTUM存在多个地址中，每个地址必须单独委托（转账费也必须单独支付）。因此，把UTXO合并到一个地址中再拆分委托可能更符合委托者的利益。在这种情况下，可以手动将不同地址的币合并到一个地址中。另一种方式是使用`sendmanywithdupes`命令，该命令可以将钱包内所有余额以合适的UTXO值发送到一个新地址内。

如果Super Staker接受了某一费率的一项委托，之后该Super Staker又降低了自己的费率标准（接受更低费率的委托任务），委托者如果也想享受该更低的费率，就必须重新设定费率，重新进行委托。

某个钱包的委托可以在"Stake"页的"委托"选项中查看，或者使用`getdelegationinfoforaddress`命令。

请保存一份wallet.dat文件以备份钱包。

# 配置Super Staker

Qtum Core钱包提供了在线的PoS共识，因此登录、配置该钱包之后就可以作为Super Staker进行操作、接受其他地址的委托。

如果想在Qtum-Qt钱包中配置成为Super Staker，请在"Stake"页面选择"Super Staker"，然后选择"+"以添加一个新的Super Staker。输入Staker名（仅作为本地识别使用，此处示例中使用地址的第一部分，并用"10"表示10%的费用），之后从下拉菜单中选择Staker地址。

![2  Super Staker Setup CN](https://user-images.githubusercontent.com/29760787/85623694-ce120c80-b636-11ea-9aa2-8587900c6abf.jpg)

作为Super Staker，钱包必须能够检查任意地址（地址索引）、启用日志以便操作智能合约（日志事件）并开启Staking选项。这三项设置可以通过设置`-superstaking`参数实现。设置`-superstaking`之后首次登录钱包时，钱包将重新扫描区块链以构建包含地址索引和日志事件的数据库。

下一步，钱包将提示您在"设置"-"选项"-"开启Super Staking"，确认之后钱包将重新启动。

![3  Qtum-Qt Enable Super Staker CN](https://user-images.githubusercontent.com/29760787/85623709-d407ed80-b636-11ea-8d6a-a1ea83dde656.jpg)

重启之后，钱包将向您确认是否要扫描区块链以便重建数据库。

![4  Rebuild the Database CN](https://user-images.githubusercontent.com/29760787/85623718-d5d1b100-b636-11ea-988f-762fb36bf926.jpg)

钱包将显示"正在硬盘上重新索引区块"以及在重建数据库时显示"同步区块头"。这可能需要几十分钟，具体时间取决于您的计算机配置。

登录之后，返回"Stake"-"Super Staker"页面，选择"设置Super Staker"按钮（现在将能显示齿轮标志）以完成Super Staker配置。点击定制按钮查看默认配置，或更改配置。点击确认完成设置。

![5  Super Staker Options CN](https://user-images.githubusercontent.com/29760787/85623722-d8340b00-b636-11ea-8829-d6c5ad2fbbbe.jpg)

配置选项包括：

* 最低费用 - Staker将会接受的最低委托费率。
* 最小UTXO值 - 设定了该Staker将接受的用于PoS共识的最小的UTXO。随着时间推进，委托地址将有许多小额区块奖励UTXO，管理这些小额UTXO将很低效（委托者应该将这些UTXO合并）。
* 委托列表类型：
  * 接受所有 - 接受所有高于最低费率的委托。
  * 允许列表 - 只接受来自特定地址的委托。使用该模式将使Super Staker只能为特定地址服务，比如只为自己的币进行Staking。
  * 排除列表 - 不接受来自列表内的地址的委托。

接下来，Super Staker将把UTXO分解成有效大小进行Staking。进行Staking的UTXO最小值为100QTUM。在Super Staker页面可以选择拆分按钮（三叉戟图标），拆分可以使用默认值或自行调整，但能用于Staking的UTXO最小值为100QTUM。

![6  Split UTXOs GUI CN](https://user-images.githubusercontent.com/29760787/85623727-d9fdce80-b636-11ea-8502-ff453d6140ce.jpg)

你也可用使用`splitutxosforaddress`命令拆分UTXO。委托地址也可用使用该功能。如果想将UTXO拆分为最小值（minValue）和最大值（maxValue）之间的值，可用使用如下命令：

`splitutxosforaddress "address" minValue maxValue ( maxOutputs )`

例如，如果一个钱包内有数量为40、50、60、70和800QTUM的几个UTXO，要把这些UTXO拆分为最小100最大200的UTXO，可用使用如下命令：

```splitutxosforaddress
{
  "txid": "197a199c3ac9dd8df574ca77da15c5da31db3f7101e2108638a3b2f94248b9f7",
  "selected": "1020.00",
  "splited": "1020.00"
}
```

以上例子中，输入总额为1020QTUM，拆分结果为9个100QTUM和1个119.99566QTUM的UTXO。钱包将发送一次对自己转账，并支付0.00434QTUM的转账费。

在前面的例子中还展示了使用`sendmanywithdupes`命令的方式，但这种方式需要注意格式，并且更适用于您想将资金发送到新地址的情况。而且，无论使用哪个命令，这些UTXO都必须等待500个区块时间的确认，成熟后才能用于Staking。

# 以Super Staker身份登录Qtum Core

以上步骤展示了从默认的Qtum Core普通用户转换为Super Staker的流程。Qtum Core钱包也可以直接以Super Staker身份登录以缩短配置流程。这种情况下，起始的区块链同步就已经包括了为地址索引和日志事件构建数据库的过程，所以钱包就可以直接支持Super Staker使用。

Qtum Core钱包可以通过"设置"-"选项"-"允许Super Staking"设置来开启Super Staker模式，或者直接在命令行中使用`-superstaking`参数（示例为测试网环境）。

![7  Linux Launch CN](https://user-images.githubusercontent.com/29760787/85623735-dc602880-b636-11ea-8dc6-c8d6d250f755.png)

该命令在Windows的默认程序目录中使用方式如下：

`qtum-qt -testnet -superstaking`

![8  Windows Command Line Launch CN](https://user-images.githubusercontent.com/29760787/85623743-dec28280-b636-11ea-9b69-5e30797db423.jpg)

当钱包登录并同步区块链时（创建地址索引和日志事件），钱包就可以添加Super Staker。配置一个Super Staker，然后选中"设置"-"选项"-"允许Super Staking"即可开启Super Staker。

# qtumd Super Staker

在Qtum Core钱包中以Super Staker身份运行的任何地址都可能受到委托地址的委托，并以独立的Super Staker进行操作。桌面图形界面版的Qtum-Qt钱包允许配置多个Super Staker地址，分别设置不同的费率和最小UTXO值。deamon/server钱包qtumd中，所有Super Staker地址只能使用同一费率和最小UTXO设置。如果在qtumd中多个Super Staker需要不同的设置，可以在Qtum-Qt钱包中设置好后将wallet.dat文件转移到qtumd中运行。

下面的流程展示了在qtumd中配置一个Super Staker地址的过程。

安装qtumd后，以以下参数登录（示例为测试网环境）：

`./qtumd -testnet -superstaking`

可以添加一些非必须参数以修改费率（10%）和最小UTXO值（100QTUM），例如：

`-stakingminfee=12  -stakingminutxovalue=120`

一旦钱包完成同步，就可以取得一个地址，并向该地址发送一些QTUM。这个地址就将是演示用的Super Staker地址。使用如下命令：

`./qtum-cli -testnet getnewaddress "legacy"`

然后向该地址发送1300QTUM。

![9  Getnewaddress Getbalance CN](https://user-images.githubusercontent.com/29760787/85623752-e124dc80-b636-11ea-9337-3239630551f3.png)

这1300QTUM以一个UTXO的形式发送，想要用于Super Staker操作就必须进行拆分。可以使用`splitutxosforaddress`命令拆分为最小100QTUM、最大200QTUM。

`./qtum-cli -testnet splitutxosforaddress "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d" 100 200`

![10  Split UTXOs for Address qtumd CN](https://user-images.githubusercontent.com/29760787/85623757-e3873680-b636-11ea-907d-36a19e01d11c.png)

命令的执行结果显示1300QTUM被拆分成12个UTXO，可以根据转账的txid在区块链浏览器中查看具体操作。

此时，qtumd钱包已经可以使用地址qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d进行Super Staker操作。可以使用以下命令查看委托情况：

`getdelegationsforstaker "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d"`

# Super Staker操作

Super Staker必须有一定量的UTXO为正在Staking的委托UTXO进行Stake以领取区块奖励。所需UTXO的数量（每个UTXO最少100QTUM）视委托权重占全网权重的百分比而定。比较安全的UTXO数量如下：30UTXO（1%全网权重）、50UTXO（2%全网权重）、100UTXO（5%全网权重）、160UTXO（10%全网权重）。

Super Staker应该时刻关注自己的钱包权重（UTXO权重减去正在Staking的数量），并在下降显著时及时补充UTXO。

请在更改offline staking设置（比如增加Super Staker或增加委托）后及时备份钱包（保存一份wallet.dat）文件，因为offline staking设置保存在wallet.dat文件内。如果wallet.dat文件丢失，也可以通过恢复选项找回设置。

向Super Staker发出的委托可以通过Super Staker页面的"委托"按钮进行查看，或者使用`getdelegationsforstaker`命令。

# 恢复

通常委托和Super Staker设置保存在wallet.dat文件内。如果wallet.dat文件遇到问题，可以通过Super Staker与委托页面的"恢复"按钮恢复委托信息和Super Staker信息。这种情况下，钱包将重新扫描智能合约状态，找到相应地址的offline staking转账相关信息。

![11  Restore super stakers CN](https://user-images.githubusercontent.com/29760787/85623770-e6822700-b636-11ea-8042-0ba6b480ccf0.jpg)

***
