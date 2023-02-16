---
title: "Registry"
excerpt: ""
---
The Registry serves as a public on-chain record of all contracts deployed via the DecentSDK and as a point of entry for the Decent Cross-Chain Indexer, which aggregates data across all of the EVM-compatible chains to which the DecentSDK has been deployed. The data is available to be consumed by other indexers, or utilized on-chain by other smart contracts.

[**Getting Started**](#getting-started)  
[**Module Methods**](#module-methods)  
[**Smart Contract Methods**](#smart-contract-methods)  

## Getting Started

To begin we'll import the DecentSDK, chain configurations, and the Registry module.

Then we'll setup our signer (via wagmi/ethers) and create a new instance of the DecentSDK.

```
// Import SDK, chain configurations, and the Registry module
import { DecentSDK, chain, registry } from "@decent.xyz/sdk";

// Get the signer via wagmi or configure using ethers
// Setup the SDK with the desired chain and signer
const sdk = new DecentSDK(chain.goerli, signer);
```

## Module Methods

[**query**](#query)  
Query the registry for all deployments by a specified deployer account.

[**getContract**](#getcontract)  
Get an ethers contract instance of the Registry contract.

## query

Query the registry for all deployments by a specified deployer account.

```
const deployments = await registry.query(sdk, address);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

**address** (*string*)  
The address of the deployer account.

## getContract

Get an ethers contract instance of the Registry contract.

```
const theRegistry = await registry.getContract(sdk);
```

**sdk** (*SDK*)  
An instance of the DecentSDK, configured with a chain and signer.

## Smart Contract Methods

[**register**](#register)  
Registers a contract with the Registry.

[**remove**](#remove)  
Removes a contract from the Registry.

[**query**](#query-1)  
Query the registry for all deployments by a specified deployer account.

## register

Registers a contract with the Registry.

```
const theRegistry = await registry.getContract(sdk);
await theRegistry.register(deployer, deployment, key);
```

**_deployer** (*address*)  
The address of the deployer account.

**_deployment** (*address*)  
The address of the deployed contract.

**_key**  (*string*)  
An identifier which is emitted but not stored, and may be used to reference different types of deployments.

## remove

Removes a contract from the Registry.

```
const theRegistry = await registry.getContract(sdk);
await theRegistry.remove(deployer, deployment);
```

**_deployer** (*address*)  
The address of the deployer account.

**_deployment** (*address*)  
The address of the deployed contract to remove.

## query

Query the registry for all deployments by a specified deployer account.

```
const theRegistry = await registry.getContract(sdk);
await theRegistry.query(deployer);
```

**address** (*string*)  
The address of the deployer account.