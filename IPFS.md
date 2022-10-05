# IPFS

This module simplifies the process of uploading files and metadata to IPFS, allowing you to generate IPFS URLs for media files such as images, audio, and video, as well as metadata json files.

If you are utilizing on-chain metadata, the media file URLs can be passed directly as initialization data to the deploy methods of [Edition](Edition.md), [Rentable](Rentable.md), [Crescendo](Crescendo.md), as well as the [bulkUpdate](MetadataRenderer.md#bulkupdate) function on [MetadataRenderer](MetadataRenderer.md).

*Note: This module is a lightweight wrapper utilzing the [nft.storage](https://nft.storage/docs/client/js/) JavaScript client library.

[**Getting Started**](#getting-started)  
[**Module Methods**](#module-methods)  

## Getting Started

To begin we'll import the IPFS module.

```
// Import the IPFS module
import { ipfs } from "@decent.xyz/sdk";
```
## Module Methods

[**createMetadata**](#createmetadata)  
Create an IPFS URL for media files, metadata json files, optionally in a single operation.

## createMetadata

Create an IPFS URL for media files, metadata json files, optionally in a single operation.

```
const ipfs = ipfs.createMetadata(metadata);
```

**metadata** (*any*)  
A media file, or an object containing both media files and metadata.

*Note: For further details refer to the [store](https://nft.storage/docs/client/js/#store---store-erc1155-nft-data) method of the [nft.storage](https://nft.storage/docs/client/js/) JavaScript client library.
