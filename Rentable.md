# Rentable

An extension to [Edition](Edition.md) implementing [ERC4907A](https://chiru-labs.github.io/ERC721A/#/erc4907a) / [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) allowing token owner's to grant time restricted user rights to another account.

[**Getting Started**](#getting-started)  
[**Module Methods**](#module-methods)  
[**Smart Contract Methods**](#smart-contract-methods)  

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the Rentable module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```
// Import SDK, chain configurations, and the Rentable module
import { DecentSDK, chain, rentable } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**deploy**](#deploy)  
Deploy a minimal proxy clone of the Rentable implementation contract.

[**getContract**](#getcontract)  
Get an ethers contract instance of a previously deployed Rentable contract.

## deploy

Deploy a minimal proxy clone of the Rentable implementation contract.

```
const myNFT = await rentable.deploy(
  sdk,
  name,
  symbol,
  maxTokens,
  tokenPrice,
  maxTokenPurchase,
  royaltyBPS,
  metadataURI,
  metadataRendererInit,
  onTxPending,
  onTxReceipt
);

console.log("Rentable deployed to: ", myNFT.address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**name** (*string*)  
The name of the NFT collection.

**symbol** (*string*)  
The symbol of the NFT collection.

**maxTokens** (*number*)  
The total number of tokens allowed to be minted from the collection.

**tokenPrice** (*BigNumber*)  
The price (in Wei) to mint a token from the collection.

**maxTokenPurchase** (*number*)  
The maximum number of tokens allowed per mint.

**royaltyBPS** (*number*)  
The maximum number of tokens allowed per mint.

**metadataURI** (*string*)  
The base URI for the collection metadata.

**metadataRendererInit** (*MetadataRendererInit*)  
An object containing metadata to initialize with the on-chain metadata renderer.

**onTxPending** (*Function*) - *optional*  
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (*Function*) - *optional*  
A callback function executed upon receipt of the deploy transaction.

## getContract

Get an ethers contract instance of a previously deployed Rentable contract.

```
const myNFT = await rentable.getContract(sdk, address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**address** (*string*)  
The contract address of a previously deployed Rentable contract.

## Smart Contract Methods

[**setUser**](#setuser)  
Set a user and expiration for a token

[**userOf**](#userof)  
Get the current user for a token

[**userExpires**](#userexpires)  
Get the timestamp of expiration for a token

*All methods available on [Edition](Edition.md) are inherited and available on Rentable.

## setUser

Set a user and expiration for a token

```
const myNFT = await rentable.getContract(sdk, address);
await myNFT.setUser(tokenId, user, expires);
```

**tokenId** (*uint256*)  
The id of the token.

**user** (*uint256*)  
The new user of the NFT.

**expires** (*uint256*)  
The timestamp at which the user expires.


## userOf

Get the current user for a token.

```
const myNFT = await rentable.getContract(sdk, address);
await myNFT.userOf(tokenId);
```

**tokenId** (*uint256*)  
The id of the token.


## userExpires

Get the timestamp of expiration for a token.

```
const myNFT = await rentable.getContract(sdk, address);
await myNFT.userExpires(tokenId);
```

**tokenId** (*uint256*)  
The id of the token.
