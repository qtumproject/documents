**IMPORTANT!**
**When using a web wallet like this one, please make 100% sure that you're entering the right URL which is**

https://qtumwallet.org

There is no other URL being used for the web wallet, please be safe and verify the green padlock with "Secure" in the URL field which validates the site:



![0. Secure site EN](https://i.imgur.com/yaCSQSu.jpg)





Welcome to the Qtum web wallet user documentation which will show 

* [Introduction to the Web Wallet](#introduction-to-the-web-wallet)
* [How to generate a new wallet or restore addresses from other wallets](#generate-new-wallet---restore-wallet)
* [How to receive and send QTUM coins, sending with Ledger, Safe Send](#receive-and-send-qtum-coins)
* [How to receive and send QRC20 tokens](#send-and-receive-qrc20-tokens)
* [How to add a new QRC20 token to the wallet](#adding-a-qrc20-token)
* [How to publish smart contracts](#how-to-publish-smart-contracts)
* [Address Delegation for Offline Staking](#address-delegation-for-offline-staking)
* [Creating and Sending NFTs](#creating-and-sending-nfts)

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

The Qtum web wallet works with Qtum standard addresses which begin with a "Q" (legacy), and is not compatible with SegWit (Segregated Witness) addresses that begin with an "M" (p2sh-segwit) or "qc1" (bech32).

***

# Generate New Wallet - Restore Wallet

There are 7 ways to generate or restore a wallet.

1. [Generate new Wallet](#1-generate-new-wallet)  creates a new address and downloads a Key File
2. [Create from Mnemonic](#2-create-from-mnemonic)  creates 12 seed words and a new address
3. [Restore from Mnemonic](#3-restore-from-mnemonic)  restores an address using 12 seed words from a desktop wallet
4. [Restore from WIF](#4-restore-from-wif)  restores an address from a private key
5. [Restore from Mobile Wallet](#5-restore-from-mobile-wallet) restores an address from 12 seed words from a compatible mobile wallet
6. [Restore from Key File](#6-restore-from-key-file) restores an address from a Key File created by the web wallet
7. [Restore from Ledger](#7-restore-from-ledger) uses a Ledger hardware wallet to sign and verify transactions

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

On the web wallet select the menu option **` Restore from Ledger `**, plugin your Ledger, and on the Ledger enter the PIN code and open the Qtum app, then on the web wallet _Restore from Ledger_ page click the red **` CONNECT `** button:

![14. Restore from Ledger EN](https://i.imgur.com/1wSYpgR.jpg)

When the Windows Security page “Making sure it’s you” appears, double press the Ledger buttons to confirm.

On the next _Restore from Ledger_ page, click on the green padlock icon to select the default path:

![15. Choose Path Default EN](https://i.imgur.com/3IErrFG.jpg)

When the Windows Security page “Making sure it’s you” appears again, double press the Ledger buttons to confirm.

On the _Default path m/44'/88'/0'/0_ page choose the address you want to use by clicking on the green padlock icon on that row. This will probably be the top row unless you made other address choices in the Ledger Live wallet.

![16. Choose Address EN](https://i.imgur.com/2M4XSCb.jpg)

The _View Wallet Info_ page will be displayed. Notice that using the Ledger there is not the option to see or copy the private key because the Ledger hardware wallet manages the private keys and does not send them to your computer. The **` Restore from Ledger `** option is not available for Testnet.

![17. View Wallet Info EN](https://i.imgur.com/LiJRR7C.jpg)

You can send QRC20 tokens to an address managed by the Ledger wallet, such as Ledger Live, but the Ledger wallet does not currently (November 2018) allow display or management of QRC20 tokens. You can use **` Restore from Ledger `** with the web wallet to display and manage QRC20 tokens held in your Ledger address, in which case the _View Wallet Info_ page will show these tokens:

![18. View Wallet Info QRC20 EN](https://i.imgur.com/PFktEEy.jpg)

***

# Receive and Send QTUM Coins

### Receive

You can receive coins for the web wallet by sending them to the address of the wallet. Before you send any coins to the wallet make sure you can close and reopen the wallet with the same receive address. Using the menu option **` Dump as Key File `** and **` Restore from Key File `** is a safe way to do this. Using the menu option to restore from seed words to reopen the wallet is riskier because entering a typo for the seed words or password will create an unexpected random address. 

On the _View Wallet Info_ page click on the blue address **` COPY `** button and then paste this address as the receiving address in the sending wallet or account, and then send the coins. Wait a few minutes for the next block to be published and reload the web wallet to see the new balance. You can also click on the menu option **` View Wallet Txs `** to see the receiving transaction: 

![19. View Wallet Txs EN](https://i.imgur.com/xjIFSvx.jpg)

### Send

From your receiving wallet or account, copy the receiving address. On the web wallet menu, click **` Send `** and paste the receiving address into the _Address*_ field, then enter the amount to send in the _Amount*_ field (if you are sending an amount less than 1.0, use a leading zero, like "0.5", not ".5"). You can leave the _Fee_ field set at the default of 0.01 (or set a lower fee if you understand how to do this) and click the green **` CONFIRM `** button:

![20. Send tokens EN](https://i.imgur.com/GpzinKD.jpg)

The _Please enter address again (Double check)_ page will be displayed. Copy and paste the receiving address into the _Address_ field and click the blue **` CONFIRM `** button:

![21. Please enter address again... EN](https://i.imgur.com/db4zBHD.jpg)

The _You are going to send_ page will be displayed, after verifying the information click the blue **` CONFIRM `** button:

![22. You are going to send... EN](https://i.imgur.com/v3zoaka.jpg)

At the bottom of the screen you will see the green confirmation bar with a link to show the transaction in the Explorer: 

![23. Successful send EN](https://i.imgur.com/fqqIIce.jpg)

The _View Wallet Info_ page will display an _Unconfirmed balance_ for the amount being sent (+ fee). 
After the transaction is published in the next block you can reload the wallet to see the updated balance and also see the transaction using the menu option **` View Wallet Txs `**.

### Sending with Ledger

Sending when the wallet has been restored from Ledger has a few more steps.

From your receiving wallet or account, copy the receiving address. On the web wallet menu, click **` Send `** and paste the receiving address into the _Address*_ field, then enter the amount to send in the _Amount*_ field. You can leave the _Fee*_ field set at the default of 0.01 (or set a lower fee if you understand how to do this) and click the green **` CONFIRM `** button:

![L1 Send Tokens](https://i.imgur.com/T7mIXiL.jpg)

The _Please enter address again (Double check)_ page will be displayed. Copy and paste the receiving address into the _Address_ field and click the blue **` CONFIRM `** button: 

![L2 Address again](https://i.imgur.com/qCeSZHH.jpg)

You will see the _You are going to send… Please confirm tx on your ledger…_ page:

![L3 You are going to send](https://i.imgur.com/CbqxuWc.jpg)

Provided you have connected the Ledger hardware wallet, entered the PIN code an selected the Qtum App, on the Ledger display you will see scrolling details of the transaction so you can confirm the address and amount:

![L4 Address and amount](https://i.imgur.com/K8aYMas.jpg)

On the Ledger, press the right button above the check mark on the display to confirm output #1, which is the main transaction, in this case sending 2.0 QTUM. You will also need to press this button again to confirm output #2, which is sending the change back to your wallet, and press the button a third time to confirm the overall transaction:

![L5 Confirm output 1](https://i.imgur.com/3KDySJ0.jpg)

Now on the web wallet, you will see the raw transaction on the _You are going to send_ page. After verifying the information click the blue **` CONFIRM `** button:

![L6 You are going to send raw transaction](https://i.imgur.com/ugFkTS4.jpg)

At the bottom of the screen you will see the green confirmation bar with a link to show the transaction in the Explorer:

![L7 Successful send](https://i.imgur.com/fMas7Ld.jpg)

The _View Wallet Info page_ will display an _Unconfirmed balance_ for the amount being sent (+ fee). After the transaction is published in the next block you can reload the wallet to see the updated balance and also see the transaction using the menu option **` View Wallet Txs `**.

### Safe Send

A basic Qtum transaction is composed of three steps:

1. Compose the base transaction: from, to, amount, fee.
2. Sign the transaction using the private key.
3. Transmit the signed transaction to the network.

"Safe Send" isolates these steps between two computers/wallets, where step 2 is performed with an offline wallet whose private keys are never exposed to the internet. The web wallet "Safe Send" walks through these 3 steps to make a very safe transaction using the offline wallet.

#### Setup Offline Wallet

For a Safe Send, first set up the offline wallet by getting a copy of the web wallet and browser software. This example will use Google Chrome on Windows, and you can adjust to your preferred browser and operating system.

On the online computer, using the Chrome browser, go to https://qtumwallet.org. In the browser upper right-hand corner select the three vertical dots for menu, select **` More tools `** then **` Save page as… `** to save the Qtum Web Wallet HTML file. This file contains all the JavaScript code to run the web wallet:

![1 The Web Wallet HTML File](https://i.imgur.com/ZdCBdhu.jpg) 
The Web Wallet HTML file

To make an offline copy of Chrome, navigate to find the Chrome install folder on your computer. For Windows it is typically in Program Files (x86) - Google:

![2019-42 Chrome Folder](https://i.imgur.com/us44CuH.png)
Copy Chrome folder

Copy the Chrome folder and Web Wallet HTML file to a USB thumb drive and then copy these to the offline computer.

This gives a copy of the current Chrome and web wallet for the offline computer, and will not get any future version updates. You can do an update with these same steps, but it should not be necessary for these basic operations.

#### Launch the wallet in Offline Mode

On the offline computer, launch the Chrome browser: in the copied Chrome folder select User Data - Application - Chrome.exe:

![2019-43 Select Chrome.exe](https://i.imgur.com/vZ4oSZ1.jpg) 
(here in a folder called "Offline wallet")

#### Launch the offline web wallet

With the cursor in the Chrome URL address bar press Control - "O" (for Open) and then navigate to and Open the Qtum Web Wallet.html file:

![2019-44 Open Qtum Web Wallet.html](https://i.imgur.com/EyE4B1x.jpg)

Using the web wallet menu select Settings and in the Mode dropdown select **` Offline `** and **` CONFIRM `**:

![2019-45 Set Offine Mode](https://i.imgur.com/JLAvVTO.jpg)

Note the gold header for the wallet in offline mode. From this point, you can generate a new wallet and save (and backup) the key file. The menu will show _Request Payment_ and the _Request Payment_ page will show the receiving address for the offline wallet:

![2019-46 Request Payment page](https://i.imgur.com/ova1s8W.jpg)

Copy the receiving address to a text file and copy to the USB thumb drive for transfer to the online computer. Now you can send QTUM to this address to fund the offline wallet.

This works to send QTUM to the offline wallet address because QTUM coins are actually stored as unspent transactions on the blockchain (no coins are ever stored in any wallet itself). However the offline wallet holds the private key for its address, and only the offline wallet can sign transactions to send QTUM from its address.

Now we can use the 3 transaction steps for a Safe Send.

1. Compose the base raw transaction with the online wallet.

From the online wallet menu select **` Safe Send `** and for step 1 fill in the addresses and amount. _From Address*_ is the address of the offline wallet. The online wallet will query the blockchain for the "From Address" and select a previous transaction or transactions that hold sufficient QTUM for the amount being sent. Use 0.01 for the Fee unless you know how to choose lower fees.

After filling in all the fields, press **` CONFIRM `**, reenter the _To Address*_, press **` CONFIRM `** and **` CONFIRM `** again to create the raw transaction file:

![2019-47 Step 1 Safe Send page](https://i.imgur.com/5Z24gc5.jpg)
Step 1 - creating the raw transaction

The online wallet will create a raw transaction text file, for example:

``{"from":"<Qtum address>","to":"<Qtum address>","amount":"5.0","fee":"0.01",
"utxo":[{"address":"<from Qtum address>","txid":"<transaction ID>","confirmations":4,
"isStake":false,"amount":10,"value":1000000000,"hash":"<hash checksum>","pos":0}]}``

Here the online wallet has selected an appropriate unspent transaction owned by the "From Address" which holds 10.0 QTUM.

You must leave the online wallet running at the end of step 1 while completing step 2 with the offline computer, then return for step 3. Exiting the online wallet at this point and reloading for step 3 will cancel the sequence.

Copy the raw transaction file to the offline wallet computer. For the offline wallet launch Chrome and the wallet in offline mode as in "Launch the Offline Wallet" above. Use the menu option **` Restore from Key File `** to load the previous address. The offline wallet will not know or display any balance.

2. On the offline wallet menu select **` Safe Send `** and on the _Safe Send_ page in step 1 press **` NEXT `** to begin step 2.

In step 2 select **` UPLOAD `** and open the raw transaction file copied from the online wallet. You will see the transaction fields as entered on the online computer. Select **` CONFIRM `**, reenter the _To Address*_ and **` CONFIRM `**, and then **` CONFIRM `** again to create the signed tx file:

![2019-48 Step 2](https://i.imgur.com/90qZsLa.jpg) 
Step 2 - sign the raw transaction file to create the tx (transmission) file

The offline wallet will generate a signed tx file, for example:

``{"from":"<Qtum Address>","to":"<Qtum Address>","amount":"5.0",
"fee":"0.01","rawTx":"<raw hex transaction code>"}``

Copy this file to a USB thumb drive and transfer to the online wallet computer.

Note that the offline wallet is completely disconnected from the internet, and can only sign the transaction using its private keys. The offline wallet cannot even show the balance for its address, but you can see the balance with the Explorer.

3. Back on the online wallet (still on the _Safe Send_ page) on step 2 select **` NEXT `** to advance to step 3.

On step 3 select **` UPLOAD `** and open the signed tx file. You will see the transaction fields as entered in step 1. Press **` CONFIRM `**, reenter the _Send To*_ address and select **` CONFIRM `**, and **` CONFIRM `** again to send the transaction to the network:

![2019-49 Step 3](https://i.imgur.com/w9eCAo8.jpg)
Step 3 - send the tx file to the network to complete the transaction

At the bottom of the screen you will see the green confirmation bar, and after the transaction is published in the next block select the Explorer link to see the transaction on the blockchain.

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

The web wallet will has built-in capability for popular QRC20 tokens, and you can add additional tokens by entering the token's smart contract information. For example, if you want to add the XYZ token, find that token on the Explorer qtum.info, copy the contract _Address Hash_ field: 

![26. Copy Address Hash EN](https://i.imgur.com/fW00puB.jpg)

On the web wallet select the menu option **` Send `**, click the drop down next to "QTUM", scroll to the bottom of the Coin/Token list and click the **` More... `** button:

![27. Add QRC20 Token EN](https://i.imgur.com/PSCBSjP.jpg)

Paste the Address Hash copied from the Explorer into the _Token Contract Address_ field and click the blue **` SEARCH `** button:

![28. Enter Address Hash EN](https://i.imgur.com/i8vYHE4.jpg)

The contract details should be displayed on the _Token_ page, verify and click the **` CONFIRM `** button to add this token to your wallet. The new token will be available in the wallet for 30 days, after which you can add it again if needed. 

***

# How to Publish Smart Contracts

The wallet has the capability to publish smart contracts creating QRC20 tokens with **` Create Token `** or any other contract using **` Create Contract `**.

### Create Token

The **` Create Token `** menu option gives an easy way to create QRC-20 tokens using a built-in contract creation transaction.

Select **` Create Token `** on the menu and fill in the _Create Token_ form:

![2019-10 Create Token](https://i.imgur.com/KYOgnEd.jpg)

For _Token Name_ enter a descriptive name, here “My Test Token”. For _Token Symbol_ enter an appropriate symbol. The symbols are not unique, you can reuse any existing symbol name or make a new one.

Leave _Decimals_ set to the recommended 8 unless you have a good reason to change. With 8 decimals the tokens will be created in Satoshis, where the amount for 1.0 will be represented by 100,000,000 in the smart contract (move the decimal point 8 places to the left to convert Satoshis to units).

Enter the _Total Supply_ of tokens to create, 100 million is a typical number.

Leave _Gas Price_, _Gas Limit_ and _Fee_ set as is, unless you understand how to make changes. If _Gas Limit_ is set too low, the contract creation transaction will run out of gas and fail. For the default settings to the total fee for the token creation contract will be 2,500,000 x 0.00000040 + 0.01 = 1.01 QTUM, so the wallet must have at least this amount and any excess gas will be refunded.

Press the green **` CONFIRM `** button. On the _Do you confirm to create this Token_ screen review the raw transaction and press the blue **` CONFIRM `** button.

![2019-11 Do you confirm to create this token](https://i.imgur.com/UvD5aVc.jpg)

You will see the green _Successful send_ bar at the bottom of the screen:

![2019-12 Send Successful bar](https://i.imgur.com/ZbXEaF4.jpg)
 
Follow the link to see the contract creation transaction on the blockchain (after the next block is published).

Note that contracts are referenced using their address hash which is a 40-character hexadecimal address and just another way to represent a Qtum “Q” address.

From this point, you can add the new token to your wallet as shown above [Adding a QRC20 Token](https://github.com/qtumproject/documents/tree/master/en/QTUM-WebWallet-usage#adding-a-qrc20-token).

### Create Contract

**` Create Contract `** allows publishing of any kind of smart contract. To create the contract, start by writing Solidity code and compile to bytecode using a web IDE (Integrated Development Environment) like [qmix](https://qmix.blockchainspaceman.com/) or [remix](http://remix.ethereum.org) or a command line tool like [solar](https://github.com/qtumproject/solar).

Here is an example using the remix website at http://remix.ethereum.org for a contract which tracks name and age:
     
```
pragma solidity >= 0.5.1 < 0.6.0;   // use only these versions of Solidity

contract NameAndAge{
    
    string private name = "null";
    uint256 private yearsAge = 0;
 
    // set the age - transaction, requires gas
    function setAge(uint256 newAge) public {
        yearsAge = newAge;
    }
  
    // set the name - transaction, requires gas
    function setName(string memory newName) public {
        name = newName;
    }
    
    // get the age - not a transaction, no gas required 
    function getAge() public view returns (uint256) {
        return yearsAge;
    }

    // get the name - not a transaction, no gas required
    function getName() public view returns (string memory) {
        return name;
    }
}
```
      
To enter this contract into the wallet, the source code needs to be compiled to bytecode and the ABI (Application Binary Interface) created.

Copy and paste the Solidity code into _remix_ and press the **` Bytecode `** button to copy the bytecode into the clipboard, then save the results in a text file.

![2019-13 remix](https://i.imgur.com/6Db8Xay.png)

The actual bytecode (outlined in red below) begins with “6080” and is about 1,200 bytes in length.

![2019-14 bytecode](https://i.imgur.com/61fwWHg.jpg)

Also, press the **` ABI `** button to copy the ABI text into the clipboard and save to the same text file with the bytecode.

Now we can publish the contract. On the web wallet menu select **` Create Contract `**, copy and paste the bytecode (the hex string given by "object" as shown above) into the _Byte Code_ field. Leave the _Gas Price_, _Gas Limit_ and _Fee_ fields set for the default unless you understand how to change these. The default settings will give a fee of 2,500,000 x 0.0000004 + 0.01 = 1.01 QTUM. Your wallet will need at least this much QTUM to publish the contract. Press the green **` CONFIRM `** button to continue:

![2019-15 Create Contract](https://i.imgur.com/dJAyKga.jpg) 

On the next page _Do you confirm to publish this contract?_ review the raw transaction and press the blue **` CONFIRM `** button:

![2019-16 Do you confirm to publish this contract](https://i.imgur.com/nayWRoW.jpg) 

See the green _Successful send_ bar at the bottom of the screen. You can follow the link to see the contract create transaction on the Explorer (after the next block is published). 

![2019-17 Successful send](https://i.imgur.com/Ao1Dfek.jpg)  

From the contract creation transaction on the Explorer, copy the _Contract Address_ (40 hex characters) for use in the next steps:

![2019-18 Contract Address](https://i.imgur.com/Gpuc61C.jpg)

### Send to Contract

**` Send to Contract `** is used to change the memory values of the contract, for example, transferring tokens or changing storage for variables in the contract’s state database. The send to contract transaction requires a fee and gas payment, so you will need sufficient QTUM in the wallet. Continuing the above example we will send to contract to set the name and age.

On the menu, press **` Send to Contract `**. On the _Send to Contract_ page copy and paste the _Contract Address_ and the _ABI_ into their fields (the ABI for this contract is about 60 lines of text, the bottom few lines are visible in the scrolling window below).

On the _Method_ row (not shown below), click the drop-down arrow and select the _setName_ method, and in the _newName_ field enter the name to set, here "Nakamoto". Press the green **` CONFIRM `** button to continue.

![2019-19 Send to Contract](https://i.imgur.com/S0QDtdR.jpg) 

On the next _Do you confirm?_ page review the raw transaction and press the blue **` CONFIRM `** button to send the transaction:

![2019-20 Do you confirm](https://i.imgur.com/izdC8ci.jpg) 

See the green _Successful send_ bar, and you can follow the link to the Explorer to see the transaction (after the next block is published).

Use the same **` Send to Contract `** steps to select the _setAge_ method, enter a _newAge_ of 25 and send the transaction.

### Contract Call

Calling the contract reads state variables in the local copy of the blockchain (in the Qtum State database) for the web wallet’s server node (without the need for a transaction using gas) and gives an immediate result since there is no need to wait for the next block to publish. For contract calls enter the contract address and the ABI interface.

On the web wallet menu select **` Contract Call `**. On the _Contract Call_ page paste in the contract address and ABI. On the _Method_ row (not shown below) press the drop-down arrow and select the _getName_ method. Notice there are no fields for gas or fees since none are required. Press the green **` CONFIRM button `**:

![2019-21 Call Contract](https://i.imgur.com/2aAR0QL.jpg) 

The Result will come back immediately:

![2019-22 Result for getName](https://i.imgur.com/WlT49Bb.jpg) 

The contract data is in hexadecimal, converting “4e616b616d6f746f” hex to ASCII gives “Nakamoto” as set above.

Using the same **` Call Contract `** steps to select _getAge_ will return:

![2019-23 Result for getAge](https://i.imgur.com/goLbJfH.jpg)

Converting hexadecimal 19 to decimal gives 25 as set above.

***

# Address Delegation for Offline Staking

The web wallet can make an address delegation to a super staker for offline staking. 

First select and copy the address of a super staker from various listings and note the required fee.

In the wallet, select **` Offline Staking `** on the menu and press the blue "+" button to add a delegation. 

On the _Add Delegation_ page paste in the Staker Address (no trailing blank spaces), the Staker Fee and leave the other fields unchanged. There will be a 1.01 QTUM fee for the address delegation transaction, but some gas may be refunded. Click the **` CONFIRM `** button and see the confirmation. You can also see the delegation for the wallet address on the qtum.info explorer.

![Add Delegation](https://user-images.githubusercontent.com/29760787/91503274-10a2d000-e898-11ea-9f58-944b969b9ee4.jpg)

After the address delegation is published in the next block, reload the wallet to see the address delegation status. If you want to remove the delegation at some later time, click the red "x" button to remove the delegation.

![Offline Staking Status](https://user-images.githubusercontent.com/29760787/91503321-2ca67180-e898-11ea-9a63-0456f5a87258.jpg)

# Creating and Sending NFTs

The web wallet can create, send, and receive QRC1155 NFTs.

The **` Create NFT `** menu option will open the _CREATE NFT_ form. Fill in the fields as shown below.

![Create NFT blank form](https://user-images.githubusercontent.com/29760787/126523382-736fa5f0-23d7-4afe-be79-e2f3aec62d24.jpg)

In the thumbnail preview box, click “+” and select the content to load. Content can be still images in JPEG, GIF, and PNG format, and animations in GIF and webp format (video can be converted to GIF or webp format with an external program). File sizes up to 20 MB are allowed.

Enter the NFT Name, up to 100 characters. Enter the NFT Description up to 500 characters. Enter the NFT amount from 1 to 10 tokens. Leave the Gas Price, Gas Limit, and Fee set to the defaults unless you know how to change these. NFT minting takes around 300,000 gas and any excess is refunded. The wallet must hold QTUM to pay the fees, 1.01 QTUM per NFT minting.

Here is an example to create 5 NFTs of the Sydney Opera House:

![Sydney Opera House](https://user-images.githubusercontent.com/29760787/126523376-8e761cbc-b2c3-47b8-9455-1295ef1c41f7.jpg)

Click the **` CONFIRM `** button to create the NFTs. 

### Sending and Receiving NFTs

The **` View Wallet Info `** menu option will show any NFTs minted or received by the wallet. The blue circle in the upper right-hand corner of the thumbnail will show the quantity of each NFT, for example, we can see there are 5 of the Sydney Opera House NFTs. Click the thumbnail to see a larger NFT image.

![View Wallet Info](https://user-images.githubusercontent.com/29760787/126523377-2fcab451-fdec-411a-930c-95e4c030d0ad.jpg)

To send an NFT, on the _View Wallet Info_ form, click on the blue **` SEND `** button for that NFT and fill out the _send NFT_ form with the address and quantity, below sending one of the Sydney Opera House NFTs. Make sure the information is correct, then click the **` CONFIRM `** button to send the transaction:

![Send NFT](https://user-images.githubusercontent.com/29760787/126523381-ecc48249-89ee-43ba-8343-717efaf116e8.jpg)


