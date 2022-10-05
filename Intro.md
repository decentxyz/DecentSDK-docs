# Welcome to the DecentSDK

#### A developer toolkit for building NFT-based applications via simple JavaScript functions.

Endeavoring to build towards a future where NFTs are not just digital collectibles, but a foundation upon which to build artist-owned applications. The DecentSDK enables you to rapidly deploy and interact with myriad smart contracts to create your own Web3 ecosystem powered by NFTs.  We prioritized ease-of-use and composability so that you can do more with less, leading to accelerating and compounding innovation.

The DecentSDK is currently deployed to Ethereum, Arbitrum, Optimism, zkSync, Polygon and each chain's primary testnet.  We hope that you enjoy using the SDK and encourage developers to contribute new modules via pull requests and post updates and issues in the repository's discussion [forum](https://github.com/decentxyz/DecentSDK/discussions) and [Discord](https://discord.gg/Z4BVZ2dK9z).



## Core Modules

- **[DCNTSDK](DCNTSDK.md)**  
This contract serves as a permanent, immutable, and permissionless foundation upon which to build your application. Its primary function is to allow artist-owned and gas-efficient deployments of the core contracts within the DecentSDK.

#### NFT Release Mechanisms

We refer to Edition, Rentable, and Crescnedo as **Base contracts**, defined as release mechanisms that generate the root unit of exchange in a community.  The Vault and Staking modules are **Wrapper contracts,** meaning they can be used to add utility to either a new or exisitng NFT collection.  Vault-Backed is a **Hybrid contract**; it leverages both the Edition or Rentable module plus the Vault module to enable both a base and wrapper contract to be deployed in a single transaction.

Base and hybrid contracts support the NFT Royalty Standard ([EIP2981](https://eips.ethereum.org/EIPS/eip-2981)).

- **[Edition](Edition.md)**  
NFT drop utilzing the gas-optimized [ERC721A](https://www.azuki.com/erc721a) which allows minting multiple NFTs for nearly the cost of one.

- **[Rentable](Rentable.md)**  
An extension to Edition implementing [ERC4907A](https://chiru-labs.github.io/ERC721A/#/erc4907a) / [EIP4907](https://eips.ethereum.org/EIPS/eip-4907), which allows a token's owner to grant time restricted user rights to another account.

- **[Crescendo](Crescendo.md)**  
NFT drop utilizing a gas-optimzed version of [ERC1155](https://github.com/transmissions11/solmate) with bonding curves to enable dynamic pricing for fan powered price discovery and guarantee liquidity to collectors.

- **[Vault](Vault.md)**  
A time-locked [vault](https://decentxyz.medium.com/introducing-dcnt-vault-wrappers-8f9253240f58) to distribute [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens to owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) or [ERC4907](https://eips.ethereum.org/EIPS/eip-4907) collection at expiry based on their percentage of ownership in the collection.

- **[Staking](Staking.md)**  
A staking vault allowing owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) or [ERC4907](https://eips.ethereum.org/EIPS/eip-4907) collection to stake their NFTs and earn [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens distributed based on the length of the lock up.

- **[VaultBackedNFT](VaultBackedNFT.md)**  
A module to simplify the process of launching a Vault-Backed NFT into a single transaction, allowing you to deploy either an [Edition](Edition.md) or [Rentable](Rentable.md) which will be automatically backed by a shared [Vault](Vault.md).

#### Marketplace Modules

- **[RentalMarket](RentalMarket.md)**  
A rental marketplace allowing instant daily rentals for [Rentable](Rentable.md) or any other NFT which implements the [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) standard.

#### Infrastructure Modules

- **[Registry](Registry.md)**  
The Registry serves as a public on-chain record of all contracts deployed via the DecentSDK and as a point of entry for the Decent Cross-Chain Indexer (please reach out to a Decent team member for access to the indexer).

- **[MetadataRenderer](MetadataRenderer.md)**  
A shared on-chain metadata renderer adhering to the [music metadata standard](https://gist.github.com/bretth18/df8358c840fa94946ec212f753e290dd) which stores and renders metadata as base64 encoded URLs.

- **[IPFS](IPFS.md)**  
Simplifies the process of uploading files and metadata to IPFS, allowing you to generate IPFS URLs for media files such as images, audio, and video, as well as metadata json files.