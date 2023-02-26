A staking vault allowing owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) or [ERC4907](https://eips.ethereum.org/EIPS/eip-4907) collection to stake their NFTs and earn [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens distributed based on the length of the lock up.

[**Getting Started**](#getting-started)
[**Module Methods**](#module-methods)
[**Smart Contract Methods**](#smart-contract-methods)

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the Staking module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```typescript
// Import SDK, chain configurations, and the Staking module
import { DecentSDK, chain, staking } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**deploy**](#deploy)
Deploy a minimal proxy clone of the Staking implementation contract.

[**getContract**](#getcontract)
Get an ethers contract instance of a previously deployed Staking contract.

## deploy

Deploy a minimal proxy clone of the Staking implementation contract.

```typescript
const myStaking = await staking.deploy(
  sdk,
  nft,
  token,
  vaultDuration,
  totalSupply,
  onTxPending,
  onTxReceipt
);

console.log("Staking deployed to: ", myStaking.address);
```
**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**nft** (_string_)
The address of the ERC721 that will be locked for staking rewards.

**token** (_string_)
The address of the ERC20 token that will be earned by staking ERC721 tokens.

**vaultDuration** (_number_)
The duration in days over which staking rewards may be earned.

**totalSupply** (_number_)
The total supply of the ERC721 collection that may earn staking rewards.

**onTxPending** (_Function_) - _optional_
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (_Function_) - _optional_
A callback function executed upon receipt of the deploy transaction.

## getContract

Get an ethers contract instance of a previously deployed Staking contract.

```typescript
const myStaking = await staking.getContract(sdk, address);
```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**address** (_string_)
The contract address of a previously deployed Rentable contract.

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

```typescript
const myStaking = await staking.getContract(sdk, address);
const tokenIds = [0,1,2];
await myStaking.stake(tokenIds);
```

**tokenIds** (_uint256[]_)
An array of tokens to lock in the staking vault.

## claim

Allows owners of the ERC721 collection to claim and withdraw earned staking rewards.

```typescript
const myStaking = await staking.getContract(sdk, address);
const tokenIds = [0,1,2];
await myStaking.claim(tokenIds);
```

**tokenIds** (_uint256[]_)
An array of tokens to claim staked earning rewards against.


## claimForAddress

Distributes staking rewards on behalf of a specified account address.

```
const myStaking = await staking.getContract(sdk, address);
const account = '0x1234567890123456789012345678901234567890';
const tokenIds = [0,1,2];
await myStaking.claimForAddress(account, tokenIds);
```

**account** (_address_)
The address of the account to claim on behalf of.

**tokenIds** (_uint256[]_)
An array of tokens to claim staked earning rewards against.


## unstake

Allows owners to claim earned staking rewards and unstake their tokens.

```typescript
const myStaking = await staking.getContract(sdk, address);
const tokenIds = [0,1,2];
await myStaking.unstake(tokenIds);
```

**tokenIds** (_uint256[]_)
An array of tokens to unstake and retreive from the staking vault.


## earningInfo

Returns the current staking rewards for the specified account address and tokens.

```typescript
const myStaking = await staking.getContract(sdk, address);
const account = '0x1234567890123456789012345678901234567890';
const tokenIds = [0,1,2];
await myStaking.earningInfo(account, tokenIds);
```

**account** (_address_)
The address of the account to check for earned staking rewards.

**tokenIds** (_uint256[]_)
An array of tokens to check for earned staking rewards.


## balanceOf

Returns the number of tokens staked by the specified account address.

```typescript
const myStaking = await staking.getContract(sdk, address);
const account = '0x1234567890123456789012345678901234567890';
await myStaking.balanceOf(account);
```

**account** (_address_)
The address of the account to check for total number of staked tokens.

## tokensOfOwner

Returns the tokens currently staked by the specified account address.

```typescript
const myStaking = await staking.getContract(sdk, address);
const account = '0x1234567890123456789012345678901234567890';
await myStaking.tokensOfOwner(account);
```

**account** (_address_)
The address of the account to check for total number of staked tokens.
