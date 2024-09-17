---
coverY: 0
---

# What is Orbs Lambda?

## Decentralized Serverless Cloud Function

Orbs Lambda is an event driven, serverless and decentralized cloud function, similar in concept to [AWS Lambda](https://aws.amazon.com/lambda/) - only decentralized.

Cloud function are implemented in a few lines of code, deployed to the Orbs Network and then executed by the network validators. Much like AWS Lambda, there is no devops involved and no instances to worry about. Unlike AWS Lambda, the protocol is fully transparent and decentralized, providing execution guaranteed to the user community by relying on dozens of independent network validators that participate in the protocol.

### Code in JavaScript

Cloud function in Orbs Lambda are written in an industry standard language - JavaScript (or TypeScript).  Developers are not required to learn unfamiliar smart contract languages or operate strange toolchains - they can rely on their existing knowledge. Developers are free to utilize dozens of familiar [NPM](https://www.npmjs.com/) packages such as [web3.js](https://www.npmjs.com/package/web3) or [node-fetch](https://www.npmjs.com/package/node-fetch).

### Execution Triggers

Orbs Lambda cloud functions are executed automatically according to pre-chosen triggers. Triggers can include a scheduled time interval (similar to a cron job), on-chain events from multiple L1 blockchains (logs emitted from smart contracts or state changes) and HTTP requests. Once a lambda function is deployed, network validators monitor these triggers and guarantee execution as soon as they occur.

### Enhance Existing Smart Contracts

Orbs Lambda is not meant to replace existing L1 smart contracts. It is a complementary solution that allows developers to enrich their business logic with actions that the smart contract sandbox is [unable to do](../overview/enhanced-execution.md), without sacrificing decentralization. Dapps that are currently relying on their own centralized backends are welcome to migrate these backends to Orbs Lambda and eliminate the centralized bottlenecks from their offering.

### Alternatives

Orbs Lambda is designed for ease of use. Writing and deploying an Orbs Lambda function can take as little as 30 minutes. For a more powerful solution that resembles AWS EC2, see [Orbs VM](broken-reference).
