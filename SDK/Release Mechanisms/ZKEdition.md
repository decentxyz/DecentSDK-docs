An extension of Decent's gas-optimized [ERC721A](https://www.azuki.com/erc721a) which allows minting multiple NFTs for nearly the cost of one.  ZKEditions enable people to collect NFTs while preserving their privacy.  A primary reason that this is important is collectors are able to showcase their NFTs without revealing their wallet address or every other transaction they have executed.  Oversharing transaction histories can become severe security issue but is remedied via ZKEditions where a wallet must submit a valid zero knowledge proof to call the contract's mint function.  Implementations of ZKEdtitions that we find exciting include:

**Private NFT auctions**: the identities of participants and the amounts they have bid can be concealed.  Think how useful this would have been to [ConstitutionDAO](https://www.artnews.com/art-news/news/why-ken-griffin-bought-us-constitution-1234636325/)!

**Brand sponsored NFTs**: corporations might wish to use NFTs as loyalty programs, carrots to attract new customers, or means of tracking impressions. These are interesting use cases; however, these brands should not be able to query wallet addresses to build detailed user profiles based on all of your financial transactions!  ZKEditions accomplish the stated goal without the dubious externalities.

[**Getting Started**](#getting-started)
[**Module Methods**](#module-methods)
[**Smart Contract Methods**](#smart-contract-methods)

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the ZKEdition module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```typescript
// Import SDK, chain configurations, and the Edition module
import { DecentSDK, chain, edition } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**deploy**](#deploy)
Deploy a minimal proxy clone of the Edition implementation contract.

[**getContract**](#getcontract)
Get an ethers contract instance of a previously deployed Edition contract.

## deploy

Deploy a minimal proxy clone of the Edition implementation contract.

```typescript
const myNFT = await edition.deploy(
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
  zkVerifier,
  onTxPending,
  onTxReceipt,
  parentIP
);

console.log("Edition deployed to: ", myNFT.address);
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

**zkVerifier** (_string_)
zkProof enabling wallet to call the contract's mint function.

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

Get an ethers contract instance of a previously deployed Edition contract.

```typescript
const myNFT = await edition.getContract(sdk, address);
```

**sdk** (_SDK_)
An instance of the DecentSDK, configured with a chain and signer.

**address** (_string_)
The contract address of a previously deployed Edition contract.

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

```typescript
const myNFT = await edition.getContract(sdk, address);
await myNFT.mint(1, { value: ethers.utils.parseEther('0.1') });
```

**numberOfTokens** (_uint256_)
The name of the NFT collection.

## flipSaleState

Toggles whether to allow minting.

```typescript
const myNFT = await edition.getContract(sdk, address);
await myNFT.flipSaleState();
```

## withdraw

Allows the owner to withdraw the contract balance.

```typescript
const myNFT = await edition.getContract(sdk, address);
await myNFT.withdraw();
```

## setBaseURI

Allows the owner to update the base URI for token metadata.

```typescript
const myNFT = await edition.getContract(sdk, address);
await myNFT.setBaseURI('https://nft.example/metadata/');
```

**uri** (_uint256_)
The base URI serving metadata for the NFT collection.
