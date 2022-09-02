# DCNTStaking

A staking vault allowing owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) collection to stake their NFTs and earn [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens distributed based on the length of the lock up.

## deployDCNTStaking

Deploy a minimal proxy clone of the DCNTStaking implementation contract.

```
deployDCNTStaking(
	'0x1234567890123456789012345678901234567890',
	'0x0987654321098765432109876543210987654321',
	365,
	100
);
```

**_nft** (address)  
The address of the ERC721 that will be locked for staking rewards.

**_token** (address)  
The address of the ERC20 token that will be earned by staking ERC721 tokens.

**_vaultDuration** (uint256)  
The duration in days over which staking rewards may be earned.

**_totalSupply** (uint256)  
The total supply of the ERC721 collection that may earn staking rewards.

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
