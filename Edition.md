# Edition

NFT drop utilzing the gas-optimized [ERC721A](https://www.azuki.com/erc721a) which allows minting multiple NFTs for nearly the cost of one.

[**Getting Started**](#getting-started)  
[**Module Methods**](#module-methods)  
[**Smart Contract Methods**](#smart-contract-methods)  

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the Edition module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```
// Import SDK, chain configurations, and the Edition module
import { DecentSDK, chain, edition } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**deploy**](#deploy)  
Deploy a minimal proxy clone of the Edition implementation contract.

[**getContract**](#getcontract)  
Get an ethers contract instance of a previously deployed Edition contract.

## deploy

Deploy a minimal proxy clone of the Edition implementation contract.

```
const myNFT = await edition.deploy(
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

console.log("Edition deployed to: ", myNFT.address);
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

Get an ethers contract instance of a previously deployed Edition contract.

```
const myNFT = await edition.getContract(sdk, address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**address** (*string*)  
The contract address of a previously deployed Edition contract.

## Smart Contract Methods

[**mint**](#mint)  
Mints the specified number of tokens to msg.sender.

[**flipSaleState**](#flipsalestate)  
Toggles whether to allow minting.

[**withdraw**](#withdraw)  
Allows the owner to withdraw the contract balance.

[**setBaseURI**](#setbaseuri)  
Allows the owner to update the base URI for token metadata. 

## mint

Mints the specified number of tokens to msg.sender

```
const myNFT = await edition.getContract(sdk, address);
await myNFT.mint(1, { value: ethers.utils.parseEther('0.1') });
```

**numberOfTokens** (*uint256*)  
The name of the NFT collection.


## flipSaleState

Toggles whether to allow minting.

```
const myNFT = await edition.getContract(sdk, address);
await myNFT.flipSaleState();
```


## withdraw

Allows the owner to withdraw the contract balance.

```
const myNFT = await edition.getContract(sdk, address);
await myNFT.withdraw();
```

## setBaseURI

Allows the owner to update the base URI for token metadata.

```
const myNFT = await edition.getContract(sdk, address);
await myNFT.setBaseURI('https://nft.example/metadata/');
```

**uri** (*uint256*)  
The base URI serving metadata for the NFT collection.
