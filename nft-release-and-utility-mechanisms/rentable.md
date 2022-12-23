# Rentable

An extension to [Edition](edition.md) implementing [ERC4907A](https://chiru-labs.github.io/ERC721A/#/erc4907a) / [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) allowing token owner's to grant time restricted user rights to another account.

[**Getting Started**](rentable.md#getting-started)\
[**Module Methods**](rentable.md#module-methods)\
[**Smart Contract Methods**](rentable.md#smart-contract-methods)

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

[**deploy**](rentable.md#deploy)\
Deploy a minimal proxy clone of the Rentable implementation contract.

[**getContract**](rentable.md#getcontract)\
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

**sdk** (_SDK_)\
An instance of the DecentSDK, configured with a chain and signer.

**name** (_string_)\
The name of the NFT collection.

**symbol** (_string_)\
The symbol of the NFT collection.

**maxTokens** (_number_)\
The total number of tokens allowed to be minted from the collection.

**tokenPrice** (_BigNumber_)\
The price (in Wei) to mint a token from the collection.

**maxTokenPurchase** (_number_)\
The maximum number of tokens allowed per mint.

**royaltyBPS** (_number_)\
The maximum number of tokens allowed per mint.

**metadataURI** (_string_)\
The base URI for the collection metadata.

**metadataRendererInit** (_MetadataRendererInit_)\
An object containing metadata to initialize with the on-chain metadata renderer.

**onTxPending** (_Function_) - _optional_\
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (_Function_) - _optional_\
A callback function executed upon receipt of the deploy transaction.

## getContract

Get an ethers contract instance of a previously deployed Rentable contract.

```
const myNFT = await rentable.getContract(sdk, address);
```

**sdk** (_SDK_)\
An instance of the DecentSDK, configured with a chain and signer.

**address** (_string_)\
The contract address of a previously deployed Rentable contract.

## Smart Contract Methods

[**setUser**](rentable.md#setuser)\
Set a user and expiration for a token

[**userOf**](rentable.md#userof)\
Get the current user for a token

[**userExpires**](rentable.md#userexpires)\
Get the timestamp of expiration for a token

\*All methods available on [Edition](edition.md) are inherited and available on Rentable.

## setUser

Set a user and expiration for a token

```
const myNFT = await rentable.getContract(sdk, address);
await myNFT.setUser(tokenId, user, expires);
```

**tokenId** (_uint256_)\
The id of the token.

**user** (_uint256_)\
The new user of the NFT.

**expires** (_uint256_)\
The timestamp at which the user expires.

## userOf

Get the current user for a token.

```
const myNFT = await rentable.getContract(sdk, address);
await myNFT.userOf(tokenId);
```

**tokenId** (_uint256_)\
The id of the token.

## userExpires

Get the timestamp of expiration for a token.

```
const myNFT = await rentable.getContract(sdk, address);
await myNFT.userExpires(tokenId);
```

**tokenId** (_uint256_)\
The id of the token.
