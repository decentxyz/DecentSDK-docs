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

[**vaultBalance**](#vaultbalance)  
Returns the balance of the ERC20 token held by the vault.

[**totalReleased**](#totalreleased)  
Returns the total amount of the ERC20 which has been claimed and released.

[**claimMany**](#claimmany)  
Allows owners of the ERC721 collection to claim their share of the ERC20 funding the vault for multiple tokens.

[**claim**](#claim)  
Allows owners of the ERC721 collection to claim their share of the ERC20 funding the vault for an individual token.

[**drain**](#drain)  
A failsafe allowing the vault owner to withdraw ERC20 tokens sent to the vault

[**drainEth**](#draineth)  
A failsafe allowing the vault owner to withdraw ETH sent to the vault

## vaultBalance

Returns the balance of the ERC20 token held by the vault.

```
vaultBalance();
```

## totalReleased

Returns the total amount of the ERC20 which has been claimed and released.

```
totalReleased();
```

## claimMany

Allows owners of the ERC721 collection to claim their share of the ERC20 funding the vault for multiple tokens.

```
claimMany('0x1234567890123456789012345678901234567890', [0,1,2]);
```

**to** (address)  
The address of the owner in the ERC721 collection to which ERC20 tokens will be sent.

**tokenIds** (uint256[])  
An array of tokens held by the owner against which to claim their share of the ERC20 tokens funding by the vault.

## claim

Allows owners of the ERC721 collection to claim their share of the ERC20 funding the vault for an individual token.

```
claim('0x1234567890123456789012345678901234567890', 0);
```

**to** (address)  
The address of the owner in the ERC721 collection to which ERC20 tokens will be sent.

**tokenId** (uint256)  
The name of the NFT collection.

## drain

A failsafe allowing the vault owner to withdraw ERC20 tokens sent to the vault

```
drain('0x1234567890123456789012345678901234567890');
```

**token** (IERC20)  
The address of the ERC20 token to withdraw from the vault.


## drainEth

A failsafe allowing the vault owner to withdraw ETH sent to the vault

```
drainEth();
```