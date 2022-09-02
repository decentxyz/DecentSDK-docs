# DCNT4907A

An extension to [DCNT721A](DCNT721A.md) implementing [ERC4907A](https://chiru-labs.github.io/ERC721A/#/erc4907a) / [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) allowing owner's to grant time restricted user rights to another account.


## deployDCNT4907A

Deploy a minimal proxy clone of the DCNT4907A implementation contract.

```
deployDCNT4907A(
	'My Awesome NFT',
	'FTW',
	100,
	ethers.utils.parseEther('0.1'),
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

[**setUser**](#setuser)  
Set a user and expiration for a token

[**userOf**](#userof)  
Get the current user for a token

[**userExpires**](#userexpires)  
Get the timestamp of expiration for a token


## setUser

Set a user and expiration for a token

```
setUser(
	1,
	'0x1234567890123456789012345678901234567890',
	1735689600
);
```

**tokenId** (uint256)  
The id of the token.

**user** (uint256)  
The new user of the NFT.

**expires** (uint256)  
The timestamp at which the user expires.


## userOf

Get the current user for a token.

```
userOf(1);
```

**tokenId** (uint256)  
The id of the token.


## userExpires

Get the timestamp of expiration for a token.

```
userExpires(1);
```

**tokenId** (uint256)  
The id of the token.
