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

[**buy**](#buy)  
Mint an NFT at the current mint rate

[**sell**](#sell)  
Sell an NFT at the current burn rate

[**totalSupply**](#sell)  
Returns the total number of NFTs currently in circulation.

[**flipSaleState**](#flipsalestate)  
Toggles whether to allow minting.

[**withdrawFund**](#withdrawfund)  
Allows the owner to withdraw the contract balance.

[**withdrawDividend**](#withdrawdividend)  
Allows the account authorized for payouts to withdraw dividends at the specified take rate.

[**liquidity**](#liquidity)  
Returns the peak liquidity held by the contract.

[**reserveAmt**](#reserveamt)  
Returns the peak reserve funds held by the contract.

[**updateUri**](#updateuri)  
Allows the owner to update the URI serving metadata for the NFT collection.

## buy  

Mint an NFT at the current mint rate

```
buy(0);
```

**tokenId** (uint256)  
The id of the token.

## sell  

Sell an NFT at the current burn rate

```
sell(0);
```

**tokenId** (uint256)  
The id of the token. (must be zero)  


## totalSupply  

Returns the total number of NFTs currently in circulation.

```
totalSupply(0);
```

**tokenId** (uint256)  
The id of the token. (must be zero)  

## flipSaleState  

Toggles whether to allow minting.

```
flipSaleState();
```

## withdrawFund  

Allows the owner to withdraw the contract balance.

```
withdrawFund();
```

## withdrawDividend  

Allows the account authorized for payouts to withdraw dividends at the specified take rate.

```
withdrawDividend();
```

## liquidity  

Returns the peak liquidity held by the contract.

```
liquidity();
```

## reserveAmt  

Returns the peak reserve funds held by the contract.

```
reserveAmt();
```

## updateUri  

Allows the owner to update the URI serving metadata for the NFT collection.

```
updateUri('https://nft.example/metadata/{id}.json');
```

**uri** (uint256)  
The URI serving metadata for the NFT collection.
