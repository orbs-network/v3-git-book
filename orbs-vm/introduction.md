# Introduction

![](../.gitbook/assets/logo-vm.png)

## Why use ORBS-VM?

Current smart contracts are limited in various ways, including:&#x20;

* Certain logic is too complex to implement on smart contracts in any current blockchain.
* Implementing this type of logic outside of the blockchain requires using centralized infrastructure.
* Smart contracts are not able to trigger calls to themselves.

Orbs VBM solves these problems and offers the following benefits:

* Allows interaction between several blockchains.
* Maintains fast cache logic.
* Provides decentralized backend infrastructrue that complements your Dapp smart contracts.

> Please note that you should only use ORBS-VM if you have determined that ORBS-Lambda does not fulfill your Dapp's requirements. For simpler functions, ORBS-Lambda is much easier to set up and maintain.

## Key benefits of using ORBS-VM

* Your Dapp can benefit from running on a decentralized, permissionless network, instead of centralized services.
* Your container is always UP, for as long the Orbs network continues to function.&#x20;
* Your Dapp can utilize the Orbs Network's consensus decisions and data. For example, you can select a particular Orbs Guardian node within ORBS-VM to perform the next action, or elect to split the computed data among several nodes to distribute computation.

## How  it works

You can configure your Dapp's logic to run on ORBS-VM in a few steps:

* Wrap your entire logic onto a single docker image
* Push the docker image to a public docker repo repo such as [https://hub.docker.com/](dockerhub/)
* Open a pull request in the v3-ORBS-VM github repository, as described [here](deploy.md)
* Your container is then gradually deployed to the Orbs Network.
