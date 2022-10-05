# Welcome to the DecentSDK

#### A developer toolkit for building multi-contrct applications via simple JavaScript functions.

Endeavoring to build towards a future where NFTs are not just digital collectibles, but a foundation upon which to build artist-owned applications. The Decent Protocol enables you to rapidly deploy and interact with myriad smart contracts to create your own Web3 ecosystem powered by NFTs.

### Core Modules

- **[DCNTSDK](DCNTSDK.md)**  
This contract serves as a permanent, immutable, and permissionless foundation upon which to build your application. It's primary function is to allow artist-owned and gas-efficient deployments of the core contracts within the DecentSDK.

- **[Edition](Edition.md)**  
NFT drop utilzing the gas-optimized [ERC721A](https://www.azuki.com/erc721a) which allows minting multiple NFTs for nearly the cost of one.

- **[Rentable](Rentable.md)**  
An extension to Edition implementing [ERC4907A](https://chiru-labs.github.io/ERC721A/#/erc4907a) / [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) allowing token owner's to grant time restricted user rights to another account.

- **[Crescendo](Crescendo.md)**  
NFT drop utilizing a gas-optimzed version of [ERC1155](https://github.com/transmissions11/solmate) with bonding curves for dynamic pricing to enable fan powered price discovery.

- **[Vault](Vault.md)**  
A time-locked vault to distribute [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens to owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) collection at expiry based on their percentage of ownership in the collection.

- **[Staking](Staking.md)**  
A staking vault allowing owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) collection to stake their NFTs and earn [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens distributed based on the length of the lock up.

- **[MetadataRenderer](MetadataRenderer.md)**  
A shared on-chain metadata renderer adhering to the [music metadata standard](https://gist.github.com/bretth18/df8358c840fa94946ec212f753e290dd) which stores and renders metadata as base64 encoded URLs.

- **[IPFS](IPFS.md)**  
Simplifies the process of uploading files and metadata to IPFS, allowing you to generate IPFS URLs for media files such as images, audio, and video, as well as metadata json files.

- **[Registry](Registry.md)**  
The Registry serves as a public on-chain record of all contracts deployed via the DecentSDK and as a point of entry for the Decent Cross-Chain Indexer.

- **[VaultBackedNFT](VaultBackedNFT.md)**  
A module to simplify the process of launching a Vault-Backed NFT into a single transaction, allowing you to deploy either an [Edition](Edition.md) or [Rentable](Rentable.md) which will be automatically backed by a shared [Vault](Vault.md).

- **[RentalMarket](RentalMarket.md)**  
A rental marketplace allowing instant daily rentals for [Rentable](Rentable.md) or any other NFT which implements the [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) standard.
