A time-locked [vault](https://decentxyz.medium.com/introducing-dcnt-vault-wrappers-8f9253240f58) to distribute [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens to owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) or [ERC4907](https://eips.ethereum.org/EIPS/eip-4907) collection at expiry based on their percentage of ownership in the collection.

[**Getting Started**](#getting-started)
[**Module Methods**](#module-methods)
[**Smart Contract Methods**](#smart-contract-methods)

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the Vault module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```typescript
// Import SDK, chain configurations, and the Vault module
import { DecentSDK, chain, vault } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**deploy**](#deploy)
Deploy a minimal proxy clone of the Vault implementation contract.

[**getContract**](#getcontract)
Get an ethers contract instance of a previously deployed Vault contract.

## deploy

Deploy a minimal proxy clone of the Vault implementation contract.

```typescript
const myVault = await vault.deploy(
  sdk,
  vaultDistributionTokenAddress,
  nftVaultKeyAddress,
  nftTotalSupply,
  unlockDate,
  onTxPending,
  onTxReceipt
);

console.log("Vault deployed to: ", myVault.address);

```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**vaultDistributionTokenAddress** (string)
The address of the ERC20 token that will be distributed by the vault.

**nftVaultKeyAddress** (_string_)
The address of the ERC20 token that will be distributed by the vault.

**nftTotalSupply** (_number_)
The total supply of the ERC721 collection that is wrapped by the vault.

**unlockDate** (_number_)
The timestamp at which the vault will unlock and allow distributions.

**onTxPending** (_Function_) - _optional_
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (_Function_) - _optional_
A callback function executed upon receipt of the deploy transaction.

## getContract

Get an ethers contract instance of a previously deployed Vault contract.

```typescript
const myVault = await vault.getContract(sdk, address);
```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**address** (_string_)
The contract address of a previously deployed Rentable contract.

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

```typescript
const myVault = await vault.getContract(sdk, address);
await myVault.vaultBalance();
```

## totalReleased

Returns the total amount of the ERC20 which has been claimed and released.

```
const myVault = await vault.getContract(sdk, address);
await myVault.totalReleased();
```

## claimMany

Allows owners of the ERC721 collection to claim their share of the ERC20 funding the vault for multiple tokens.

```typescript
const myVault = await vault.getContract(sdk, address);
const to = '0x1234567890123456789012345678901234567890';
const tokenIds = [0,1,2];
await myVault.claimMany(to, tokenIds);
```

**to** (_address_)
The address of the owner in the ERC721 collection to which ERC20 tokens will be sent.

**tokenIds** (_uint256[]_)
An array of tokens held by the owner against which to claim their share of the ERC20 tokens funded by the vault.

## claim

Allows owners of the ERC721 collection to claim their share of the ERC20 funding the vault for an individual token.

```typescript
const myVault = await vault.getContract(sdk, address);
const to = '0x1234567890123456789012345678901234567890';
const tokenId = 0;
await myVault.claim(to, tokenId);
```

**to** (_address_)
The address of the owner in the ERC721 collection to which ERC20 tokens will be sent.

**tokenId** (_uint256_)
The id of the token against which to claim a share of the ERC20 tokens funded by the vault.

## drain

A failsafe allowing the vault owner to withdraw ERC20 tokens sent to the vault

```typescript
const myVault = await vault.getContract(sdk, address);
const token = '0x1234567890123456789012345678901234567890';
await myVault.drain(token);
```

**token** (_IERC20_)
The address of the ERC20 token to withdraw from the vault.


## drainEth

A failsafe allowing the vault owner to withdraw ETH sent to the vault

```typescript
const myVault = await vault.getContract(sdk, address);
await myVault.drainEth();
```
