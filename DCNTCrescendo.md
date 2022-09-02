# DCNTCrescendo

NFT drop utilizing a gas-optimzed version of [ERC1155](https://github.com/transmissions11/solmate) with bonding curves for dynamic pricing to enable fan powered price discovery.

## deployDCNTCrescendo

Deploy a minimal proxy clone of the DCNT4907A implementation contract.

```
deployDCNTCrescendo(
	'My Awesome NFT',
	'FTW',
	'https://nft.example/{id}.json',
	ethers.utils.parseEther('0.05'),
	ethers.utils.parseEther('0.005'),
	ethers.utils.parseEther('0.05'),
	20,
	1500,
	10000,
	'0x1234567890123456789012345678901234567890'
)
```

**_name** (string)  
The name of the NFT collection.

**_symbol** (string)  
The symbol of the NFT collection.

**_uri** (string)  
The base uri for the NFT collection metadata.

**_initialPrice** (uint256)  
The initial price (in Wei) to mint a token from the collection.

**_step1** (uint256)  
The amount to increment/decrement the per token price pre-hitch.

**_step2** (uint256)  
The amount to increment/decrement the per token price post-hitch.

**_hitch** (uint256)  
Once total supply exceeds the hitch the amount by which we increment/decrement pricing increases.

**_trNum** (uint256)  
The take rate numerator used for calculating take rate basis points.

**_trDenom** (uint256)  
The take rate denominator used for calculating take rate basis points.

**_payouts** (uint256)  
The account address authorized to withdraw take rate payouts.

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
