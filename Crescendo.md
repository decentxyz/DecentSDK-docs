NFT drop utilizing a gas-optimized version of [ERC1155](https://github.com/transmissions11/solmate) with bonding curves to enable dynamic pricing for fan powered price discovery and guarantee liquidity to collectors.

[**Getting Started**](#getting-started)
[**Module Methods**](#module-methods)
[**Smart Contract Methods**](#smart-contract-methods)

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the Crescendo module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```typescript
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

```typescript
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
  saleStart,
  royaltyBPS,
  contractURI,
  metadataURI,
  metadataRendererInit,
  onTxPending,
  onTxReceipt,
  parentIP
);

console.log("Crescendo deployed to: ", myNFT.address);
```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**name** (_string_)
The name of the NFT collection.

**symbol** (_string_)
The symbol of the NFT collection.

**initialPrice** (_BigNumber_)
The initial price (in Wei) to mint a token from the collection.

**step1** (_BigNumber_)
The amount to increment/decrement the per token price pre-hitch.

**step2** (_BigNumber_)
The amount to increment/decrement the per token price post-hitch.

**hitch** (_number_)
Once total supply exceeds the hitch, the amount by which we increment/decrement pricing increases.

**takeRateBPS** (_number_)
The take rate in basis points used to calculate reserve funds for trading liquidity.

**unlockDate** (_number_)
The timestamp at which crescendo will unlock and allow profit distributions.

**saleStart** (_number_)
Unix time general sale starts.

**royaltyBPS** (_number_)
The maximum number of tokens allowed per mint.

**contractURI** (_string_)
The URI for contract level metadata.

**metadataURI** (_string_)
The base URI for the collection metadata.

**metadataRendererInit** (_MetadataRendererInit_)
An object containing metadata to initialize with the on-chain metadata renderer.

**onTxPending** (_Function_) - _optional_
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (_Function_) - _optional_
A callback function executed upon receipt of the deploy transaction.

**parentIP** (_string_) - _optional_
Implementation of [EIP 5553](https://eips.ethereum.org/EIPS/eip-5553) to assign token metadata to the address of another NFT with registered IP.

## getContract

Get an ethers contract instance of a previously deployed Crescendo contract.

```typescript
const myNFT = await crescendo.getContract(sdk, address);
```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**address** (_string_)
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

```typescript
const myNFT = await crescendo.getContract(sdk, address);
const currentPrice = await crescendo.calculateCurvedMintReturn(1, 0);
await crescendo.buy(0, { value: currentPrice });
```

**tokenId** (_uint256_)
The id of the token.

## sell

Sell an NFT at the current burn rate

```typescript
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.sell(0);
```

**tokenId** (_uint256_)
The id of the token. (must be zero)


## totalSupply

Returns the total number of NFTs currently in circulation.

```typescript
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.totalSupply(0);
```

**tokenId** (_uint256_)
The id of the token. (must be zero)

## flipSaleState

Toggles whether to allow minting.

```typescript
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.flipSaleState();
```

## withdraw

Allows the contract owner to withdraw dividends at the specified take rate.

```typescript
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.withdraw();
```

## liquidity

Returns the peak liquidity held by the contract.

```typescript
const myNFT = await crescendo.getContract(sdk, address);
const liquidity = await crescendo.liquidity();
```

## reserveAmt

Returns the peak reserve funds held by the contract.

```typescript
const myNFT = await crescendo.getContract(sdk, address);
const reserve = await crescendo.reserveAmt();
```

## updateUri

Allows the owner to update the URI serving metadata for the NFT collection.

```typescript
const myNFT = await crescendo.getContract(sdk, address);
await crescendo.updateUri('https://nft.example/metadata/{id}.json');
```

**uri** (_uint256_)
The URI serving metadata for the NFT collection.
