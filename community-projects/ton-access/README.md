# TON Access

## What is TON Access?

Unthrottled anonymous RPC access to TON blockchain via the dozens of decentralized nodes of the Orbs Network.

Access a network of public API endpoints that allow TON dapp clients to make HTTP queries from the browser to TON blockchain (call getters, balances, get block data, etc). Access is unrestricted without an API Key and without requiring dapps to run any backend.

Supports all popular RPC protocols on TON:

1. [TonCenter HTTP API v2](https://toncenter.com/api/v2/) - replaces the [https://toncenter.com/api/v2/jsonRPC](https://toncenter.com/api/v2/jsonRPC) endpoint
2. [TonHub HTTP API v4](https://github.com/ton-foundation/ton-api-v4) - replaces the [https://mainnet-v4.tonhubapi.com](https://mainnet-v4.tonhubapi.com/) endpoint
3. [Raw ADNL Proxy](https://github.com/ton-community/ton-lite-client) - coming soon

### Benefits of using the Orbs TON Access

1. **No throttling for anonymous users**\
   RPC access like [https://toncenter.com/api/v2/jsonRPC](https://toncenter.com/api/v2/jsonRPC) throttle anonymous users to 1 request per second. Most dapps cannot operate under these restrictions since their users are anonymous. The Orbs Network endpoints are designed to serve anonymous dapp users and will not restrict your users from using your dapp client, except in extreme cases of abuse.
2. **No need for registering an API Key**\
   RPC access like [https://toncenter.com/api/v2/jsonRPC](https://toncenter.com/api/v2/jsonRPC) reduce user throttling by requiring you to register an API Key. This API Key cannot be stored client-side since it can be abused (it's supposed to be a secret) and dapps should not run a centralized backend to store this secret since they should be decentralized.
3. **No need to run your own RPC backend**\
   If you're building a dapp, your dapp should be decentralized so it can be trustless. If you're running your own centralized backend as part of your dapp, you've made your dapp centralized. If your backend suffers downtime for example, your users will lose access to their funds. If the infrastructure is decentralized, you don't need to worry about it.
4. **Decentralized access to the chain**\
   By relying on [https://toncenter.com/api/v2/jsonRPC](https://toncenter.com/api/v2/jsonRPC), you're relying on a centralized business (toncenter.com), not a protocol. The Orbs Network TON-Access is a decentralized protocol operated by dozens of [independent nodes](https://status.orbs.network/) that are all part of the [Orbs Network](https://github.com/orbs-network). The network mainnet is running since 2019 and validators are staked with Proof-of-Stake consensus with over $100 million TVL locked. The network is extremely robust against downtime due to the number of independent nodes.

See full developer documentation here: [https://github.com/orbs-network/ton-access](https://github.com/orbs-network/ton-access)
