# GamePower Wallet Template

## Project Overview :page_facing_up:

The `GamePower Wallet` is a multi-chain non-custodial mobile wallet which will allow users to claim, store and manage an unlimited number of tokenized assets from any Substrate based blockchain. This project will consist of 3 major parts: the mobile wallet for users, the javascript sdk for front-end developers to create NFTs and a substrate pallet for connecting chains with the wallet.

<u>**Users:**</u> By scanning QR codes, users will be able to claim NFTs into their wallet. These NFTs can be consumed (burned), listed for sale or sent to others. Users will also have the ability to mint NFTs from within the mobile app. The mobile app will be downloadable from Apple's App Store and Google's Play Store.

<u>**Substrate developers:**</u> By adding the `gamepower-wallet` pallet to their substrate runtime, developers will allow the GamePower Collectibles Wallet to connect to their blockchain. The pallet will expose an interface for the wallet to manage NFTs.

<u>**Front-end developers:**</u> By using the `gamepower-wallet-javascript-sdk`, javascript developers can create a UI for creating new NFTs. This javascript sdk will be able to connect to any substrate node via Polkadot.js.


### Overview

The reason we are creating the NFT Collectibles Wallet is to allow users of GamePower Network (https://www.gamepower.network) to claim NFTs from games published on the platform. We could have made the wallet closed sourced such as other projects (Enjin Wallet), but we decided since we are the new kids on the block, it is better for us to contribute to the Substrate/Polkadot/Kusama community. That is what excites us so much about this project.

Our team is very passionate about gaming and NFTs. We believe the use case for NFTs in gaming is one of the most valuable in crypto right now. The problem we see with NFTs is that explaining NFTs to the general consumer and giving them a streamlined and friendly place to use those NFTs is lacking. We want to solve this with the NFT Collectibles Wallet.

By allowing Substrate developers to integrate our module into their runtime, they can also take advantage of this wallet and offers users of their blockchain the same streamlined experience we will offer users for the GamePower Network.

## Project Details
---
## **Mobile Wallet Details:**

The mobile wallet will be built using `React Native`. We feel this will allow us to use a coding language (javascript) we've used for years and build performant mobile applications. Using React Native also allows us to code once and deploy on multiple mobile platforms.

Mobile Stack:
- React Native
- Polkadot.js
- react-qr-scanner

A mockup of our mobile wallet UI. This mockup outlines the wallet creation, QR scanning and collectibles viewer.
![img](https://github.com/GamePowerNetwork/nft-collectibles-wallet/raw/open-grant/images/Mobile_App_Wireframe.png)

## **Substrate Pallet Details:**

The `nft-wallet-pallet` will use ORML (open runtime modules library: https://github.com/open-web3-stack/open-runtime-module-library) which will provide us with some underlying NFT code. The pallet will also talk to the balances pallet to handle any minting and consuming which is needed since each NFT is minted with a type of currency native to the blockchain it is on.

Substrate Stack:
- Substrate
- ORML

These methods will serve as an interface for the NFT Wallet to communicate with any substrate runtime. `nft-wallet-pallet` expects ORML's nft pallet to be a part of the runtime since it will be used to handle all NFT related functions.

We will expose TRANSFER, BURN and CLAIM callbacks so that the runtime can do any domain specific logic when sending or burning an NFT.


## **Javascript SDK Details:**

The front-end UI will be built using React + Polkadot.js. This will be a straight-forward and clean UI to allow the creation and management of NFTs. This UI is not a front-end for consumers but for developers to create NFTs. The underlying SDK for the front-end can be used to create any type of custom NFT management UI.

Web Stack:
- React
- Polkadot.js

Mockup of the admin frontend.
![img](https://github.com/GamePowerNetwork/nft-collectibles-wallet/raw/open-grant/images/Admin.png)


### Ecosystem Fit

The NFT Collectibles Wallet provides the ecosystem with a streamlined and standard way to create, manage and exchange NFTs. By allowing the wallet to connect to any substrate based chain, users can freely move around the ecosystem without downloading multiple wallets for each chain, while still having a wallet that focuses specifically on collectibles.


## Run in Docker
---
First, install [Docker](https://docs.docker.com/get-docker/) and
[Docker Compose](https://docs.docker.com/compose/install/).

Then run the following command to build the docker image.

```bash
docker build -t gamepower-wallet:0.0.1 .
```

Next you can run the image in a container using the following command

```bash
docker run -p 9944:9944 gamepower-wallet:0.0.1
```

## Interacting on Polkadot.js.org
---
You can access your local running docker container here: [Polkadot.js Local Node](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944)

### STEP 0
>Before we begin, there are some types that need to be added to the polkadot.js app. You can enter these types under `Settings -> Developer`

```
{
  "ListingId": "u64",
  "ClaimId": "u128",
  "Asset": {
    "ClassIdOf": "ClassIdOf",
    "TokenIdOf": "TokenIdOf"
  },
  "ListingOf": "Listing",
  "Listing": {
    "id": "ListingId",
    "owner": "AccountId",
    "asset": "Asset",
    "price": "Balance"
  },
  "OrderOf": "Order",
  "Order": {
    "listing": "ListingOf",
    "buyer": "AccountId",
    "block": "BlockNumber"
  },
  "ClaimOf": "Claim",
  "Claim": {
    "receiver": "AccountId",
    "asset": "Asset"
  },
  "WalletClassData": {
    "metadata": "Vec<u8>"
  },
  "WalletAssetData": {
    "metadata": "Vec<u8>"
  },
  "TokenInfo": {
    "metadata": "Vec<u8>",
    "owner": "AccountId",
    "data": "WalletAssetData"
  },
  "ClassInfo": {
    "metadata": "Vec<u8>",
    "total_issuance": "TokenId",
    "owner": "AccountId",
    "data": "WalletClassData"
  }
}
```
### STEP 1
Once here, visit `Developer -> Extrinsics` tab. Here you can select `Bob` as your selected account

Select the `gamePowerWalletIntegration` module and the `createClass` method as shown below.

You must have at least 1 asset class and token available to perform this test. Enter the data and submit the transaction.
<p align="center">
  <img alt="step1" src="/images/step1.png">
</p>

### STEP 2
Select the `mint` method and add any meta data or properties that you like, set the quantity. Then submit the transaction.
<p align="center">
  <img alt="step2" src="/images/step2.png">
</p>


### STEP 3
Now let's actually do something cool. Select the `gamePowerWallet` module and the `list` method as shown below. We will use this to sell the NFT on the market.

Enter the id of the class we create 0 and token id we just created which is 0..(quantity minted). Finally set a price for this asset on the market and submit the transaction.
<p align="center">
  <img alt="step3" src="/images/step3.png">
</p>

### STEP 4
If you go to the `Network -> Explorer` tab you will see our listing event under `recent events`. Here you can also see the ListingId which is 0. Let's use this.
<p align="center">
  <img alt="step4a" src="/images/step4a.png">
</p>

You can also go to `Developer -> Chain state` tab and you will see under `gamePowerWallet` storage that we have a listing with the supplied data. Leave the ListingId field blank to see all of the listings in storage.
<p align="center">
  <img alt="step4b" src="/images/step4b.png">
</p>

Let's use that ListingId back on the `Extrinsics` view to allow `Alice` to buy the asset listed. Select the `buy` method under `gamePowerWallet` module to provide the ListingId of 0 and then submit the transaction.
<p align="center">
  <img alt="step4c" src="/images/step4c.png">
</p>

### STEP 5
Now we can go back to `Network -> Explorer` tab and see under `recent events` that our purchase was successful and the balance was transferred to the seller.

<p align="center">
  <img alt="step5a" src="/images/step5a.png">
</p>

Now we can go back to `Developer -> Chain state` tab and see that our buy order was recorded under `orderHistory`.

<p align="center">
  <img alt="step5b" src="/images/step5b.png">
</p>
