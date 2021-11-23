# Qtum Ledger Loader - Address Delegation with Ledger and QRC20 Tokens with Ledger

The Qtum Ledger Loader allows sideloading the Qtum App to a Ledger Nano S. The Qtum core devs developed the Qtum App which enables Ledger Nano S users to make smart contract transactions such as QRC20 transfers and offline staking address delegations with Ledger where users will see the familiar interface on the Ledger device, scroll through screens to verify the hash and transaction details, and manually approve everything on the device.

The Qtum Ledger Loader application contains the Qtum App to be installed on the Ledger Nano S. Communications with the Ledger is managed through Python using pyloader and ledgerblue which is a Python program that handles communication with the Ledger.

Setup for sideloading with these steps, which are given in more detail in the Appendix:

1. Install Python using a custom installation with pyloader and setting the path. Install ledgerblue.
2. Install the Qtum Ledger Loader.
3. Sideload the Qtum App by running the Qtum Ledger Loader connected to your Ledger Nano S.
4. Setup Qtum Electrum with Ledger.

# Address Delegation with Ledger

Qtum offline staking address delegation works with Qtum legacy "Q" addresses only. If your Ledger holds QTUM in a SegWit "M" address, create a Qtum legacy "Q" address on the Ledger, send the QTUM to this address, and then delegate from this address. For more information about Qtum legacy addresses on Ledger see the note "Qtum address formats" at [Ledger Docs – Qtum](https://support.ledger.com/hc/en-us/articles/115003776913-Qtum-QTUM-?docs=true). For larger wallets (> 5k QTUM) delegate address UTXOs should be "split" into 100 QTUM sizes [Reference 3].

Download and install the current version Qtum Electrum wallet from [Qtum Electrum Releases](https://github.com/qtumproject/qtum-electrum/releases). Then complete sections 1 through 4 in the Appendix to sideload the Qtum App into Ledger and setup with the Qtum Electrum wallet.

1. Connect the Ledger to your computer, enter the PIN and launch the Qtum App.

2. Launch Qtum Electrum and select to use hardware device, Ledger in the setup:

![3  Use a hardware device and Ledger Nano S](https://user-images.githubusercontent.com/29760787/142965429-93404386-90ed-4364-b6ab-2ac52c66cf8e.jpg)

On the Electrum View menu select "Show Delegations", then on the Delegation page right-click to add an address delegation. Click the Address drop-down and select the address to be delegated, enter the Staker address (a list of super stakers is available at [Super staker list](https://stake-a-thon.qtum.org/en/super-staker/list)), Fee Percent, use the default fees, and click "Add". 

![4  Address Delegation with Side Panels](https://user-images.githubusercontent.com/29760787/142965447-c53734f8-6e43-46d1-a42e-b65229d6d104.jpg)

Confirm the address delegation on the Ledger, scrolling right and selecting "Sign message"

![5  Sign message](https://user-images.githubusercontent.com/29760787/142965456-9c9da90c-8df6-417a-b5dc-46d2008e50f6.jpg)

Confirm the transaction back on Electrum by clicking "Send":

![6  Confirm transaction with side panels](https://user-images.githubusercontent.com/29760787/142965466-61e0f1de-9113-4750-91ce-16d8e9e40866.jpg)

On the Ledger, scroll right to review the transaction and select "Approve", then scroll right and select "Accept", finally selecting "Accept and send":

![7  Approve Accept Accept and send](https://user-images.githubusercontent.com/29760787/142965478-a5294ab6-0f17-4108-8bd8-7e74a3c9f8b3.jpg)

Electrum will broadcast the transaction which will be confirmed in the next block with the delegation showing on Electrum's Delegations page and the qtum.info explorer. Follow the same pattern to undelegate by right-clicking on the delegation shown on the Delegations page.

For more information on Qtum address delegation see [Delegating Address FAQs](https://blog.qtum.org/delegating-address-faqs-5958e8b79e72).

# Sending QRC20 Tokens from a Ledger Address

Complete sections 1 through 4 in the Appendix to sideload the Qtum App into Ledger and setup with Qtum Electrum.

Once Qtum Electrum is set up with Ledger, and the Qtum App is installed on the Ledger, you can use the Electrum wallet to send QRC20 tokens from the Ledger address.

1. Connect the Ledger to your computer, enter the PIN, and launch the Qtum App.

2. To view QRC20 tokens for the Ledger address, find the token contract address at [Qtum.info QRC20](https://qtum.info/qrc20), select the token, copy the token Contract Address and enter it on the wallet Tokens page by right-clicking in the "Name|Bind Address" field and paste the contract address: (MED shown here)

![8  Adding token MED](https://user-images.githubusercontent.com/29760787/142965493-13035edc-e91e-40b7-b98b-50244112065d.jpg)

To send the QRC20 tokens, on the Electrum Tokens page, right-click the desired token, click send, enter the receiving address ("Pay to"), amount, fees, and click "Send". On the Ledger, scroll through to approve the transaction details and select "Accept and send" to send the transaction. Electrum will confirm the transaction.

![9  Accept and send](https://user-images.githubusercontent.com/29760787/142965506-d03a270e-3937-4bc1-a00e-6b859ed18c59.jpg)

# Security Note

Hardware wallets provide some of the best security for cryptocurrency wallets because they hold the private keys offline for signing transactions, and allow manual inspection and approval of transactions on the hardware device. This Qtum Ledger Loader solution maintains the full security of the hardware wallet and does not export private keys. The Qtum App for Ledger Nano S has been developed by the Qtum core developers and submitted to Ledger for review and incorporation for sideloading through their official Ledger Live wallet, but priorities and resources at Ledger have delayed availability, so Qtum is providing this direct approach.

# Appendix – Installation Steps

## 1. Install Python

1. Download the Python installer for your computer from [Python Downloads](https://www.python.org/downloads/) and run the installer.

2. At the bottom of the install screen check Add Python 3.10 to PATH and then click on "Customize installation":

![10  Add Python to PATH and Customize installation](https://user-images.githubusercontent.com/29760787/142965519-53750db5-7c32-4f53-b8a3-d67882f6f86a.jpg)

On the Optional Features page leave all features checked and click "Next".

![11  Optional Features](https://user-images.githubusercontent.com/29760787/142965524-51e7c874-0741-492b-96b9-cf95a62b16f0.jpg)

3. On the Advanced Options page check "Install for all users" and click "Install" to complete the Python installation.

![12  Advanced Optoins - Insttall for all users](https://user-images.githubusercontent.com/29760787/142965536-87b5e4ba-d65e-4167-962a-672c621fcee9.jpg)

4. Install the ledgerblue package to interface with Ledger. On Windows open the Command Prompt, on other systems open the Terminal, and enter:

`python -m pip install --user ledgerblue`

![13  Install ledgerblue](https://user-images.githubusercontent.com/29760787/142965541-2e89759b-ceeb-407e-94c9-ab41ff619ab9.jpg)

## 2. Install the Qtum Ledger Loader

1. Download the Qtum Ledger Loader version for your computer from https://github.com/qtumproject/qtum-ledger-loader/releases :

* Windows users select the file ending in **win64-setup-unsigned.exe**

* Mac users select the file ending in **osx-unsigned.dmg**

* Linux (x86) users select the file ending in **x86_64-linux-gnu.tar.gz**

* Raspberry Pi users select the file ending in **arm-linux-gnueabihf.tar.gz**

Override any file warnings to save the downloaded file and you may use a checksum utility to validate the SHA-256 checksums given on the releases page.

2. Run the downloaded installer file to complete the installation. Exit the installer and close the Qtum Ledger Loader if it opened.

![14  Run anyway - Completed](https://user-images.githubusercontent.com/29760787/142965549-388fa0e8-679e-4f11-b285-c884978c0744.jpg)

## 3. Sideload the Qtum App

The Qtum Ledger Loader works with Ledger Nano S and will not work with Nano X which does not allow sideloading.

During the sideload process the Ledger will give some prompts "Allow unsafe manager" about using the Qtum Ledger Loader, which must be accepted to allow the Qtum App to load.

1. Connect the Ledger Nano S to your computer and enter the PIN code but do not select any Apps. The old Qtum App is shown below.

![15  Starting Screen](https://user-images.githubusercontent.com/29760787/142965560-b8c4b429-3a23-4925-9224-c9e2a4370efb.jpg)

2. Run the Qtum Ledger Loader. Leave the options set for "Qtum Wallet" and "Mainnet" (unless you want Testnet) and click on "Install".

![16  Qtum Ledger Loader](https://user-images.githubusercontent.com/29760787/142965565-c134b8ba-8ea7-457d-a407-92ca79d77aa1.jpg)

On the Ledger scroll right past the initial "Deny" screen, keep scrolling right and verify the public key (9 screens), then select (using the double button press) "Allow unsafe manager".

![17  Public Key and Allow unsafe manager](https://user-images.githubusercontent.com/29760787/142965571-b348b125-d3fd-4c63-8e3f-491657b4e15e.jpg)
The Installer will say "Confirm Qtum install on your Ledger device…"

On the Ledger scroll right to see the public key again (9 screens) and select "Allow unsafe manager", and the App will load.

![18  Public Key Allow unsafe Loading](https://user-images.githubusercontent.com/29760787/142965577-2766182b-1c30-4bc4-9b60-6603882b57df.jpg)

On the Ledger you will see "Install app Qtum", scroll right to see the version, identifier, and Code identifier. Select "Perform installation" and enter the PIN number to complete the installation.

![19  Install Identifier Perform Installation](https://user-images.githubusercontent.com/29760787/142965581-e8aae921-2f61-47f2-ab0d-710da4c1d76e.jpg)

At this point, you can scroll the apps to see the Qtum App installed (version 1.6.5).

![20  Qtum App Installed](https://user-images.githubusercontent.com/29760787/142965591-c7ac342e-07fc-4f08-be29-e98d3e6a42da.jpg)

## 4. Setup Qtum Electrum with Ledger

Download and install the latest version of Qtum Electrum from https://github.com/qtumproject/qtum-electrum/releases.

Connect the Ledger device, enter the PIN, and run the Qtum App. Assumes the Qtum App is installed. On the Ledger, scroll past the warning and identifier, and select "Open application" to launch the Qtum App and see "Application is ready".

![21  Public Key Allow Open application](https://user-images.githubusercontent.com/29760787/142965599-4823abbc-3f41-44af-b0fc-7530750de964.jpg)

Run Qtum Electrum, choose "Standard wallet" and "Use a hardware device". Continue selecting "Ledger Nano S", "legacy" address, and leave the default derivation path.

![22  Use Hardware Ledger Nano S legacy](https://user-images.githubusercontent.com/29760787/142965610-06f1c705-354d-4125-b5b8-d89c2e583c14.jpg

Select to "Encrypt wallet file" which means the Ledger will be required to reopen the wallet. The wallet will open and begin synchronizing and after full synchronization will show the current balances for the Ledger address.

# References

1. Ledgerblue is a Python library to communicate with Ledger Blue and Nano S available at [Ledgerblue](https://pypi.org/project/ledgerblue/) The ledgerblue package contains Python tools to communicate with Ledger Blue, Nano S, and Nano X and manage applications life cycle.

2. Windows 7 can not install current versions of Python. Instead, use Python 3.8.8 (for Windows 7) from https://www.pytyon.org

3. Better returns for larger wallets (> 5k QTUM) are achieved by "splitting" UTXOs into 100 QTUM sizes. For Qtum Electrum, use the "Tools" "Pay to many" page to send to a new address in the Electrum (a Ledger address if desired) and then delegate that address. Note that coins must mature for 2,000 confirmations before they will be used for staking.

