# Execution Environment

## CPU architecture

The official CPU architecture supported by the protocol is `x86_64` since network validators run cloud-compatible machines (normally Linux, but this is not required). To make sure your image supports this architecture, it should support the `amd64` variant. If you want to keep image size down, it's ok to support this architecture only.

## Memory

A running docker image should not consume more than 500MB of RAM. Consuming too much memory for sustained durations will put the service at risk of termination and non execution.

The service may naturally keep variables in memory to maintain its internal state. Regard this memory as a nice-to-have cache only, meaning the service may be restarted from scratch without warning and lose all of its memory contents.

## Persistent disk storage

A service is allowed to use persistent disk storage for data. This storage is not intended for big data and should be limited to 1GB of space per node (the distributed storage is then 1GB multiplied by the number of nodes running the container which can be dozens).

You should be aware that although most validator nodes have been quite stable since mainnet launch in 2019, validators may change, decide to leave the network and others may come in their place. Any data stored on a specific node may be lost. By continuously synchronizing important data across all validator nodes, there's strong certainty that this data would not be lost.

If you need a dedicated storage solution, there are quite a few decentralized storage solutions available in the industry. Small amounts of data with extremely high availability and robustness can be stored on-chain on smart contracts in networks like Polygon and Avalanche. Large amounts of data can be stored on decentralized services like [IPFS](https://ipfs.tech/) and [TON Storage](https://ton-blockchain.github.io/docs/ton.pdf) (4.1.7). An overview of available industry storage solutions is available [here](https://ethereum.org/en/developers/docs/storage/).

## CPU load

Orbs VM is not designed for computationally intensive actions. Most services are [I/O-bound](https://stackoverflow.com/questions/868568/what-do-the-terms-cpu-bound-and-i-o-bound-mean). If your business logic is CPU-bound, Orbs VM may not be the right solution for you. Containers that consume excessive CPU for long durations of time (over 20% of an average cloud core) are at risk of termination and non execution.

It is a good practice to spread CPU consumption over time. It is also a good practice to spread intense I/O operations over time, for example avoiding heavy reading and writing to disk for long periods of time.

## Communication and ports

Containers are able to listen for incoming connections and make outgoing network requests. Port mapping for your container is specified during deployment.

## Standard output and logs

A container may output logs to standard output (stdout). A recent extract of these logs is available for analysis by visiting the network [status page](https://status.orbs.network). Be aware that these logs are publicly accessible to anyone.

## Privacy and secrets

Much like smart contracts on-chain, Orbs VM is a decentralized protocol running on public and open infrastructure. This means that the source code of your service is generally expected to be open and all data retained by the service is publicly available to any community auditor. Do not store any private information or secrets that you would not otherwise store in a smart contract.
