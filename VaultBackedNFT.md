# VaultBackedNFT

This module simplifies the process of launching a Vault-Backed NFT into a single transaction, allowing you to deploy either an [Edition](Edition.md) or [Rentable](Rentable.md) which will be automatically backed by a shared [Vault](Vault.md).

## Module Methods

[**create**](#create)  
Creates deployments of minimal proxy clones of the [Vault](Vault.md) as well as [Edition](Edition.md) or [Rentable](Rentable.md) implementation contracts.

## create

Creates deployments of minimal proxy clones of the [Vault](Vault.md) as well as [Edition](Edition.md) or [Rentable](Rentable.md) implementation contracts.

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

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**name** (*string*)  
The name of the NFT collection.

**symbol** (*string*)  
The symbol of the NFT collection.

**maxTokens** (*number*)  
The total number of tokens allowed to be minted from the collection.

**tokenPrice** (*BigNumber*)  
The price (in Wei) to mint a token from the collection.

**maxTokenPurchase** (*number*)  
The maximum number of tokens allowed per mint.

**royaltyBPS** (*number*)  
The maximum number of tokens allowed per mint.

**metadataURI** (*string*)  
The base URI for the collection metadata.

**metadataRendererInit** (*MetadataRendererInit*)  
An object containing metadata to initialize with the on-chain metadata renderer.

**vaultDistributionTokenAddress** (string)  
The address of the ERC20 token that will be distributed by the vault.

**unlockDate** (*number*)  
The timestamp at which the vault will unlock and allow distributions.

**supports4907** (*boolean*)  
A flag indicating whether to deploy a [Rentable](Rentable.md) (true) or [Edition](Edition.md) (false) as the underlying NFT.

**onTxPending** (*Function*) - *optional*  
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (*Function*) - *optional*  
A callback function executed upon receipt of the deploy transaction.
