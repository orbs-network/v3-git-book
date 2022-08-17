# ORBS-VM introduction

## Why use ORBS-VM?
- Some logic is too hard to implement on smart contracts in any blockchain.
- Implementing this login outside the blockchain is centralized.
- Smart contract can not trigger calls to themselves.
- Interaction between several blockchain.
- Maintain fast cache logic.
- Decentralized backend complementry to your dapp smart contracts.

> Please note that ORBS-VM should be chosen only if ORBS-Lambda does not fulfill your dapp's requirement, As ORBS_Lambda is much easier to set up and maintain. 

## keypoints using ORBS-VM
- It can benefit from running on a decentralized permissionless network.
- your container is always UP so long the network is alive
- it can enjoy ORBS concensus decisions and data, for instace, which orbs-node with ORBS-VM performs the next action, or split the computed data amongst several nodes to distribute computation.

## how does it work
You may get your dapp logic to run on as an ORBS-VM in a very few steps:

- Wrap your entire logic on a single docker image
- Push it to a public docker repo repo such as [https://hub.docker.com/](dockerhub)
- Open a pull request in v3-ORBS-VM github as described [here](./deploy.md)
- You container is gradually deployed to the orbs-network.


