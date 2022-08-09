# orbs-vm introduction

## why orbs-vm?
- some logic is too hard to implement on smart contracts on any platform
- smart contract can not trigger calls to themselves
- interaction between several blockchain
- decentralized backend complementry to your dapp smart contracts

## how does it work
- wrap your entire logic on a single docker image
- push it to a public repo
- open a pull request in v3-orbs-vm github repo
- once authorized - you container is gradually deployed to the orbs-network.

## why use orbs-vm
- It can benefit from running on a decentralized permissionless network.
- your container is always UP so long the network is alive
- it can enjoy ORBS concensus decisions and data, for instace, which orbs-node with orbs-vm performs the next action, or split the computed data amongst several nodes to distribute computation.

