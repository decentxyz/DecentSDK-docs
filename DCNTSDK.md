# DCNTSDK

#### A proxy factory enabling low-cost deployments of the core contracts available within the DecentSDK

This contract serves as a permanent, immutable, and permissionless foundation upon which to build your application. It's primary function is to allow artist-owned and gas-efficient deployments of the core contracts within the DecentSDK.

### Mainnet Deployments
SDK Mainnet deployments share a single canonical address across Ethereum, Polygon, Optimism, and Arbitrum.

| Network | Verified Contract Address |
| --- | --- |
| Ethereum | [0x006A667D701088243238A4Af19A2543fd37b1C6A](https://etherscan.io/address/0x006A667D701088243238A4Af19A2543fd37b1C6A#code) |
| Polygon | [0x006A667D701088243238A4Af19A2543fd37b1C6A](https://polygonscan.com/address/0x006A667D701088243238A4Af19A2543fd37b1C6A#code) |
| Optimism | [0x006A667D701088243238A4Af19A2543fd37b1C6A](https://optimistic.etherscan.io/address/0x006A667D701088243238A4Af19A2543fd37b1C6A#code) |
| Arbitrum | [0x006A667D701088243238A4Af19A2543fd37b1C6A](https://arbiscan.io/address/0x006A667D701088243238A4Af19A2543fd37b1C6A/contracts#code) |


### Testnet Deployments

| Network | Verified Contract Address |
| --- | --- |
| Goerli | [0x006A667D701088243238A4Af19A2543fd37b1C6A](https://goerli.etherscan.io/address/0x006A667D701088243238A4Af19A2543fd37b1C6A#code) |
| Polygon Mumbai | [0x4056334cdCa09A54AD0e99c195a8de321406c242](https://mumbai.polygonscan.com/address/0x4056334cdCa09A54AD0e99c195a8de321406c242#code) |
| Optimism Goerli | [0x030605530848177c08201494469aBE89DF197ed6](https://goerli-optimism.etherscan.io/address/0x030605530848177c08201494469aBE89DF197ed6#code) |
| Arbitrum Goerli | [0x006A667D701088243238A4Af19A2543fd37b1C6A](https://goerli-rollup-explorer.arbitrum.io/address/0x006A667D701088243238A4Af19A2543fd37b1C6A/contracts#address-tabs) |


## Smart Contract Methods

[**deployDCNT721A**](Edition.md)  
Deploy a minimal proxy clone of the DCNT721A implementation contract.

[**deployDCNT4907A**](Rentable.md)  
Deploy a minimal proxy clone of the DCNT4907A implementation contract.

[**deployDCNTCrescendo**](Crescendo.md)  
Deploy a minimal proxy clone of the DCNTCrescendo implementation contract.

[**deployDCNTVault**](Vault.md)  
Deploy a minimal proxy clone of the DCNTVault implementation contract.

[**deployDCNTStaking**](Staking.md)  
Deploy a minimal proxy clone of the DCNTStaking implementation contract.