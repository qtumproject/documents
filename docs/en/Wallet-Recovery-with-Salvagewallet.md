# Recovery wallet data with salvagewallet

This is a very helpful method to recovery your wallet data. It can fix following issues.

 - Incorrect balance
 - Broken wallet
 - Wallet launching issue

**PLEASE make sure backup your wallet before below operations. These operations may break your wallet.**

## Windows wallet turtorial

Let's take Windows 10 as example. Other windows are similar.

Firstly please find the shortcut of *Qtum-Qt*. It's on the desktop or the start menu. Copy it to the desktop.

![](https://s.qtum.site/uploads/8c063738e99659bdd7107e4d18d11340.png)
![](https://s.qtum.site/uploads/5722815f8ea76738222daa9bc295cce1.png)

Right click on the short cut, click on **Properties** and click on **Shortcut**. Then add `--salvagewallet` to the end of **Target**.

![](https://s.qtum.site/uploads/04561479b811f843a7c4d277966c291e.png)

Click on **OK**. The dialogue will be closed.

Now double click on the shortcut. The wallet will launch and reindex blocks.

![](https://s.qtum.site/uploads/1206d81a66ec6284065773b47b7292bc.png)

We can have a look at the data menu of Qtum. Open menu `%APPDATA%\Qtum`. **Please be careful and don't remove or change any content under this menu except you are aware of them.**

![](https://s.qtum.site/uploads/c5f68c974ac0076a09da14a5896776be.png)

Now the old wallet has been backed up to `wallet.1516172743.bak`. The wallet is using the new `wallet.dat` file. It contains all private keys with brand new data.

After the above steps, it's better to remove the shortcut on the desktop in order not to reindex your wallet next time.
