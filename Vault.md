# Vault

A time-locked vault to distribute [ERC20](https://eips.ethereum.org/EIPS/eip-20) tokens to owners of an [ERC721](https://eips.ethereum.org/EIPS/eip-721) collection at expiry based on their percentage of ownership in the collection.

## Module Methods

[**deploy**](#deploy)  
Deploy a minimal proxy clone of the Vault implementation contract.

[**getContract**](#getcontract)  
Get an ethers contract instance of a previously deployed Vault contract.

## deploy

Deploy a minimal proxy clone of the Vault implementation contract.

```
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

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**vaultDistributionTokenAddress** (string)  
The address of the ERC20 token that will be distributed by the vault.

**nftVaultKeyAddress** (*string*)  
The address of the ERC20 token that will be distributed by the vault.

**nftTotalSupply** (*number*)  
The total supply of the ERC721 collection that is wrapped by the vault.

**unlockDate** (*number*)  
The timestamp at which the vault will unlock and allow distributions.

**onTxPending** (*Function*) - *optional*  
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (*Function*) - *optional*  
A callback function executed upon receipt of the deploy transaction.

## getContract

Get an ethers contract instance of a previously deployed Vault contract.

```
const myVault = await vault.getContract(sdk, address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**address** (*string*)  
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

```
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

```
const myVault = await vault.getContract(sdk, address);
const to = '0x1234567890123456789012345678901234567890';
const tokenIds = [0,1,2];
await myVault.claimMany(to, tokenIds);
```

**to** (*address*)  
The address of the owner in the ERC721 collection to which ERC20 tokens will be sent.

**tokenIds** (*uint256[]*)  
An array of tokens held by the owner against which to claim their share of the ERC20 tokens funded by the vault.

## claim

Allows owners of the ERC721 collection to claim their share of the ERC20 funding the vault for an individual token.

```
const myVault = await vault.getContract(sdk, address);
const to = '0x1234567890123456789012345678901234567890';
const tokenId = 0;
await myVault.claim(to, tokenId);
```

**to** (*address*)  
The address of the owner in the ERC721 collection to which ERC20 tokens will be sent.

**tokenId** (*uint256*)  
The id of the token against which to claim a share of the ERC20 tokens funded by the vault.

## drain

A failsafe allowing the vault owner to withdraw ERC20 tokens sent to the vault

```
const myVault = await vault.getContract(sdk, address);
const token = '0x1234567890123456789012345678901234567890';
await myVault.drain(token);
```

**token** (*IERC20*)  
The address of the ERC20 token to withdraw from the vault.


## drainEth

A failsafe allowing the vault owner to withdraw ETH sent to the vault

```
const myVault = await vault.getContract(sdk, address);
await myVault.drainEth();
```
