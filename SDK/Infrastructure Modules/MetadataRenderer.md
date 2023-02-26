A shared on-chain metadata renderer adhering to the [music metadata standard](https://gist.github.com/bretth18/df8358c840fa94946ec212f753e290dd) which stores and renders metadata as base64 encoded URLs.

[**Getting Started**](#getting-started)
[**Module Methods**](#module-methods)
[**Smart Contract Methods**](#smart-contract-methods)

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the MetadataRenderer module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```typescript
// Import SDK, chain configurations, and the MetadataRenderer module
import { DecentSDK, chain, metadataRenderer } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**getContract**](#getcontract)
Get an ethers contract instance of the MetadataRenderer contract.

## getContract

Get an ethers contract instance of the MetadataRenderer contract.

```typescript
const renderer = await metadataRenderer.getContract(sdk);
```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

## Smart Contract Methods

[**bulkUpdate**](#bulkupdate)
Initialized or updates the edition data for a specific target contract.

[**tokenURITarget**](#tokenuritarget)
Returns the base64 encoded metadata for a specific target contract.

## bulkUpdate

Returns the balance of the ERC20 token held by the vault.

```typescript
const renderer = await metadataRenderer.getContract(sdk);
await renderer.bulkUpdate(
  target,
  songMetadata,
  projectMetadata,
  tags,
  credits
);
```

**target** (_address_)
The address of the NFT collection for which to initialize or update metadata.

**\_songMetadata** (_SongMetadata_)
A struct containing the song metadata.

**\_projectMetadata** (_ProjectMetadata_)
A struct containing the project metadata.

**\_tags** (_string[]_)
An array of tags.

**\_credits** (_Credit[]_)
An array of structs containing credits.

## tokenURITarget

Returns the base64 encoded metadata for a specific target contract.

```typescript
const renderer = await metadataRenderer.getContract(sdk);
const tokenId = 0;
const target = '0x1234567890123456789012345678901234567890';
const metadata = await renderer.tokenURITarget(tokenId, target);
```

**tokenId** (_uint256_)
The id of the token to retrieve metadata for.

**target** (_address_)
The address of the NFT collection to retrieve metadata for.