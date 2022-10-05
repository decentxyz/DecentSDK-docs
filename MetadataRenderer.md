# MetadataRenderer

A shared on-chain metadata renderer adhering to the [music metadata standard](https://gist.github.com/bretth18/df8358c840fa94946ec212f753e290dd) which stores and renders metadata as base64 encoded URLs.

## Module Methods

[**getContract**](#getcontract)  
Get an ethers contract instance of the MetadataRenderer contract.

## getContract

Get an ethers contract instance of the MetadataRenderer contract.

```
const renderer = await metadataRenderer.getContract(sdk);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

## Smart Contract Methods

[**bulkUpdate**](#bulkupdate)  
Initialized or updates the edition data for a specific target contract.

[**tokenURITarget**](#tokenuritarget)  
Returns the base64 encoded metadata for a specific target contract.

## bulkUpdate

Returns the balance of the ERC20 token held by the vault.

```
const renderer = await metadataRenderer.getContract(sdk);
await renderer.bulkUpdate(
  target,
  songMetadata,
  projectMetadata,
  tags,
  credits
);
```

**target** (*address*)  
The address of the NFT collection for which to initialize or update metadata.

**_songMetadata** (*SongMetadata*)  
A struct containing the song metadata.

**_projectMetadata** (*ProjectMetadata*)  
A struct containing the project metadata.

**_tags** (*string[]*)  
An array of tags.

**_credits** (*Credit[]*)  
An array of structs containing credits.

## tokenURITarget

Returns the base64 encoded metadata for a specific target contract.

```
const renderer = await metadataRenderer.getContract(sdk);
const tokenId = 0;
const target = '0x1234567890123456789012345678901234567890';
const metadata = await renderer.tokenURITarget(tokenId, target);
```

**tokenId** (*uint256*)  
The id of the token to retrieve metadata for.

**target** (*address*)  
The address of the NFT collection to retrieve metadata for.
