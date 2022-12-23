# ZKEdition

An extension of Decent's gas-optimized [ERC721A](https://www.azuki.com/erc721a) which allows minting multiple NFTs for nearly the cost of one.  ZKEditions enable people to collect NFTs while preserving their privacy.  A primary reason that this is important is collectors are able to showcase their NFTs without revealing their wallet address or every other transaction they have executed.  Oversharing transaction histories can becomne severe security issue but is remedied via ZKEditions where a wallet must submit a valid zk proof to call the contract's mint function.  Implementations of ZKEdtitions that we find exciting include:

**Private NFT auctions**: the identities of participants and the amounts they have bid can be concealed.  Think how useful this would have been to [ConstitutionDAO](https://www.artnews.com/art-news/news/why-ken-griffin-bought-us-constitution-1234636325/)!

**Brand sponsored NFTs**: corporations might wish to use NFTs as loyalty programs, carrots to attract new customers, or means of tracking impressions. These are interesting use cases; however, these brands should not be able to querey wallet addresses to build detailed user profiles based on all of your financial transactions!  ZKEditions accomplish the stated goal without the dubious externalities.

[**Getting Started**](#getting-started)  
[**Module Methods**](#module-methods)  
[**Smart Contract Methods**](#smart-contract-methods)  

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the ZKEdition module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```
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

```
const myNFT = await edition.deploy(
  sdk,
  name,
  symbol,
  hasAdjustableCap,
  parentIP,
  maxTokens,
  tokenPrice,
  maxTokenPurchase,
  merkleRoot,
  presaleStart,
  presaleEnd,
  saleStart,
  saleEnd,
  zkVerifier,
  royaltyBPS,
  metadataURI,
  metadataRendererInit,
  hasTokenGate,
  onTxPending,
  onTxReceipt
);

console.log("Edition deployed to: ", myNFT.address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**name** (*string*)  
The name of the NFT collection.

**symbol** (*string*)  
The symbol of the NFT collection.

**hasAdjustableCap** (*boolean*) - *optional*  
Include the ability to change `maxTokens` at a date after deployment.

**parentIP** (*string*) - *optional*  
Implementation of [EIP 5553](https://eips.ethereum.org/EIPS/eip-5553) to assign token metadata to the address of another NFT with registered IP.

**maxTokens** (*number*)  
The total number of tokens allowed to be minted from the collection.

**tokenPrice** (*BigNumber*)  
The price (in Wei) to mint a token from the collection.

**maxTokenPurchase** (*number*)  
The maximum number of tokens allowed per mint.

**merkleRoot** (*string*) - *optional* 
Hash of allowlist updated to gate minting.

**presaleStart** (*number*) - *optional* 
Unix time presale goes live.

**presaleEnd** (*number*) - *optional* 
Unix time presale ends.

**saleStart** (*number*) - *optional but recommended*
Unix time general sale starts.  General sale applies to contracts deployed with and without an allowlist.

**saleEnd** (*number*) - *optional but recommended*
Unix time general sale ends.

**zkVerifier** (*string*)
zkProof enabling wallet to call the contract's mint function.

**royaltyBPS** (*number*)  
The maximum number of tokens allowed per mint.

**metadataURI** (*string*)  
The base URI for the collection metadata.

**hasTokenGate** (*string*)  
The address of an NFT contract from wich users must own a token to mint.  Think of as a more dynamic allowlist or light anti-sybil mechanism.

**metadataRendererInit** (*MetadataRendererInit*)  
An object containing metadata to initialize with the on-chain metadata renderer.

**onTxPending** (*Function*) - *optional*  
A callback function executed upon submission of the deploy transaction.

**onTxReceipt** (*Function*) - *optional*  
A callback function executed upon receipt of the deploy transaction.

## getContract

Get an ethers contract instance of a previously deployed Edition contract.

```
const myNFT = await edition.getContract(sdk, address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**address** (*string*)  
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

```
const myNFT = await edition.getContract(sdk, address);
await myNFT.mint(1, { value: ethers.utils.parseEther('0.1') });
```

**numberOfTokens** (*uint256*)  
The name of the NFT collection.


## flipSaleState

Toggles whether to allow minting.

```
const myNFT = await edition.getContract(sdk, address);
await myNFT.flipSaleState();
```


## withdraw

Allows the owner to withdraw the contract balance.

```
const myNFT = await edition.getContract(sdk, address);
await myNFT.withdraw();
```

## setBaseURI

Allows the owner to update the base URI for token metadata.

```
const myNFT = await edition.getContract(sdk, address);
await myNFT.setBaseURI('https://nft.example/metadata/');
```

**uri** (*uint256*)  
The base URI serving metadata for the NFT collection.
