# Crescendo

NFT drop utilizing a gas-optimzed version of [ERC1155](https://github.com/transmissions11/solmate) with bonding curves to enable dynamic pricing for fan powered price discovery and guarantee liquidity to collectors.

[**Getting Started**](#getting-started)  
[**Module Methods**](#module-methods)  
[**Smart Contract Methods**](#smart-contract-methods)  

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the Crescendo module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```
// Import SDK, chain configurations, and the Crescendo module
import { DecentSDK, chain, crescendo } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**deploy**](#deploy)  
Deploy a minimal proxy clone of the Crescendo implementation contract.

[**getContract**](#getcontract)  
Get an ethers contract instance of a previously deployed Crescendo contract.

## deploy

Deploy a minimal proxy clone of the Crescendo implementation contract.

```
const myNFT = await crescendo.deploy(
  sdk,
  name,
  symbol,
  initialPrice,
  step1,
  step2,
  hitch,
  takeRateBPS,
  unlockDate,
  royaltyBPS,
  metadataURI,
  metadataRendererInit,
  onTxPending,
  onTxReceipt
);

console.log("Crescendo deployed to: ", myNFT.address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**name** (*string*)  
The name of the NFT collection.

**symbol** (*string*)  
The symbol of the NFT collection.

**initialPrice** (*BigNumber*)  
The initial price (in Wei) to mint a token from the collection.

**step1** (*BigNumber*)  
The amount to increment/decrement the per token price pre-hitch.

**step2** (*BigNumber*)  
The amount to increment/decrement the per token price post-hitch.

**hitch** (*number*)  
Once total supply exceeds the hitch, the amount by which we increment/decrement pricing increases.

**takeRateBPS** (*number*)  
The take rate in basis points used to calculate reserve funds for trading liquidity.

**unlockDate** (*number*)  
The timestamp at which crescendo will unlock and allow profit distributions.

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

Get an ethers contract instance of a previously deployed Crescendo contract.

```
const myNFT = await crescendo.getContract(sdk, address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**address** (*string*)  
The contract address of a previously deployed Crescendo contract.

## Smart Contract Methods

[**buy**](#buy)  
Mint an NFT at the current mint rate

[**sell**](#sell)  
Sell an NFT at the current burn rate

[**totalSupply**](#sell)  
Returns the total number of NFTs currently in circulation.

[**flipSaleState**](#flipsalestate)  
Toggles whether to allow minting.

[**withdraw**](#withdraw)  
Allows the account authorized for payouts to withdraw dividends at the specified take rate.

[**liquidity**](#liquidity)  
Returns the peak liquidity held by the contract.

[**reserveAmt**](#reserveamt)  
Returns the peak reserve funds held by the contract.

[**updateUri**](#updateuri)  
Allows the owner to update the URI serving metadata for the NFT collection.

## buy  

Mint an NFT at the current mint rate

```
const myNFT = await crescendo.getContract(sdk, address);
const currentPrice = await crescendo.calculateCurvedMintReturn(1, 0);
await crescendo.buy(0, { value: currentPrice });
```

**tokenId** (*uint256*)  
The id of the token.

## sell  

Sell an NFT at the current burn rate

```
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.sell(0);
```

**tokenId** (*uint256*)  
The id of the token. (must be zero)  


## totalSupply  

Returns the total number of NFTs currently in circulation.

```
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.totalSupply(0);
```

**tokenId** (*uint256*)  
The id of the token. (must be zero)  

## flipSaleState  

Toggles whether to allow minting.

```
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.flipSaleState();
```

## withdraw  

Allows the contract owner to withdraw dividends at the specified take rate.

```
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.withdraw();
```

## liquidity  

Returns the peak liquidity held by the contract.

```
const myNFT = await crescendo.getContract(sdk, address);
const liquidity = await crescendo.liquidity();
```

## reserveAmt  

Returns the peak reserve funds held by the contract.

```
const myNFT = await crescendo.getContract(sdk, address);
const reserve = await crescendo.reserveAmt();
```

## updateUri  

Allows the owner to update the URI serving metadata for the NFT collection.

```
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.updateUri('https://nft.example/metadata/{id}.json');
```

**uri** (*uint256*)  
The URI serving metadata for the NFT collection.
