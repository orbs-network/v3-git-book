# Allowed Packages

A lambda may require specific [NPM packages](https://npmjs.com/) that are present in this list. To request any additional NPM packages to be whitelisted, please open an issue on the main [Orbs Lambda repo](https://github.com/orbs-network/orbs-lambda).

You can see the exact versions of all packages by inspecting [`package.json`](https://github.com/orbs-network/orbs-lambda/blob/master/package.json) in the main Orbs Lambda repo.

## web3

Package: [https://www.npmjs.com/package/web3](https://www.npmjs.com/package/web3)

Provides basic interaction with EVM blockchains and smart contracts through simple JavaScript API. Note that most trigger event handlers receive an initialized `web3` object that is ready for mainnet interaction.

<pre class="language-javascript"><code class="lang-javascript"><strong>const Web3 = require("web3");
</strong></code></pre>

## ethereum-multicall

Package: [https://www.npmjs.com/package/ethereum-multicall](https://www.npmjs.com/package/ethereum-multicall)

Multicall allows multiple smart contract constant function calls to be grouped into a single call and the results aggregated into a single result. This reduces the number of separate JSON RPC requests that need to be sent over the network and provides the guarantee that all values returned are from the same block.

```javascript
const { Multicall } = require("ethereum-multicall");
```

## bn.js

Package: [https://www.npmjs.com/package/bn.js](https://www.npmjs.com/package/bn.js)

Big numbers in JavaScript without floating point support, only integers. Compatible with the numeric types of all EVM blockchains.

```javascript
const BN = require("bn.js");
```

## bignumber.js

Package: [https://www.npmjs.com/package/bignumber.js](https://www.npmjs.com/package/bignumber.js)

A JavaScript library for arbitrary-precision decimal and non-decimal arithmetic. Supports floating point numbers, not just integers.

```javascript
const BigNumber = require("bignumber.js");
```

## node-fetch

Package: [https://www.npmjs.com/package/node-fetch](https://www.npmjs.com/package/node-fetch)

A light-weight module that brings [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch\_API) to Node.js and allows to make arbitrary HTTP requests to external websites and endpoints.

```javascript
const fetch = require("node-fetch");
```

## axios

Package: [https://www.npmjs.com/package/axios](https://www.npmjs.com/package/axios)

Promise based HTTP client for the browser and Node.js. Different package that allows to make arbitrary HTTP requests to external websites and endpoints.

```javascript
const axios = require("axios").default;
```

## @orbs-network/\*

Packages: [https://www.npmjs.com/org/orbs-network](https://www.npmjs.com/org/orbs-network)

All packages published by the Orbs organization on NPM are allowed for use.
