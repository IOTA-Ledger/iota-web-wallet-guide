# Using Ledger Hardware Wallet With IOTA

This is an application for the Ledger Nano S Hardware Wallet to be used for securely storing the IOTA cryptocurrency.

If you have any questions or encounter any unexpected behavior with the app please contact us in [our discord](https://discordapp.com/invite/SEdaqG9).

### You will need:
1. Ledger Nano S already initialized with [up to date firmware](https://support.ledgerwallet.com/hc/en-us/articles/360002731113)
2. IOTA currency

### Installation:
1. Install [Ledger Live](https://www.ledger.com/pages/ledger-live)
2. After downloading, go through the initialization steps
3. Once initialized, click “Manager” on the left side of the window
4. Find IOTA and click “Install”

The IOTA app should now be installed. If you encountered an error during installation, it could mean your device is not up to date, or there isn’t enough room on the device for the app. If you run into issues, get a hold of us in [our discord](https://discordapp.com/invite/SEdaqG9) and we will try to help you.

## Terminology:
IOTA uses what are called “seeds”. Each seed can have many different addresses, but each address is used only once and these addresses are referenced by their “index” on the seed. For instance the address at index 0 will be different from the address at index 5.

IOTA sends transactions in what are called “transaction bundles” and every bundle must have a net value of 0. Furthermore, either the entire bundle is accepted (and all transactions within it), or the entire bundle is rejected.

There are three types of transactions: output, input, and change. Input transactions must always take all the funds on the address. If there are leftover funds after sending to the output address, the remainder must go to a new address called the “change address”.

### Example:
- Output: 60 iota
- Input 1: 40 iota
- Input 2: 45 iota
- Change: 25 iota

Neither input on their own has enough balance to cover the output so both must be used. But it leaves a remainder of 25 iotas, so these must be sent to a new address. Now the bundle is balanced, with a net value (out minus in) being 0.

IOTA uses “change addresses” because once an address has been spent from, its signature is partly exposed. This is called signature reuse which can lead to an attacker forging the signature and stealing any funds left on the address. As such, it is imperative that once you spend from an address you ensure nobody sends funds to the address any more. Most modern wallets should ensure the destination address has never been spent from before.

For more information on how IOTA works visit https://iota.org/sec.

## Usage:
The IOTA app uses the left button to move up in the menu, the right button to move down in the menu, and both buttons (simultaneously) to mean “confirm” or “back”. 

Most of the time a “double button press” will be denoted with two small lines just below the buttons. The exception is when displaying a text menu, in which case it will confirm the current menu option, or it will take you back to the previous menu. It should be intuitive when and what a “double button press” will do.

1. Launch the IOTA application on the Ledger Nano S
2. Scroll down (right button) on the initialization screen, and on the last piece of text press both buttons to confirm you understand
3. Visit https://semkodev.gitlab.io/romeo.html using Chrome or Opera to access the web wallet
4. Select the “Ledger Nano” tab and then “Login with Ledger”
5. The wallet will now grab one or more addresses from the Ledger Device, and the address will be displayed on the right
6. The balance will appear beside the address on the right, and the total balance for the “page” will appear at the top next to this symbol: 
    - The Romeo web wallet uses “pages” as new seeds, so if it starts taking too long to sync the transactions, create a new page which will move everything to a brand new seed.
7. In order to send a transaction click the green paper airplane icon along the top: 
8. Enter the output address, an (optional) tag, and the amount to send and press the big green button “Next: Select source addresses”
    - If you would like to go back to the main screen, click on “Page 1” near the top of the screen: 
9. By default “Automatic source selection” will most likely be used. If you have multiple addresses with balance and want to specifically choose which address to take funds from, deselect it to manually choose the input address(es) then click “Next: Confirm transfer”
10. Review the transaction and click “Send transfer(s)”
11. The wallet will then send the transaction bundle to the Ledger application. Once it is fully received, the device will display the transaction bundle on its screen beginning with the output amount.<br>
Each transaction in the bundle is broken up into two parts, first will come the output/input/change amount, followed by the corresponding address.<br>
Pressing both buttons on any output/input/change screen will toggle the value between the abbreviated amount and the full amount (eg. 5.23 Ki will then read 5,232 i).<br>
Pressing both buttons on any address screen will toggle between the short version of the address, and the full address. The short version of the address will show the first four letters, the last four letters of the address, as well as a checksum for the entire address. The checksum is just an easier way to verify the entire address is correct without having to check letter by letter, however currently Romeo (the web wallet) does not display the checksum. This is fine - just verify the address the good old-fashioned way, and in the future we hope wallets will support checksums.<br>
When displaying an Input or Change transaction, it will show “Input: [0]”. Between brackets is the index of the address (verified to be on the seed by the device itself). Verify that the inputs and especially the “Change” index are what you expect them to be.<br>
On an input or change address (the full address), if you scroll to the bottom, you will see the BIP path used to generate said address. It will look something like “ 2c’|107a’|0’|0’ ”. This  is used by the device to define which seed these addresses belong to.<br>
Use the right button to scroll through the whole transaction bundle, and then select either “Approve” or “Deny”.
12. If you selected approve, it will then generate the required signatures and send them to the host machine to be broadcast to the tangle.
13. After a few moments, verify using a tangle explorer (eg. https://thetangle.org or https://iotasear.ch) that your transaction was successfully broadcast to the network. If it was not, exercise caution when proceeding to ensure you don’t re-sign the same transaction with a new signature (weakening the signature).

### Notes:
Inputs and change addresses are always verified to belong to the device itself and cannot be external addresses. As such, the most important pieces of information to verify each and every time you send a transaction, are the output amount, the output address, and the change index.

If the device and wallet lose connection (if the device gets unplugged or the wallet times out waiting for a response) you must log out of the wallet and log back in.

Use the “Ledger” button below the addresses to display the address on the Ledger. If the address on the Ledger is correct, that means it belongs to the Ledger (and isn’t a malicious address).

## Security:
Don't rush through signing a transaction.
When generating a transaction for the Ledger to sign, you will scroll through each transaction before signing off on the bundle. The transaction information will come up in order (while scrolling from left to right). The first screen will display the tx type (output, input, or change), as well as the amount. The next screen will display the corresponding address for said transaction. This will repeat until all transactions have been displayed, then you can select "Approve" or "Deny".
- All output transactions to 3rd party addresses will say "Output:" and below that "1.56 Mi" (for example). "Output" being the key word here.
- All input transactions will say "Input: [0]", and the final output transaction (the change transaction) will say "Change: [4]" ([4] being the seed-index of the change tx). This means the Ledger has verified the addresses used for inputs as well as the change tx all belong to the Ledger.
- If the input amount perfectly matches the output amount, there will be no change transaction. If there is no change transaction, double check that you are sending the proper amount to the proper address because there is no remainder being sent back to your seed.
- Note: When transferring from one seed (controlled by the Ledger device) to another seed (also controlled by the Ledger device) it will not display a "Change tx". As such the wallet should first display the address on the new seed that it intends to send it to on the Ledger (thus verifying it belongs to the Ledger), and then create the transaction. The user would then verify in the transaction that the "Output:" tx is in fact going to the address previously displayed on the Ledger.

Verify ALL information in a transaction and NEVER re-sign a transaction.

For other coins you only need to verify the destination address and amount, but for IOTA you must also verify all input transactions. If you sign a transaction on the Ledger but the transaction is not using all of the funds on a specific address, leftover funds on the address are then vulnerable.

As such make sure the input amount(s) are what you expect them to be, make sure the output destination and amount is what you intend to send, and make sure there is a change tx if applicable with all of your remaining funds.

Note: After signing a transaction, you should verify the transaction was successfully broadcast to the network. You should NEVER re-sign the same transaction on the Ledger. If the transaction does not get confirmed, you should promote the transaction on the host machine. This avoids generating a new signature and weakening the security of the addresses.
If the transaction was not broadcast to the network, and you can't find it in the wallet you should be EXTREMELY CAUTIOUS before proceeding to sign a new transaction. If an infected machine is silently storing the signatures without broadcasting them, it could steal your funds after re-signing.
If this situation should arise you should consider going to a more trusted machine before re-signing a transaction.
