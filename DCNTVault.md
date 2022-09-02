# DCNTVault

A time-locked vault to distribute [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens to owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) collection at expiry based on their percentage of ownership in the collection.

## deployDCNTVault

Deploy a minimal proxy clone of the DCNTVault ipmlementation contract.

```
deployDCNTVault(
	'0x1234567890123456789012345678901234567890',
	'0x0987654321098765432109876543210987654321',
	100,
	1735689600
);

```

**_vaultDistributionTokenAddress** (address)  
The address of the ERC20 token that will be distributed by the vault.

**_nftVaultKeyAddress** (address)  
The address of the ERC20 token that will be distributed by the vault.

**_nftTotalSupply** (uint256)  
The total supply of the ERC721 collection that is wrapped by the vault.

**_unlockDate** (uint256)  
The timestamp at which the vault will unlock and allow distributions.

## Smart Contract Methods

[**exampleMethod**](#examplemethod)  
Description of an example method

## exampleMethod

Description of an example method.

```
coolMethod('coolParameter');
```

**coolParameter** (uint256)  
Description of an example parameter.
