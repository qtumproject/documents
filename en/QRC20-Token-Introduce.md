# QRC20 Token

## About QRC20

QRC20 is the implementation of a standard API for tokens within smart contracts on Qtum，basically it is the same as [ERC20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md).
<br>
Methods and Events：

```
function name() constant returns (string name)
function symbol() constant returns (string symbol)
function decimals() constant returns (uint8 decimals)
function totalSupply() constant returns (uint256 totalSupply)
function balanceOf(address _owner) constant returns (uint256 balance)
function transfer(address _to, uint256 _value) returns (bool success)
function transferFrom(address _from, address _to, uint256 _value) returns (bool success)
function approve(address _spender, uint256 _value) returns (bool success)
function allowance(address _owner, address _spender) constant returns (uint256 remaining)
event Transfer(address indexed _from, address indexed _to, uint256 _value)
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```

# Creating QRC20 Tokens

You can use [QRC20Token](https://github.com/qtumproject/QRC20Token) code to create your own QRC20 token on Qtum. For this example, we will use Qtum testnet, first getting some testnet QTUM.

After installing the Qtum Core wallet from https://qtumeco.io/wallet or https://github.com/qtumproject/qtum/releases, get the wallet receiving address by selecting **Window** - **Receiving addresses**, select and copy the wallet receiving address qXGdYmLypZRy8pTpj9EdTBHkqtv6cv99ky.

![1  Copy Receiving Address](https://user-images.githubusercontent.com/29760787/83460974-acf23d80-a435-11ea-9d5f-80b22249003e.jpg)

We need some QTUM to pay for the smart contract gas and transaction fees and can get some testnet QTUM from the [Qtum Testnet Faucet](http://testnet-faucet.qtum.info/). Paste the receiving address into the faucet address field and press the blue checkmark button.

![2  Testnet Faucet](https://user-images.githubusercontent.com/29760787/83460980-b11e5b00-a435-11ea-9892-2b344bdc2611.jpg)

Next, copy the token code at [QRC20Token](https://github.com/qtumproject/QRC20Token). In the QRC20Token.sol file you can change `name`, `symbol`, and `totalSupply` to your preference. For this example, we will edit later to name the token "QRC TEST 527", the symbol "QT527" and have a total supply of 1,000,000,000 which is entered as "10 * * 9". We will leave `decimals` set for 8, to give 8 decimal places for each token, so for example, you should send a 1.12345678 token amount. 

![3  Solidity](https://user-images.githubusercontent.com/29760787/83460987-b380b500-a435-11ea-8a10-c8a070180fc5.jpg)

After editing the Solidity file, save it locally or just copy to paste into Remix.

Next, we will use Remix to compile the Solidity code into bytecode. In a browser, go to Remix at http://remix.ethereum.org/ and select the SOLIDITY Environment.

![4  Select Solidity](https://user-images.githubusercontent.com/29760787/83460993-b67ba580-a435-11ea-8ca0-fd5a39a43a66.jpg)

Click the "+" button to create a new file.

![5  New File](https://user-images.githubusercontent.com/29760787/83460998-ba0f2c80-a435-11ea-9dd2-9e778321e74a.jpg)

Enter the file name "QRC20Token.sol" and "OK" to create a new file. 

![6  Enter File Name](https://user-images.githubusercontent.com/29760787/83461007-bd0a1d00-a435-11ea-868d-45bf6a0470da.jpg)

Paste in the source code from the QRC20Token.sol file.

![7  Paste in Code](https://user-images.githubusercontent.com/29760787/83461013-c0050d80-a435-11ea-84d7-fac39301d0e6.jpg)

Here you can see the code has been edited to name the token "QRC TEST 527", with the symbol "QT527", and a supply of 1 billion.

Also, create a new file, enter the file name "SafeMath.sol" and paste in the code for [SafeMath.sol](https://github.com/qtumproject/QRC20Token/blob/master/SafeMath.sol).
 
Select the compiler button on the left side.
 
![8  Compiler](https://user-images.githubusercontent.com/29760787/83461029-c4312b00-a435-11ea-8655-b99a41a84103.jpg)

The compiler tab is shown below. You can leave the Solidity version set for 0.4.26. At the top, click the tab for QRC20Token.sol to select that file to compile, and click the blue **Compile QRC20Token.sol** button to compile the source code into bytecode.

![9  Run Compiler](https://user-images.githubusercontent.com/29760787/83461047-c72c1b80-a435-11ea-9df4-6dbc3d106327.jpg)

Ignore the warnings.

Click on the Bytecode button to copy the bytecode.

![10  Copy Bytecode](https://user-images.githubusercontent.com/29760787/83461057-cabfa280-a435-11ea-9cad-c02cb59b1b94.jpg)

Paste the copied bytecode into a text editor, and select just the numeric characters for the object code (shown here highlighted in blue). The object code starts with "60806" and ends with "00029" (not shown in this image).

![11  Get Object](https://user-images.githubusercontent.com/29760787/83461066-cdba9300-a435-11ea-953c-6dacb3b8fdf8.jpg)

On the wallet, go to **Smart Contracts** - **Create** and paste the copied object code into the "Bytecode" field.

![12  Paste in Bytecode](https://user-images.githubusercontent.com/29760787/83461070-d01ced00-a435-11ea-8a75-b11427e66f42.jpg)

At the bottom of the Create Contract form, click the drop-down on "Sender Address" and select qXGdYmLypZRy8pTpj9EdTBHkqtv6cv99ky. This sets the address to be used by the contract. Leave the gas set at 25000000 and price set at 0.0000040 unless you know how to safely change these. Click the **Create Contract** button and **Yes** to send the transaction. 

![13  Select Address](https://user-images.githubusercontent.com/29760787/83461072-d27f4700-a435-11ea-9ce2-8bb9f5248f8a.jpg)

The wallet will confirm the transaction on the "Result 1" tab. Copy the Contract Address 137d046beb3cb66c0cdd389bf8bab4faeae16c0b.

![14  Results](https://user-images.githubusercontent.com/29760787/83461083-d7dc9180-a435-11ea-80f1-f3dbe66de36a.jpg)

The wallet Transactions page will show the transactions so far. First, the wallet received 90.0 QTUM sent from the Testnet faucet. Next, the contract create transaction sent the contract bytecode and fees of 1.01414 QTUM. Finally, the wallet received a gas refund of 0.623456 QTUM. Gas refunds are sent in the coinstake transaction, so they are show as "mined" in the wallet and must mature for 500 blocks before they can be used. 

![15  Transactions](https://user-images.githubusercontent.com/29760787/83461085-da3eeb80-a435-11ea-8259-e1a6165cd22b.jpg)

You can also see the contract create transaction on [testnet.qtum.info](https://testnet.qtum.info/tx/0db7a5f38c1959d473405165bf842dcf726c9b79615b0b294514cb44e53fb801)

![16  Explorer](https://user-images.githubusercontent.com/29760787/83461088-dca14580-a435-11ea-94c6-f6fd9c3eaf01.jpg)

The transaction was sent with 2,500,000 gas at price of 0.00000040 QTUM. The contract creation used 941,360 gas giving a gas refund of 2,500,000 - 941,360 = 1,558,640 at price of 0.00000040 or 0.623456 QTUM for the refund. 

# Adding Tokens

Smart contract transactions are sent to the smart contract address, not the wallet address, and for the wallet to see or make smart contract transactions we must inform the wallet, in this case by "adding" the token. To see the new token in the wallet, select **QRC Tokens** and the "**+**" button to the right of the Add new token.

![17  Add Token](https://user-images.githubusercontent.com/29760787/83461094-e034cc80-a435-11ea-84f9-79e01860fc9f.jpg)

Paste the contract address 137d046beb3cb66c0cdd389bf8bab4faeae16c0b into the "Contract Address" field, and rest of the form will be autofilled. At the bottom of the form click the drop-down arrow to the right of the Token address field and select qXGdYmLypZRy8pTpj9EdTBHkqtv6cv99ky and **Confirm**. If the wallet is using multiple addresses, chose the correct Qtum address that was used to create the token.

![18  Paste Contract Address](https://user-images.githubusercontent.com/29760787/83461105-e3c85380-a435-11ea-8e0f-680bc1d8a175.jpg)

You will see the Log events prompt "Enable log events from the option menu to receive token transactions". We will do this step below.

![19  Log Events](https://user-images.githubusercontent.com/29760787/83461112-e75bda80-a435-11ea-9acb-e8a68a6d7a28.jpg)

# Sending Tokens

To send QRC20 tokens, select **QRC20 Tokens** and **Send**. Note there is single row listing for the QT527 token tied to address qXGdYmLypZRy8pTpj9EdTBHkqtv6cv99ky here, but tokens could be tied to different addresses of this wallet, in which case they would be listed individually and need to be sent individually.

Fill in the fields for "PayTo" and "Amount". The "Description" field is optional. Click **Send** and **Yes** to complete the transaction.

![20  Send QRC20 Tokens](https://user-images.githubusercontent.com/29760787/83461124-eaef6180-a435-11ea-9c19-828ce6237e90.jpg)

Wallet **Transactions** will now show the contract send transaction. Right-click on the transaction to see the details including the transaction ID.

# Enable Log Events

We can follow up now on the previous prompt to enable log events. For the wallet to fully display token transactions it needs to have log events enabled. Select **Settings** - **Options** and click to select **Enable log events**. You must restart the wallet and rescan. The prompt will show "Client restart required to activate changes." Select **OK** then **Yes**. The wallet will exit, then restart the wallet. 

![21  Enable Log Events](https://user-images.githubusercontent.com/29760787/83461137-edea5200-a435-11ea-94f1-e1e6865ad27c.jpg)

When the wallet restarts, click **OK** to rebuild the block database. 

The wallet status will show "Reindexing blocks on disk..." and "Syncing headers" for several minutes or several tens of minutes, depending on your computer. 

![22  Restarting Rebuild Database](https://user-images.githubusercontent.com/29760787/83461141-f04cac00-a435-11ea-8059-ed8939ddb339.jpg)

# Multiple Tokens in Wallet

QRC20 token balances are managed by the smart contract for individual Qtum addresses, even if these Qtum addresses are for the same wallet.

Continuing the example above, we sent 500 QT527 tokens to the wallet on a new receiving address qRdxBZSvUx1edUfygyHr35mVgmX9pAMLrZ. To show this new transaction of QT527 tokens in the wallet we must complete the Add Token step for this new address.

![23  Add 2nd Token](https://user-images.githubusercontent.com/29760787/83461152-f2af0600-a435-11ea-9d6a-5daae2e2a33c.jpg)

Now the tokens for each tied address are shown separately and each row can be used separately for send and receive operations.

![24  Two QRC20 Tokens Listed](https://user-images.githubusercontent.com/29760787/83461156-f6db2380-a435-11ea-9047-fbe52dcd9106.jpg)

***
