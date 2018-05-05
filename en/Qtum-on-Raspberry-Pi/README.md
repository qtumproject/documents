# Qtum on Raspberry Pi

Just like we did on Debian, we need to download and install Qtum's public key

```wget -qO - http://repo.qtum.info/apt/public.key | sudo apt-key add - ```

This downloads and installs the Qtum public key

### Adding repository to your APT sources.

`sudo su` - Sudo to root first

` echo "deb http://repo.qtum.info/apt/raspbian/ jessie main" >> /etc/apt/sources.list`
or
` echo "deb http://repo.qtum.info/apt/raspbian/ stretch main" >> /etc/apt/sources.list`

This will add the repository to your APT sources file.

### Refreshing APT sources and installing Qtum

`sudo apt update && sudo apt install qtum`

By doing this, we'll update our sources and install Qtum on our raspberry Box, which can act now as a staking server/node.



## Changing default password

This option is recommended for security reasons, the default password on the pi is well known, it's highly recommended to change it upon first login.

To change just type: `passwd`

The prompt will ask you to write and repeat the new password to confirm.



## Protecting access with a basic firewall

Well, our raspberry is only for staking, there's no need to have all those ports open, let's close everything we don't need and only allow access to necesary services.

First, let's install UFW (uncomplicated firewall) which is an easy-to-use interface for iptables

`sudo apt install ufw`

Once this is installed, we proceed with access permissions, we will define which ports will be accessible. Let's check first what's open:

`sudo ufw status` This should show something like this: 

`Status: active`

`To               Action      From`

`--               ------      ----`

`22               ALLOW       Anywhere`



#### Ok so it's time to start closing down access, type the following:

`sudo ufw default deny incoming`

`sudo ufw allow 3888/tcp`

`sudo ufw allow 3889/tcp`

Here we've defined the basics, closing down everything except port 3888 and 3889 which are used by Qtum to function.

If you're using SSH, it's recommended to only allow access from local network.

`sudo ufw allow from 196.168.0.0/24 to any port 22`



## Launching Qtum daemon

All we need to do to launch the Qtum daemon is type:
`qtumd -daemon`

As soon as you type this, the wallet will create the wallet.dat file among other files (if they’re not already there). The wallet will run and begin syncing instantly from the other Blockchain nodes, this can take a few hours to complete so you can go ahead and have some coffee and let it synchronize.

## Encrypting wallet

We can encrypt the wallet at any time, it's better to do it before we go any further.

To do this, type the following on the command line:

`qtum-cli encryptwallet yourpassword`

This will encrypt the wallet which in turn closes the daemon, you'll see the following message:

`wallet encrypted; Qtum server stopping, restart to run with encrypted wallet.` If you alreadby backed up before encrypting, you ** need to make a new backup. **

`qtum-cli getaccountaddress` "" -> Right after launching the daemon, you can obtain your wallet address by typing this.

You can send Qtum coins to the address we just obtained from the daemon, please remember that those transactions require at least 500+ confirmations before they become mature enough for staking.

## Staking

Now that we've waited until we have at least 501 confirmations on our received transaction, we are elligible for staking, however, if our wallet is encrypted (which we did for security reasons) we won't be able to stake, let's open our wallet for staking using the command line!.

`qtum-cli walletpassphrase password 999999999 true`

The above command will unlock the walet for 31.6 Years! that should be enough for now. Please note, this will not unlock your backup, only the wallet that's running right now.

Now that we've unlocked our wallet, we need to wait until we have more than 501 confirmations to be elligible for staking, if we already do, it's a matter of time which will vary depending on the network weight vs your wallet's weight.

## Checking Balance

To check your balance, type qtum-cli getinfo this will show general information, including your available balance and balance in staking

## Check transactions

To check your transactions (incoming and outgoing) type qtum-cli listtransactions

## Check staking info

To check Qtum's staking information, type qtum-cli getstakinginfo

## Staking tips

Staking really depends on network weight vs your wallet’s weight which is based on the amount of coins you have, higher weight increases your chances of staking a block.

If you have a large amount of coins, it’s a good idea to split those up in separate transactions, for instance, if you have 10.000 QTUM, it’s better to send 10 transactions of 1000 QTUM each to your wallet, each one generates a UTXO input which will take part in staking. This optimizes the staking process and works much better than just one large 10.000 QTUM input.

If you want to split your coins into different addresses inside your VPS wallet, type the following to obtain new addresses inside your wallet: qtum-cli getnewaddress Each time you type this, you’ll get a new address, QTUM can generate any amount of addresses you want, but please keep in mind, if you do go over 100 new address, you might want to make a new backup of your wallet.


## Updating wallet

We’re always launching new updates, sometimes it’s to add new features or fix bugs. In any case, updating is a breeze, all you have to do is type
` sudo apt update && sudo apt install —only-upgrade qtum `
