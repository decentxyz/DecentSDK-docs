---
title: "Rental Market"
excerpt: ""
---

A rental marketplace allowing instant daily rentals for [Rentable](Rentable.md) or any other NFT which implements the [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) standard.

Token owners can list their NFT tokens for rent, specify the desired fees and terms, and the marketplace takes care of designating users as well as collecting and distributing rental fees to token owners.

In addition, RentalMarket supports [EIP2981](https://eips.ethereum.org/EIPS/eip-2981) and distributes a royalty fee on all rentals back to the creator.

[**Getting Started**](#getting-started)  
[**Module Methods**](#module-methods)  
[**Smart Contract Methods**](#smart-contract-methods)  

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the RentalMarket module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```
// Import SDK, chain configurations, and the RentalMarket module
import { DecentSDK, chain, rentalMarket } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**getContract**](#getcontract)  
Get an ethers contract instance of the RentalMarket contract.

## getContract

Get an ethers contract instance of the RentalMarket contract.

```
const market = await rentalMarket.getContract(sdk);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

## Smart Contract Methods

[**setRentable**](#setrentable)  
Set the listing status, fees, and terms for a specified token.

[**getRentable**](#getrentable)  
Get the listing status, fees, and terms for a specified token.

[**toggleListed**](#togglelisted)  
Toggle the listing status for a specified token.

[**rent**](#rent)  
Rent a listed token for a specified number of days.


## setRentable

Set the listing status, fees, and terms for a specified token.

```
const market = await rentalMarket.getContract(sdk);

const nft = '0x1234567890123456789012345678901234567890';
const tokenId = 0;
const isListed = true;
const pricePerDay = ethers.utils.parseEther('0.1');
const minDays = 1;
const maxDays = 7;

const myNFT = await rentable.getContract(sdk, nft);
await myNFT.approve(market.address, tokenId);

await market.setRentable(
  nft,
  tokenId,
  isListed,
  pricePerDay,
  minDays,
  maxDays
);
```

**_nft** (*address*)  
The address of an NFT which implements the [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) standard.

**_tokenId** (*uint256*)  
The id of the token.

**_isListed** (*bool*)  
A flag indicating whether the token is currently listed for rentals.

**_pricePerDay** (*uint256*)  
The price (in Wei) per day to rent the token.

**_minDays** (*uint16*)  
The minimum acceptable number of days which a renter may specify for rental duration.

**_maxDays** (*uint16*)  
The maxium acceptable number of days which a renter may specify for rental duration.

## getRentable

Get the listing status, fees, and terms for a specified token.

```
const market = await rentalMarket.getContract(sdk);
const nft = '0x1234567890123456789012345678901234567890';
const tokenId = 0;
const listing = await market.getRentable(nft, tokenId);
```

**_nft** (*address*)  
The address of the NFT.

**_tokenId** (*uint256*)  
The id of the token.

## toggleListed

Toggle the listing status for a specified token.

```
const market = await rentalMarket.getContract(sdk);
await market.toggleListed(nft, tokenId);
```

## rent

Rent a listed token for a specified number of days.

```
const market = await rentalMarket.getContract(sdk);
const nft = '0x1234567890123456789012345678901234567890';
const tokenId = 0;
const days = 3;
const listing = await market.getRentable(nft, tokenId);
const rentalFee = listing.pricePerDay.mul(days);

await market.rent(
  nft,
  tokenId,
  days,
  { value: rentalFee }
);
```

**_nft** (*address*)  
The address of the NFT.

**_tokenId** (*uint256*)  
The id of the token.

**_days** (*uint16*)  
The number of days to rent the specified token.
