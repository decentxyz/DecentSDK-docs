An extension to [Edition](Edition.md) implementing [ERC4907A](https://chiru-labs.github.io/ERC721A/#/erc4907a) / [EIP4907](https://eips.ethereum.org/EIPS/eip-4907) allowing token owner's to grant time restricted user rights to another account.

[**Getting Started**](#getting-started)
[**Module Methods**](#module-methods)
[**Smart Contract Methods**](#smart-contract-methods)

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the Rentable module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```typescript
// Import SDK, chain configurations, and the Rentable module
import { DecentSDK, chain, rentable } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**deploy**](#deploy)
Deploy a minimal proxy clone of the Rentable implementation contract.

[**getContract**](#getcontract)
Get an ethers contract instance of a previously deployed Rentable contract.

## deploy

Deploy a minimal proxy clone of the Rentable implementation contract.

```typescript
const myNFT = await rentable.deploy(
  sdk,
  name,
  symbol,
  hasAdjustableCap,
  isSoulbound,
  maxTokens,
  tokenPrice,
  maxTokenPurchase,
  presaleMerkleRoot,
  presaleStart,
  presaleEnd,
  saleStart,
  saleEnd,
  royaltyBPS,
  payoutAddress,
  contractURI,
  metadataURI,
  metadataRendererInit,
  tokenGateConfig,
  onTxPending,
  onTxReceipt,
  parentIP
);

console.log("Rentable deployed to: ", myNFT.address);
```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**name** (_string_)
The name of the NFT collection.

**symbol** (_string_)
The symbol of the NFT collection.

**hasAdjustableCap** (_boolean_)
Include the ability to change maxTokens at a date after deployment.

**isSoulBound** (_boolean_)
Implementation of [Soulbound](https://vitalik.ca/general/2022/01/26/soulbound.html) NFTs so that tokens in this collection are non-transferrable.  Best set to `true` if NFTs are intended to be used as a credential or another purely non-financial use case.

**maxTokens** (_number_)
The total number of tokens allowed to be minted from the collection.

**tokenPrice** (_BigNumber_)
The price (in Wei) to mint a token from the collection.

**maxTokenPurchase** (_number_)
The maximum number of tokens allowed per mint.

**presaleMerkleRoot** (_number_ \| _BigNumber_)
A merkle root representation of the allowlisted accounts, and their relative max purchase and price per token.

```typescript
import { MerkleTree } from 'merkletreejs';
import { ethers } from 'ethers';

const createMerkleRoot = (allowlist: Allowed[]) => {
  const leaves = allowlist.map((leaf) => {
    const address = leaf[0];
    const maxQuantity = leaf[1];
    const pricePerToken = ethers.utils.parseEther(leaf[2].toString());
    return ethers.utils.solidityKeccak256(
      ["address", "uint256", "uint256"],
      [address, maxQuantity, pricePerToken]
    );
  });
  const tree = new MerkleTree(leaves, ethers.utils.keccak256, { sortPairs: true });
  return tree.getHexRoot();
}

const presaleMerkleRoot = createMerkleRoot([
  ['0xce90a7949bb78892f159f428d0dc23a8e3584d75', 1, 0.1],
  ['0xab5801a7d398351b8be11c439e05c5b3259aec9b', 1, 0.1],
]);
```

**presaleStart** (_number_ \| _BigNumber_)
Unix time presale ends.

**presaleEnd** (_number_ \| _BigNumber_)
Unix time presale ends.

**saleStart** (_number_ \| _BigNumber_)
Unix time general sale starts.  General sale applies to contracts deployed with and without an allowlist.

**saleEnd** (_number_ \| _BigNumber_)
Unix time general sale ends.

**royaltyBPS** (_number_)
The maximum number of tokens allowed per mint.

**payoutAddress** (_string_)
An alternate address for withdrawals and royalty payments may be used. Use zero address as the default setting for owner payouts.

**contractURI** (_string_)
The URI for contract level metadata.

**metadataURI** (_string_)
The base URI for the collection metadata.

**metadataRendererInit** (_MetadataRendererInit_)
An object containing metadata to initialize with the on-chain metadata renderer.

```typescript
type MetadataRendererInit = {
  description: string;
  imageURI: string;
  animationURI: string;
}
```

**tokenGateConfig** (_TokenGateConfig_) _optional_
The configuration for a token gate, an NFT contract from wich users must have a minimum balance to mint.  Think of this as a more dynamic allowlist or light anti-sybil mechanism.

```typescript
 type TokenGateConfig = {
  tokenAddress: string;
  minBalance: number;
  saleType: number;
}

enum SaleType {
  ALL = 0,
  PRESALE = 1,
  PRIMARY = 2
}
```

**onTxPending** (_Function_) - _optional_
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (_Function_) - _optional_
A callback function executed upon receipt of the deploy transaction.

**parentIP** (_string_) - _optional_
Implementation of [EIP 5553](https://eips.ethereum.org/EIPS/eip-5553) to assign token metadata to the address of another NFT with registered IP.

## getContract

Get an ethers contract instance of a previously deployed Rentable contract.

```typescript
const myNFT = await rentable.getContract(sdk, address);
```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**address** (_string_)
The contract address of a previously deployed Rentable contract.

## Smart Contract Methods

[**setUser**](#setuser)
Set a user and expiration for a token

[**userOf**](#userof)
Get the current user for a token

[**userExpires**](#userexpires)
Get the timestamp of expiration for a token

\*All methods available on [Edition](Edition.md) are inherited and available on Rentable.

## setUser

Set a user and expiration for a token

```typescript
const myNFT = await rentable.getContract(sdk, address);
await myNFT.setUser(tokenId, user, expires);
```

**tokenId** (_uint256_)
The id of the token.

**user** (_uint256_)
The new user of the NFT.

**expires** (_uint256_)
The timestamp at which the user expires.

## userOf

Get the current user for a token.

```typescript
const myNFT = await rentable.getContract(sdk, address);
await myNFT.userOf(tokenId);
```

**tokenId** (_uint256_)
The id of the token.

## userExpires

Get the timestamp of expiration for a token.

```typescript
const myNFT = await rentable.getContract(sdk, address);
await myNFT.userExpires(tokenId);
```

**tokenId** (_uint256_)
The id of the token.
