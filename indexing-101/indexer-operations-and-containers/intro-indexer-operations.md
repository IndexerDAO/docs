# Wallets Overview
It is crucial to understand that **wallets** are essential and necessary tools to securely manage and access Ethereum accounts. 

Ethereum wallets within the Web3 ecosystem are applications that function like physical wallets where your identification and assets are held. Wallets allow you to sign into apps, view balances, send transactions, and verify your I.D. 

> It’s helpful to think of wallets as windows to view and manage your assets on Ethereum, and _**not**_ as an Ethereum account. So, a wallet allows you to use the keys associated with your Ethereum account to interact with it. 

However, most wallet products will let you generate an Ethereum account, so you don't need one before you download a wallet. 

**Types of wallets:**
  - Physical hardware wallets are physical devices that allow you to keep your crypto offline and they are the most secure.
  - Mobile application wallets allow you to easily access your accounts.
  - Browser wallets are web applications that allow you to interact with your account directly on a browser.
  - Browser extension wallets are extensions that you download to interact with your account through a browser.
  - Desktop applications allow you to manage your funds from your macOS, Windows, or Linux system. 

_Keep this in mind as we move forward, and we review the differences between hot and cold wallets._

## Hot Wallets ##

----

Hot wallets are online wallets that are _**always**_ connected to the internet; they can be web-based, mobile, or a desktop app. They have private keys that grant you access to your blockchain address and all your digital assets. 

### Types of Hot Wallets: ###
  - Web Wallets: Allow you access to your account via web browser. They are provided by various online platforms such as MyEtherWallet, MetaMask, and Trust Wallet
  - Mobile Wallets: Apps that allow you quick on-the-go access to your account such as Trust Wallet and Coinbase Wallet

    **Pros:**
      - They are highly convenient
      - Give you quick access 

    **Cons:**
      - They are more vulnerable to cyber-attacks and hacks
      - They are considered less secure compared to cold wallets  

### Function & Security ###


You typically download and install hot wallets on your computer, smartphone, or use online wallet services.
When setting up the wallet, you generate a cryptographic key pair:
  - **Public Key:** Allows you to receive assets—this is the wallet address where others can send cryptocurrency to you.
  - **Private Key:** Authorizes direct access to assets within a blockchain address; it is used to access and control the funds in the wallet. This is a secret key that you must keep secure and never share with anyone. 

There are two broad categories of hot wallets, based on how you can access your account’s private keys: 

**Custodial wallets**, also known as hosted wallets or third-party wallets, are crypto exchange wallets like Binance and Coinbase. With this type of wallet, the third-party provider holds and manages your cryptocurrency assets on your behalf. They allow you to view your public keys, but the custodian or wallet provider controls the private keys. You access your wallet via login credentials, but it has no direct link to the address on the blockchain where your funds are stored. 
Essentially, you rely on the custodian to facilitate access. These types of wallets are designed to be user-friendly and more accessible. 

**Non-custodial wallets**, also known as self-hosted wallets, give you absolute control of your assets by leaving you in charge of the private key for this blockchain address. This means that you have direct access to your blockchain address, independently of the wallet. 
You get a seed phrase, a 12-word recovery phrase, when you set up the wallet. This seed phrase encodes your private keys and helps you regain access to the wallet if you lose your device. An example of a non-custodial hot wallet is Metamask. 

## Cold Wallets ##

---

Cold wallets, also known as cold storage solutions, are cryptocurrency wallets that are not connected to the internet. They are essential because they reduce the risk of hackers stealing your funds by providing iron-clad security against online attack vectors such as software viruses, clipboard malware, and smart contract bugs.

They protect your crypto by generating and storing private keys offline. It’s important to note that these keys are not the same as the seed phrase you generate every time you create a wallet (i.e., see hot wallets), but they are needed to sign a transaction and whoever holds them has authority to move that crypto to another address. 

### Types of Cold Wallets: ###
  - **Paper Wallets:** Physical documents that include a pair of private and public keys (and sometimes a QR Code address) designed to store cryptocurrency. You generate the keys offline and print a copy of them. Since it's a physical item, it's considered a basic, archaic wallet, but it is offline making it immune to online threats and a cost-effective way to store cryptocurrency and move it across borders. However, it must be stored securely to prevent physical theft or damage.
  - **Hardware Wallets:** Physical devices that use a secure smart card to generate and store cryptographic keys offline. The most popular hardware wallet companies are Ledger and Trezor, which build devices with screens and buttons that perform basic operations. They may require a physical connection with an external internet-connected device to initiate transactions or simply enable a secure connection via Bluetooth technology. They are the most widely adopted cold storage wallets because as long as you safeguard the wallet and seed phrase, there is minimal risk of losing funds to a security breach. However, you should purchase them from official sources to avoid human error in production or shipping. 
  - **Metal Wallets:** Are made of durable materials like metal but are like paper wallets and store cryptocurrency private keys. They are resistant to physical damage from fire or water.
  - **Offline Software Wallets:** These are installed on a computer that has never been connected to the internet. This isolation ensures that the wallet and its private keys are never exposed to online threats.
  - **Sound wallets:** Sound files on CDs, vinyl discs, or USB flash drives where you encrypt and record high-quality audio of your private key or seed phrase. You would generally set up a spectroscope application or device to decode the keys in the future. They are often considered an expensive way to store cryptocurrency. However, its primary appeal is that it encourages long-term storage since you go through a lengthy process to recover their private keys.
  - **Deep Cold Storage:** Deep cold storage is a bit more complicated. It involves storing your private key using a method that makes it relatively difficult to access. For instance, you may split seed phrases and keep them in several vault locations far from your home. High-profile individual or institutional investors may opt for third-party vault services that provide secure cold storage with multi-signature access to prevent unauthorized access. Others choose to use an immutable time lock contract (a.k.a. smart contracts) preventing access to the coins for a defined period. Sometimes, it could take a few days or even weeks to access your private keys depending on the storage location.


**Pros:**
  - Eliminate the risk of theft or hacking
  - Considered long-term storage of cryptocurrencies
  - Offer better security
    
**Cons:**
  - Cannot be accessed from anywhere since they’re offline

### Function: Regular Cold & Ultra-Cold Storage ###

There are two approaches to broadcasting signed transactions to the network when completing the transaction signing process: regular cold storage and ultra-cold storage.

**Regular Cold Storage** 

_What do you do?_

- You connect the offline cold storage wallet to another device with an internet connection using a USB cable. 
  - This enables you to plug the hardware wallet into MetaMask to sign transactions, which allows you access to smart contracts. You can provide liquidity, vote on governance proposals, and even take out loans. Every transaction requires you to enter a pin on the device manually. 

_What are the potential risks?_

Although it is more secure than hot wallets, any USB connection can expose your device to malware.

_What are the benefits?_

Each initiated transaction is temporarily transferred to the secure offline space on the wallet, which stores the private key. The transaction is signed and returned to the online environment before being broadcast on the blockchain network. This process takes place in a matter of seconds. 

**Ultra-cold Storage** 

_What do you do?_

- You have to manually broadcast a signed transaction to the network.
  - Some wallets, like Ellipal, use digital screens to make this process more user-friendly. With this type of wallet, when you want to send a transaction, you enter the receiver’s address on the device and sign the transaction. The device then transforms that signed transaction into a QR code that can be scanned with an internet-connected device. Once you have the signed transaction, you can then broadcast it to the network.

_What are the potential risks?_

Because this type of wallet is completely isolated from any device capable of internet connectivity, they are not as convenient as hot wallets, and they require several steps to complete transactions. Additionally, the assets stored within this type of wallet remain untouched for a relatively long time. 

_What are the benefits?_

They function as a type of vault that cannot be easily accessed which strengthens its security. 

>Reports confirm that over 80% of bitcoin’s supply is held in cold storage, which makes it a popular choice among bitcoin investors. 
Additionally, cryptocurrency-related businesses such as exchanges and custodians also adopt various forms of institutional-grade cold storage solutions.

Overall, a cold wallet can provide even greater security by integrating multi-signature support and additional passphrases.

## Multisig Wallets ##

Multisignature wallets, also sometimes called multisig vaults or safes, require two or more private keys to perform certain tasks. This increases the security of the funds stored in the wallet because it requires multiple parties to sign before sending any transactions. 

The process of a multisig wallet works by requiring multiple signatures from a set of predetermined addresses, and if any one of these signatures is missing, the transaction will not be able to go through. 
_Think of it as a safe with unique keys that must be used together to open it._

### Types: ###

**Type one:** Require all parties to attest or sign to a transaction, most commonly three-key wallets

**Type Two:** Require a certain number out of the total pool to participate for a transaction to process, for example, two of three or three of five

**Important Distinction**

The process of signing transactions on multisig wallets has a different key design from traditional wallets. Traditional wallets are known as externally owned accounts (EOA), meaning they are generated by users and controlled by private keys. EOAs are generally considered to be _user accounts_, meaning they are created for members of the general public to interact with blockchains.

Multisig wallets, on the other hand, are smart contract-based wallets. Rather than being endpoints controlled by a user, these smart wallets are controlled by code and governed on-chain by their owners. Because of this setup, multisig wallets are considered a _seedless_ form of self-custody. 

**Pros**
  - Provide a better experience for institutions and DAOs
  - No ‘key person’ risk
  - Greater transparency
  - Buildable 

