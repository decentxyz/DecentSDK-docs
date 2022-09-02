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

[**stake**](#stake)  
Allows owners of the ERC721 collection to lock up their tokens for staking rewards.

[**claim**](#claim)  
Allows owners of the ERC721 collection to claim and withdraw earned staking rewards.

[**claimForAddress**](#claimforaddress)  
Distributes staking rewards on behalf of a specified account address.

[**unstake**](#unstake)  
Allows owners to claim earned staking rewards and unstake their tokens.

[**earningInfo**](#earninginfo)  
Returns the current staking rewards for the specified account address and tokens.

[**balanceOf**](#balanceof)  
Returns the number of tokens staked by the specified account address.

[**tokensOfOwner**](#tokensofowner)  
Returns the tokens currently staked by the specified account address.

## stake

Allows owners of the ERC721 collection to lock up their tokens for staking rewards.

```
stake([0,1,2]);
```

**tokenIds** (uint256[])  
An array of tokens to lock in the staking vault.

## claim

Allows owners of the ERC721 collection to claim and withdraw earned staking rewards.

```
claim([0,1,2]);
```

**tokenIds** (uint256[])  
An array of tokens to claim staked earning rewards against.


## claimForAddress

Distributes staking rewards on behalf of a specified account address.

```
claimForAddress('0x1234567890123456789012345678901234567890', [0,1,2]);
```

**account** (address)  
The address of the account to claim on behalf of.

**tokenIds** (uint256[])  
An array of tokens to claim staked earning rewards against.


## unstake

Allows owners to claim earned staking rewards and unstake their tokens.

```
unstake([0,1,2]);
```

**tokenIds** (uint256[])  
An array of tokens to unstake and retreive from the staking vault.


## earningInfo

Returns the current staking rewards for the specified account address and tokens.

```
earningInfo('0x1234567890123456789012345678901234567890', [0,1,2]);
```

**account** (address)  
The address of the account to check for earned staking rewards.

**tokenIds** (uint256[])  
An array of tokens to check for earned staking rewards.


## balanceOf

Returns the number of tokens staked by the specified account address.

```
balanceOf('0x1234567890123456789012345678901234567890');
```

**account** (address)  
The address of the account to check for total number of staked tokens.

## tokensOfOwner

Returns the tokens currently staked by the specified account address.

```
tokensOfOwner('0x1234567890123456789012345678901234567890');
```

**account** (address)  
The address of the account to check for total number of staked tokens.
