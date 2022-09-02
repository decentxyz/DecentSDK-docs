# Welcome to the DecentSDK

#### A developer toolkit for building artist owned ecosystems powered by NFTs

Endeavoring to build towards a future where NFTs are not just digital collectibles, but a foundation upon which to build artist-owned applications, the DecentSDK enables you to rapidly deploy and interact with myriad smart contracts to create your own Web3 ecosystem powered by NFTs.

### Core Modules

- **[DCNTSDK](DCNTSDK.md)**  
This contract serves as a permanent, immutable, and permissionless foundation upon which to build your application. It's primary function is to allow artist-owned and gas-efficient deployments of the core contracts within the DecentSDK.

- **[DCNT721A](DCNT721A.md)**  
NFT drop utilzing the gas-optimized [ERC721A](https://www.azuki.com/erc721a) which allows minting multiple NFTs for nearly the cost of one.

- **[DCNT4907A](DCNT4907A.md)**  
An extension to DCNT721A implementing [ERC4907A](https://chiru-labs.github.io/ERC721A/#/erc4907a) / [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) allowing owner's to grant time restricted user rights to another account.

- **[DCNTCrescendo](DCNTCrescendo.md)**  
NFT drop utilizing a gas-optimzed version of [ERC1155](https://github.com/transmissions11/solmate) with bonding curves for dynamic pricing to enable fan powered price discovery.

- **[DCNTVault](DCNTVault.md)**  
A time-locked vault to distribute [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens to owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) collection at expiry based on their percentage of ownership in the collection.

- **[DCNTStaking](DCNTStaking.md)**  
A staking vault allowing owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) collection to stake their NFTs and earn [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens distributed based on the length of the lock up.

