---
coverY: 0
---

# What is Orbs VM?

## Decentralized Docker-Based Virtual Machine

Orbs VM is a dedicated and decentralized virtual machine, similar in concept to [AWS EC2](https://aws.amazon.com/ec2/) - only decentralized.

Orbs VM services are implemented as [Docker](https://www.docker.com/) containers, deployed to the Orbs Network and then executed by the network validators. Much like AWS EC2 container services, there is minimal devops involved as orchestration is automated. Unlike AWS EC2, the protocol is fully transparent and decentralized, providing execution guaranteed to the user community by relying on dozens of independent network validators that participate in the protocol.

### Any Programming Language

Services in Orbs VM are implemented as an industry standard container - Docker. As such, they can rely on any familiar programming language like Go, C++, Rust, JavaScript, Python and Java. Developers are not required to learn unfamiliar smart contract languages or operate strange toolchains - they can rely on their existing knowledge.

### Always On

Just like regular Docker containers, Orbs VM services are always-on. They are not event-driven and do not become dormant when unused. Any event-driven logic can be implemented inside the container by implementing the logic that scans continuously for the desired condition. For example, services can monitor any number of L1 blockchains by continuously reading new published blocks and analyzing their content.

### Enhance Existing Smart Contracts

Orbs VM is not meant to replace existing L1 smart contracts. It is a complementary solution that allows developers to enrich their business logic with actions that the smart contract sandbox is [unable to do](../overview/enhanced-execution.md), without sacrificing decentralization. Dapps that currently rely on their own centralized backends are welcome to migrate these backends to Orbs VM and eliminate the centralized bottlenecks from their offering.

### Alternatives

Before trying Orbs VM, please consider [Orbs Lambda](broken-reference) - a solution designed for ease of use that resembles AWS Lambda. Orbs VM is more difficult to use, but is more flexible and designed for  complex use-cases that require the service to be always-on or require non-JavaScript dependencies.
