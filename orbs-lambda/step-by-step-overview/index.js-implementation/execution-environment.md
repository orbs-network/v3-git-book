# Execution Environment

## Memory

A lambda function should not consume more than 100MB of RAM. Consuming too much memory will put the lambda at risk of termination and non execution.

A lambda may keep global variables in memory to maintain its internal state. Regard this memory as a nice-to-have cache only, meaning the lambda may be restarted from scratch without warning and lose all of its memory contents. An appropriate use of this cache is to initialize web3 [contract objects](https://web3js.readthedocs.io/en/v1.8.0/web3-eth-contract.html) for example.

## Persistent disk storage

A lambda is not allowed to access the local filesystems and may not rely on the disk to store its persistent storage. If you require persistent storage, take a look at allowed packages that provide some of this functionality.

## CPU load

Orbs Lambda is not designed for computationally intensive actions. Most lambdas are [I/O-bound](https://stackoverflow.com/questions/868568/what-do-the-terms-cpu-bound-and-i-o-bound-mean). If your business logic is CPU-bound, Orbs Lambda may not be the right solution for you. Lambdas that consume excessive CPU for long durations of time (over 10% of an average cloud core) are at risk of termination and non execution.

## Standard output and logs

A lambda may output logs to standard output (stdout) with commands like `console.log()`. A recent extract of these logs is available for analysis by visiting the network [status page](https://status.orbs.network).

## Throwing exceptions

Exceptions thrown from within lambda code are logged in the output of the lambda. A recent list of exceptions is available for analysis by visiting the network [status page](https://status.orbs.network).

## Privacy and secrets

Much like smart contracts on-chain, Orbs Lambda is a decentralized protocol running on public and open infrastructure. This means that the source code of your function is open and all data retained by the lambda is publicly available to any community auditor. Do not store any private information or secrets that you would not otherwise store in a smart contract.
