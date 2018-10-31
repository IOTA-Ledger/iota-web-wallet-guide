# Using Ledger Hardware Wallet With IOTA

This guide explains how to secure IOTA tokens with a Ledger Nano S Hardware Wallet.

If you have any questions or encounter any unexpected behaviour please contact the development team on
 [our Discord server](https://discordapp.com/invite/SEdaqG9).

### You will need:
1. Ledger Nano S already initialized with [up-to-date firmware](https://support.ledgerwallet.com/hc/en-us/articles/360002731113)
2. IOTA currency

### Installation:
1. Install the [Ledger Live](https://www.ledger.com/pages/ledger-live) application.
2. Complete the setup process.
3. Once set up, click "Manager" in the left-hand menu and follow the instructions.
4. Find IOTA and click "Install".

The IOTA app should now be installed. If you encountered an error during installation, it could mean your device is not up to date, or that it has insufficient space. If you run into any issues, get in touch on [our Discord server](https://discordapp.com/invite/SEdaqG9), and we will try to help you.

## Usage
In the IOTA app the left button is used to navigate up in the menu, the right button to navigate down, and both buttons simultaneously to "confirm" or "go back".

Most of the time, a "double button press" is prompted by two horizontal lines at the top of the Ledger screen. And in a menu, a "double button press" will either confirm the selected-menu option, or take you back to the previous menu. 

What button(s) to press and when should be intuitive.

1. Launch the IOTA application on the Ledger Nano S.
2. Scroll down (right button) on the initialization screen, and on the last piece of text press both buttons to confirm you understand.
3. Visit https://semkodev.gitlab.io/romeo.html using Chrome or Opera to access the web wallet.
4. Select the "Ledger Nano" tab and then "Login with Ledger".
5. The wallet will now generate one or more addresses on the Ledger Device. The address(es) will be displayed on the right-hand side.
6. The balance is displayed next to each address, and the total balance for the "page" is displayed at the top, next to this symbol: ![balance](/media/balance.png)
    - Note: The Romeo web wallet uses a paging system. If transaction syncing takes too long, create a new page. This will automatically move your funds to a brand new seed secured by your Ledger device.
7. In order to send a transaction click the green send icon: ![send](/media/send.png)
8. Enter the output address, an (optional) tag, and the transaction amount. Then press the big green button "Next: Select source addresses".
    - If you would like to go back to the main screen, click on "Page 1" near the top of the screen: ![page1](/media/page1.png)
9. "Automatic source selection" will be used by default. If you have multiple addresses with balance and want to specifically choose which address to use as inputs, deselect this setting and manually choose the input address(es). Then click "Next: Confirm transfer".
10. Review the transaction and click "Send transfer(s)".
11. The Ledger device will display the full transaction bundle. You MUST understand what this means, so that you can verify your transaction on the device. 

Please read [Terminology](#terminology) and [Security](#security) before continuing.

Please note, Romeo does not currently display address checksums. This is fine - just verify the address the old-fashioned way, checking letter by letter.

Use the right button to scroll through the whole transaction bundle, and then select either "Approve" or "Deny".

12. If you selected approve, your Ledger device will generate the required signatures and send them to the host machine to be broadcast to the Tangle.
13. After a few moments, verify that your transaction was successfully broadcast to the network using a Tangle explorer (e.g. https://thetangle.org or https://iotasear.ch).

### Notes:
If the device or wallet loses connection (e.g. the device is unplugged or the wallet times out waiting for a response) you must log out and log back in to Romeo.

Use the "Ledger" button below the addresses to display the address on the Ledger. If the address on the Ledger device is correct, that means that it belongs to the seed controlled by the Ledger device (and is not a malicious address).

## Terminology

#### Seed:
An IOTA seed is the key to your funds. When using a Ledger Nano S with IOTA, your seed is secured by the Ledger device.

#### Addresses:
Each seed can have many different addresses, but each address is used only once. Addresses are referenced by their "index" i.e. the address at index 0 will be different from the address at index 5.

#### Output, input, and change transactions:
A transaction involves a transfer of value to or from an address. There are three types of transactions: output, input, and change. An input transaction takes all the funds on an address. The funds are sent to the destination address in an output transaction. And if there are leftover funds between input and output transactions, the remainder is sent to a new "change" address.

#### Bundle:
IOTA sends transactions in "bundles". The bundles are comprised of input, output and change transactions. Bundles must have a net value (sum of inputs and outputs) of 0. 

#### Bundle example:
- Output: 50i
- Input 1: 30i
- Input 2: 40i
- Change: 20i

On their own, neither input address (30i and 40i) has enough balance to cover the output (50i) transaction, so both inputs must be used. This leaves a remainder of 20i (output minus inputs), which is sent to a new change address. The bundle is balanced, with a net value of 0.

IOTA uses "change addresses" because once an address has been spent from, its signature is partially exposed. Address reuse could enable an attacker to forge the signature and steal any funds left on the address. It is essential that once you spend from an address, no more funds should be sent to that address. Most wallets, including Trinity, will ensure that you are protected from address reuse.

For more information on how IOTA works and using a Ledger device with IOTA visit https://docs.iota.org and https://github.com/IOTA-Ledger/blue-app-iota/blob/master/README.md.

## Security
**Do not rush through sending a transaction. Take your time to verify the transaction bundle.**

When signing a transaction with your Ledger device, you will scroll through the full transaction bundle before approving it. The bundle information is displayed in order, scrolling from left to right.

The first screen will display the transaction type (output, input, or change), and the amount. The next screen will display the corresponding address for that transaction. This is repeated for every transaction in the bundle. You can then select either "Approve" or "Deny".

- Output transactions display "Output:" and the amount e.g. "1.56 Mi". "Output" is the key word here.
- All input transactions will look like "Input: [1]". The number between brackets is the seed index of the address used in the transaction.
- The change transaction will look like "Change: [4]".
- If the input amount matches the output amount, there will be no change transaction. If there is no change transaction, double check that you are sending the correct amount to the correct address.

### Checklist:
When using other currencies with a Ledger device you only need to verify the destination address and amount. But with IOTA you must also verify all input transactions. 
1. Verify ALL the information in a transaction and NEVER sign the same input twice.
2. Make sure the output address and amount match what you intend to send.
3. Make sure the input amount(s) match what you expect.
4. Make sure there is a change transaction, if applicable, with all remaining funds.
5. Verify that the transaction was successfully broadcast to the network.
    - If the transaction does not confirm, promote the transaction through your wallet software. 

#### Extra notes:
- Pressing both buttons on any output/input/change transaction will toggle between abbreviated and full amounts (eg. 5.23 Ki will then read 5,232 i). Pressing both buttons on any address screen will toggle between abbreviated and full addresses. A checksum (the last 9 characters of the address) is displayed for simpler address verification.
- When transferring between two seeds both controlled by the Ledger device, no change transaction will be displayed. You must verify that the "Output:" transaction is being sent to the address previously displayed on the Ledger device.
- When displaying a full input or change address, scroll to the bottom to view the BIP path used to generate that address. It will look something like `2c’|107a’|0’|0’`. The device uses this path to define which seed the address belongs to.
