# DCNT721A

NFT drop utilzing the gas-optimized [ERC721A](https://www.azuki.com/erc721a) which allows minting multiple NFTs for nearly the cost of one.


## deployDCNT721A

Deploy a minimal proxy clone of the DCNT721A implementation contract.

```
deployDCNT721A(
	'My Awesome NFT',
	'FTW',
	100,
	10000000000000000,
	2
)
```

**_name** (string)  
The name of the NFT collection.

**_symbol** (string)  
The symbol of the NFT collection.

**_maxTokens** (uint256)  
The total number of tokens allowed to be minted from the collection.

**_tokenPrice** (uint256)  
The price (in Wei) to mint a token from the collection.

**_maxTokenPurchase** (uint256)  
The maximum number of tokens allowed per mint.

## Smart Contract Methods

[**mint**](#mint)  
Mints the specified number of tokens to msg.sender.

[**flipSaleState**](#flipsalestate)  
Toggles whether to allow minting.

[**withdraw**](#withdraw)  
Allows the owner to withdraw the contract balance.

[**setBaseURI**](#setbaseuri)  
Allows the owner to update the base URI for token metadata.

## mint

Mints the specified number of tokens to msg.sender

```
mint(1);
```

**numberOfTokens** (uint256)  
The name of the NFT collection.


## flipSaleState

Toggles whether to allow minting.

```
flipSaleState();
```


## withdraw

Allows the owner to withdraw the contract balance.

```
withdraw();
```


## setBaseURI

Allows the owner to update the base URI for token metadata.

```
setBaseURI('https://nft.example/metadata/');
```

**uri** (uint256)  
The base URI serving metadata for the NFT collection.
