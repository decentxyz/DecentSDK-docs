---
cover: ../.gitbook/assets/protocol (2).jpg
coverY: 139.57055214723925
---

# NFT Release & Utility Mechanisms

Protocol modules for constructing innovative NFT releases. &#x20;

We refer to Edition, Rentable, and Crescnedo as **Base contracts**, defined as release mechanisms that generate the root unit of exchange in a community. The Vault and Staking modules are **Wrapper contracts,** meaning they can be used to add utility to either a new or exisitng NFT collection. Vault-Backed is a **Hybrid contract**; it leverages both the Edition or Rentable module plus the Vault module to enable both a base and wrapper contract to be deployed in a single transaction.

Base and hybrid contracts support the NFT Royalty Standard ([EIP2981](https://eips.ethereum.org/EIPS/eip-2981)).
