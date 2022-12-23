# VaultBackedNFT

This module simplifies the process of launching a Vault-Backed NFT into a single transaction, allowing you to deploy either an [Edition](edition.md) or [Rentable](rentable.md) which will be automatically backed by a shared [Vault](vault.md).

[**Getting Started**](vaultbackednft.md#getting-started)\
[**Module Methods**](vaultbackednft.md#module-methods)

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and VaultBackedNFT module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```
// Import SDK, chain configurations, and the VaultBackedNFT module
import { DecentSDK, chain, vaultBackedNFT } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**create**](vaultbackednft.md#create)\
Creates deployments of minimal proxy clones of the [Vault](vault.md) as well as [Edition](edition.md) or [Rentable](rentable.md) implementation contracts.

## create

Creates deployments of minimal proxy clones of the [Vault](vault.md) as well as [Edition](edition.md) or [Rentable](rentable.md) implementation contracts.

```
const [myNFT, myVault] = await edition.deploy(
  sdk,
  name,
  symbol,
  maxTokens,
  tokenPrice,
  maxTokenPurchase,
  royaltyBPS,
  metadataURI,
  metadataRendererInit,
  vaultDistributionTokenAddress,
  unlockDate,
  supports4907,
  onTxPending,
  onTxReceipt
);

console.log("NFT deployed to: ", myNFT.address);
console.log("Vault deployed to: ", myVault.address);
```

**sdk** (_SDK_)\
An instance of the DecentSDK, configured with a chain and signer.

**name** (_string_)\
The name of the NFT collection.

**symbol** (_string_)\
The symbol of the NFT collection.

**maxTokens** (_number_)\
The total number of tokens allowed to be minted from the collection.

**tokenPrice** (_BigNumber_)\
The price (in Wei) to mint a token from the collection.

**maxTokenPurchase** (_number_)\
The maximum number of tokens allowed per mint.

**royaltyBPS** (_number_)\
The maximum number of tokens allowed per mint.

**metadataURI** (_string_)\
The base URI for the collection metadata.

**metadataRendererInit** (_MetadataRendererInit_)\
An object containing metadata to initialize with the on-chain metadata renderer.

**vaultDistributionTokenAddress** (string)\
The address of the ERC20 token that will be distributed by the vault.

**unlockDate** (_number_)\
The timestamp at which the vault will unlock and allow distributions.

**supports4907** (_boolean_)\
A flag indicating whether to deploy a [Rentable](rentable.md) (true) or [Edition](edition.md) (false) as the underlying NFT.

**onTxPending** (_Function_) - _optional_\
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (_Function_) - _optional_\
A callback function executed upon receipt of the deploy transaction.
