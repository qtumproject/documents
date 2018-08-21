**IMPORTANT!**
**When using a web wallet like this one, please make 100% sure that you're entering the right URL which is**

https://qtumwallet.org

There is no other URL being used for the web wallet, please be safe and verify the green padlock with "Secure" in the URL field which validates the site:

![0. Secure Site](https://github.com/JB395/QtumMon/blob/master/Images/0.%20Secure%20EN.jpg)

Welcome to the Qtum web wallet user documentation which will show 

* [Introduction to the Web Wallet](https://github.com/JB395/QtumMon/wiki#introduction-to-the-web-wallet)
* [How to generate a new wallet or restore addresses from other wallets](https://github.com/JB395/QtumMon/wiki#generate-new-wallet---restore-wallet)
* [How to receive and send QTUM coins](https://github.com/JB395/QtumMon/wiki#receive-and-send-qtum-coins)
* [How to receive and send QRC20 tokens](https://github.com/JB395/QtumMon/wiki#send-and-receive-qrc20-tokens)
* [How to add a new QRC20 token to the wallet](https://github.com/JB395/QtumMon/wiki#adding-a-qrc20-token)
* [How to publish smart contracts](https://github.com/JB395/QtumMon/wiki#how-to-publish-smart-contracts) (future)

***

# Introduction to the Web Wallet

The Qtum web wallet runs in your browser and connects to the Qtum network through a full node interface. The web wallet does not store your private keys so you must manage those with a downloaded Key File or seed words. This is completely your responsibility.

The web wallet may be launched by navigating to the site listed above and clicking on the **`  Web  `** button:

![A. Select Web Wallet EN](https://i.imgur.com/jE89N81.jpg)

Scroll down and click the large blue **`  Visit Website  `** button: 

![B. Select Visit Website EN](https://i.imgur.com/yNLtnZR.jpg) 

Upon loading the web wallet, we get this very important warning, please take a few seconds and read it.

![Warning](https://i.imgur.com/ZGBb9u6.jpg)

Welcome to the Qtum web wallet! As shown below the left panel gives a menu with various options to create or restore a wallet, and other actions. The top of the menu gives seven choices for creating or restoring a wallet. The bottom of the menu gives various operations and configuration choices. The center part of the wallet page presents forms for data entry, viewing and management of the wallet assets.

The menu option **` Settings `** will allow selection of language and setting the wallet to work on Mainnet or Testnet. Select the desired network **before** restoring a wallet or entering a password.

***

# Generate New Wallet - Restore Wallet

There are 7 ways to generate or restore a wallet.

1. [Generate new Wallet](https://github.com/JB395/QtumMon/wiki#1-generate-new-wallet) – creates a new address and downloads a Key File
2. [Create from Mnemonic](https://github.com/JB395/QtumMon/wiki#2-create-from-mnemonic) – creates 12 seed words and a new address
3. [Restore from Mnemonic](https://github.com/JB395/QtumMon/wiki#3-restore-from-mnemonic) – restores an address using 12 seed words from a desktop wallet
4. [Restore from WIF](https://github.com/JB395/QtumMon/wiki#4-restore-from-wif) – restores an address from a private key
5. [Restore from Mobile Wallet](https://github.com/JB395/QtumMon/wiki#5-restore-from-mobile-wallet) – restores an address from 12 seed words from a compatible mobile wallet
6. [Restore from Key File](https://github.com/JB395/QtumMon/wiki#6-restore-from-key-file) – restores an address from a Key File created by the web wallet
7. [Restore from Ledger](https://github.com/JB395/QtumMon/wiki#7-restore-from-ledger) – uses a Ledger hardware wallet to sign and verify transactions

![2. Generate New Wallet](https://i.imgur.com/5LdWl0r.jpg)

### 1. Generate New Wallet

Now let's choose the first option on the menu screen above and click on the red **` GENERATE NEW WALLET `** button. Next, you will enter a password which will be used to create a series of private keys. Write down a new long and strong password, enter the password and click the blue **` CONFIRM `** button: 

![3. Enter Password](https://i.imgur.com/6cFzE2p.jpg)

Next click the large green button to download the Key File:

![4. Download Key File](https://i.imgur.com/MPlJCXK.jpg)

The Key File will download to your computer, save the file in a location you can find again and back up the file offline. The key file name will have a format like "1529379436736.txt" where the long number is the file creation time as Unix epoch time in milliseconds. You will need this Key File and the password to reload the wallet. If you lose the Key File or password, the funds in your wallet will be lost.

The _View Wallet Info_ page will appear for your wallet where you can see:

1. Address - receiving address for the wallet
2. Balance - confirmed coins
3. Unconfirmed Balance - coins waiting to be confirmed in the next block
4. Private Key - the private key for this address

![5. View Wallet Info](https://i.imgur.com/nW88f0h.jpg)

### 2. Create from Mnemonic

Click on the menu option **` Create from Mnemonic `**, **` GENERATE NEW WALLET `**, enter a password and click **` CONFIRM `**. The wallet will create a new address from 12 random seed words:

![6. Generate Seed Words](https://i.imgur.com/ioGSwbq.jpg)

Please write down and save these seed words, only you as the wallet user have access to these seed words (seed words and private keys aren't stored on the server, if you lose these seed words you'll lose access to your funds!).

Next you have to enter the seed words manually to confirm you have saved them. Click on the blue button **` I HAVE REMEMBERED ALL. LET'S CHECK `**, enter your password, re-enter the seed words and click the green **` CONFIRM `** button:

![7. Confirm Seed Words](https://i.imgur.com/1ClZwHq.jpg)

Then you will see the _View Wallet Info_ page as shown above. You may want to download a Key File for the wallet using the menu option **` Dump as Key File `** which will give another way to restore the wallet as described in step 6 below.

### 3. Restore from Mnemonic

For the menu option **` Restore from Mnemonic `** you will enter the seed words saved in step 2 above. Make sure you enter the seed words correctly (with no typos or additional blank spaces), click the green **` CONFIRM `** button:

![8. Enter Seed Words](https://i.imgur.com/DAU5res.jpg)

After entering a new password, you will see the _View Wallet Info_ page. Verify that the expected address was created. You may want to back up the wallet using the menu option **` Dump As Key File `**.

### 4. Restore from WIF

This choice allows restoring the wallet from a Wallet Input Format (WIF) private key such as from the web wallet, Qtum Core wallet or Qtum Electrum wallet. A WIF private key will be 52 characters long and has error checking and encoding (to reduce size) as compared with an original private key, which will be 64 hexadecimal characters.

Copy the WIF private key from another wallet. Select the menu option **` Restore from WIF `**, paste the private key into the _WIF_ field and click the green **` CONFIRM `** button:

![9. Restore from WIF](https://i.imgur.com/UxnrajH.jpg)

The _View Wallet Info_ page will be displayed. Verify you restored the expected address. You may want to back up the wallet using the menu option **` Dump As Key File `**.

### 5. Restore from Mobile Wallet 

Restore from Mobile Wallet allows restoring a wallet address from a compatible mobile wallet such as the Qtum mobile wallet, Qbao wallet, or the Qtum Electrum wallet (if the Qtum Electrum wallet was initialized to be compatible with the Qtum mobile wallets).

Select the menu option **` Restore from Mobile Wallet `** and enter the 12 seed words from your other wallet. Enter the words carefully in lower case (never in UPPERCASE) and make sure there are no blank spaces after the words, and click the green **` CONFIRM `** button:

![10. Restore from Mobile Wallet EN](https://i.imgur.com/4BS3jFi.jpg)

Next, choose the address to restore, it will probably be the top address row unless you were using multiple addresses on your mobile. If you don't see the correct address, reenter the seed words carefully. Click the green **` CHOOSE `** button for the desired address:

![11. Choose Address EN](https://i.imgur.com/tUo4mGY.jpg)

The _View Wallet Info_ page will be displayed. You may want to back up the wallet using the menu option **` Dump As Key File `**.

### 6. Restore from Key File

Select the menu option **` Restore from Key File `**, **` UPLOAD `**, select the key file to upload and click **` Open `**. Enter your password and click the blue **` CONFIRM `** button. The _View Wallet Info_ page will be displayed.

![12. Restore from Key File EN](https://i.imgur.com/xcaPvzh.jpg)

### 7. Restore from Ledger

To use your Ledger Nano S or Ledger Blue with Qtum, you will first need to run the Ledger Manager and install the Qtum app on your Ledger using these instructions:
https://support.ledgerwallet.com/hc/en-us/articles/115003776913-Install-and-use-Qtum-QTUM-

![13. Qtum App EN](https://i.imgur.com/th4IymV.jpg)

On the web wallet select the menu option **` Restore from Ledger `**, plugin your Ledger, and on the Ledger enter the PIN code and open the Qtum app, then on the web wallet _Restore from Ledger_ page click the red **` CONNECT `** button:

![14. Restore from Ledger EN](https://i.imgur.com/1wSYpgR.jpg)

On the next _Restore from Ledger_ page, click on the green padlock icon to select the default path:

![15. Choose Path Default EN](https://i.imgur.com/3IErrFG.jpg)

On the _Default path m/44’/88’/0’/0_ page choose the address you want to use by clicking on the green padlock icon on that row. This will probably be the top row unless you made other address choices in the Ledger Live wallet.

![16. Choose Address EN](https://i.imgur.com/2M4XSCb.jpg)

The _View Wallet Info_ page will be displayed. Notice that using the Ledger there is not the option to see or copy the private key because the Ledger hardware wallet manages the private keys and does not send them to your computer. The **` Restore from Ledger `** option is not available for Testnet.

![17. View Wallet Info EN](https://i.imgur.com/LiJRR7C.jpg)

You can send QRC20 tokens to an address managed by the Ledger wallet, such as Ledger Live, but the Ledger wallet does not currently (August 2018) allow display or management of QRC20 tokens. You can use **` Restore from Ledger `** with the web wallet to display and manage QRC20 tokens held in your Ledger address, in which case the _View Wallet Info_ page will show these tokens:

![18. View Wallet Info QRC20 EN](https://i.imgur.com/PFktEEy.jpg)

***

# Receive and Send QTUM Coins

### Receive

You can receive coins for the web wallet by sending them to the address of the wallet. Before you send any coins to the wallet make sure you can close and reopen the wallet with the same receive address. Using the menu option **` Dump as Key File `** and **` Restore from Key File `** is a safe way to do this. Using the menu option to restore from seed words to reopen the wallet is riskier because entering a typo for the seed words or password will create an unexpected random address. 

On the _View Wallet Info_ page click on the blue address **` COPY `** button and then paste this address as the receiving address in the sending wallet or account, and then send the coins. Wait a few minutes for the next block to be published and reload the web wallet to see the new balance. You can also click on the menu option **` View Wallet Txs `** to see the receiving transaction: 

![19. View Wallet Txs EN](https://i.imgur.com/xjIFSvx.jpg)

### Send

From your receiving wallet or account, copy the receiving address. On the web wallet menu, click **` Send `** and paste the receiving address into the _Address*_ field, then enter the amount to send in the _Amount*_ field. You can leave the _Fee_ field set at the default of 0.01 (or set a lower fee if you understand how to do this) and click the green **` CONFIRM `** button:

![20. Send tokens EN](https://i.imgur.com/GpzinKD.jpg)

The _Please enter address again (Double check)_ page will be displayed. Copy and paste the receiving address into the _Address_ field and click the blue **` CONFIRM `** button:

![21. Please enter address again... EN](https://i.imgur.com/db4zBHD.jpg)

The _You are going to send…_ page will be displayed, after verifying the information click the blue **` CONFIRM `** button:

![22. You are going to send... EN](https://i.imgur.com/v3zoaka.jpg)

At the bottom of the screen you will see the green confirmation bar with a link to show the transaction in the Explorer: 

![23. Successful send EN](https://i.imgur.com/fqqIIce.jpg)

The _View Wallet Info_ page will display an _Unconfirmed balance_ for the amount being sent (+ fee). 
After the transaction is published in the next block you can reload the wallet to see the updated balance and also see the transaction using the menu option **` View Wallet Txs `**.

***

# Send and Receive QRC20 Tokens

If you haven't done this, make sure you can back up the wallet using menu option **` Dump as Key File `**, and then reopen to the same address using **` Restore from Key File `**.

### Receive QRC20 Tokens

To receive QRC20 tokens, on the web wallet _View Wallet Info_ page and copy the _Address_ field by clicking the blue **` COPY `** button, paste this address into the sending wallet or exchange, and send the tokens. After the next block publishes, reload the wallet to see the tokens:

![24. Receive QRC20 Tokens EN](https://i.imgur.com/pozYh4S.jpg)

### Send QRC20 Tokens

To send QRC20 tokens you must have sufficient QTUM coins in the address tied to that token. The web wallet default fee for sending tokens is 0.00000040 gas price x 250,000 gas = 0.1 QTUM plus the default transaction fee of 0.01 QTUM, for a total fee of 0.11 QTUM. You can use these default values unless you understand how to set lower values, but don't worry, any excess gas will be refunded as a mined amount (the mined amount must mature for 500 blocks before it can be sent or used for gas/fees).

![25. Send QRC20 Token EN](https://i.imgur.com/ttRyUqK.jpg)

***

# Adding a QRC20 Token

The web wallet will has built-in capability for popular QRC20 tokens, and you can add additional tokens by entering the token’s smart contract information. For example, if you want to add the XYZ token, find that token on the explorer qtum.info, copy the contract _Address Hash_ field: 

![26. Copy Address Hash EN](https://i.imgur.com/fW00puB.jpg)

On the web wallet select the menu option **` Send `**, click the drop down next to "QTUM", scroll to the bottom of the Coin/Token list and click the **` More... `** button:
 
![27. Add QRC20 Token EN](https://i.imgur.com/PSCBSjP.jpg)

Paste the Address Hash copied from the Explorer into the _Token Contract Address_ field and click the blue **` SEARCH `** button:

![28. Enter Address Hash EN](https://i.imgur.com/i8vYHE4.jpg)

The contract details should be displayed on the _Token_ page, verify and click the **` CONFIRM `** button to add this token to your wallet. The new token will be available in the wallet for 30 days, after which you can add it again if needed. 

***

# How to Publish Smart Contracts

(FUTURE)

