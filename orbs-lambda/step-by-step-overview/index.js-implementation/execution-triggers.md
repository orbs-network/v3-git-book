# Execution Triggers

All triggers must be set during registration. A lambda may register multiple triggers.

```javascript
module.exports.register = function(engine) {
  // register all triggers here
  engine.onInterval(...);
  engine.onCron(...);
  engine.onEvent(...);
  engine.onBlocks(...);
}
```

### Concurrency

There are dozens of independent [validators](../../../) that execute lambdas on Orbs Network. By default, every time the trigger condition takes place, a single validator from the group will be selected to execute the lambda (this is handled automatically by the protocol).

If you want multiple validators to execute the trigger concurrently (in order to implement some custom consensus behavior), this can be specified in most triggers under the `concurrency` argument.

## Trigger on interval

Execute a lambda function repeatedly every interval of time. For example once a day. There are no guarantees when exactly the function will run, meaning a lambda function that runs daily may trigger at any specific hour during the day. The function will run at least once in the requested interval, but in rare cases may also trigger more than once during the interval.

Interval string format: `[integer]m|h|d`\
Examples: `"10m"` - every 10 minutes, `"6h"` - every 6 hours, `"30d"` - every 30 days

```javascript
engine.onInterval(handler, {
  interval, // required string - [integer]m|h|d per format above
  network, // optional string - Network ID per supported networks
  concurrency, // optional string - "single" for single node (default), "multiple" for multiple nodes
});
```

```javascript
async function handler(args) {
  args.web3 // initialized web3 object if network was selected on registration
  args.guardians /* key-value object of Guardians data: 
  {
  "NEOPLY": {
    "weight": 279476867,
    "nodeAddress": "0xf8cd99a88707c4fc64ac91f237af8570a83cc018",
    "guardianAddress": "0x9520f53fd81c668e8088ae194c40e3f977b73d28",
    "ip": "54.95.108.148",
    "currentNode": true
  },
  "오뽀가디언 - WhaleCoreStake - ORBS KOREA - ": {
    "weight": 134901962,
    "nodeAddress": "0x8cd2a24f0c3f50bce2f12c846277491433b47ae0",
    "guardianAddress": "0xc5e624d6824e626a6f14457810e794e4603cfee2",
    "ip": "34.227.204.75",
    "currentNode": false
  }, 
}
....
*/
```

### Example

```javascript
// run every 10 minutes on Ethereum mainnet
engine.onInterval(handler, { interval: "10m", network: "ethereum" });
```

## Trigger on cron

Execute a lambda in a predefined schedule according to a standard cron expression.

Cron string format: the standard format as [explained here](https://en.wikipedia.org/wiki/Cron)\
Example: `"42 * * * *"` - run every hour when the minute is 42 (19:42, 20:42, etc)\
Example: `"0 0 * * 1"` - run at 00:00 every Monday

```javascript
engine.onCron(handler, {
  cron, // required string - standard cron format
  network, // optional string - Network ID per supported networks
  concurrency, // optional string - "single" for single node (default), "multiple" for multiple nodes
});
```

```javascript
async function handler(args) {
  args.web3 // initialized web3 object if network was selected on registration
  args.guardians /* key-value object of Guardians data: 
  {
  "NEOPLY": {
    "weight": 279476867,
    "nodeAddress": "0xf8cd99a88707c4fc64ac91f237af8570a83cc018",
    "guardianAddress": "0x9520f53fd81c668e8088ae194c40e3f977b73d28",
    "ip": "54.95.108.148",
    "currentNode": true
  },
  "오뽀가디언 - WhaleCoreStake - ORBS KOREA - ": {
    "weight": 134901962,
    "nodeAddress": "0x8cd2a24f0c3f50bce2f12c846277491433b47ae0",
    "guardianAddress": "0xc5e624d6824e626a6f14457810e794e4603cfee2",
    "ip": "34.227.204.75",
    "currentNode": false
  }, 
}
....
*/
}
```

### Example

```javascript
// run every Monday at midnight (00:00) on Polygon mainnet
engine.onCron(handler, { cron: "0 0 * * 1", network: "polygon" });
```

## Trigger on contract event

Execute a lambda every time a specific smart contract [emits a new event](https://solidity-by-example.org/events/) on-chain. The lambda will only be triggered for new events, meaning past events emitted before the lambda was deployed will not trigger execution. If multiple events were emitted, the lambda will be called separately for each one.

Some arguments, such as the optional filter and the resulting event passed to the handler, are compatible with the [`getPastEvents`](https://web3js.readthedocs.io/en/v1.8.0/web3-eth-contract.html#getpastevents) method in web3.

```javascript
engine.onEvent(handler, {
  network, // required string - Network ID per supported networks
  contractAddress, // required string - smart contract address starting with "0x"
  abi, // required array - ABI interface of the smart contract
  eventName, // required string - the event name in ABI
  filter, // optional object - as in getPastEvents() web3.js method
  concurrency, // optional string - "single" for single node (default), "multiple" for multiple nodes
});
```

```javascript
async function handler(args) {
  args.web3 // initialized web3 object according to the network
  args.event // the actual event as in getPastEvents() web3.js method return value
  args.guardians /* key-value object of Guardians data: 
  {
  "NEOPLY": {
    "weight": 279476867,
    "nodeAddress": "0xf8cd99a88707c4fc64ac91f237af8570a83cc018",
    "guardianAddress": "0x9520f53fd81c668e8088ae194c40e3f977b73d28",
    "ip": "54.95.108.148",
    "currentNode": true
  },
  "오뽀가디언 - WhaleCoreStake - ORBS KOREA - ": {
    "weight": 134901962,
    "nodeAddress": "0x8cd2a24f0c3f50bce2f12c846277491433b47ae0",
    "guardianAddress": "0xc5e624d6824e626a6f14457810e794e4603cfee2",
    "ip": "34.227.204.75",
    "currentNode": false
  }, 
}
....
*/
}
```

### Example

```javascript
// run every time there's a swap in the Uniswap V2 pair for ORBS-ETH
const abi = [{"name":"Swap","type":"event","anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"sender","type":"address"},{"indexed":false,"internalType":"uint256","name":"amount0In","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"amount1In","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"amount0Out","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"amount1Out","type":"uint256"},{"indexed":true,"internalType":"address","name":"to","type":"address"}]}];
engine.onEvent(handler, { network: "ethereum", contractAddress: "0xC98B3B8C7CC0D7D925d1a407347b845D9F001391", abi, eventName: "Swap" });
```

## Trigger on blocks

Execute a lambda every time new blocks are created on-chain. The lambda will only be triggered for new blocks, meaning past blocks created before the lambda was deployed will not trigger execution. If multiple blocks were created since the lambda was last triggered, an array of blocks is given to the handler. The range of blocks is always continuous between executions, so no blocks are missed.

```javascript
engine.onBlocks(handler, {
  network, // required string - Network ID per supported networks
  concurrency, // optional string - "single" for single node (default), "multiple" for multiple nodes
});
```

```javascript
async function handler(args) {
  args.web3 // initialized web3 object according to the network
  args.fromBlock // number - the first block number in the range
  args.toBlock // number - the last block number in the range
  args.guardians /* key-value object of Guardians data: 
  {
  "NEOPLY": {
    "weight": 279476867,
    "nodeAddress": "0xf8cd99a88707c4fc64ac91f237af8570a83cc018",
    "guardianAddress": "0x9520f53fd81c668e8088ae194c40e3f977b73d28",
    "ip": "54.95.108.148",
    "currentNode": true
  },
  "오뽀가디언 - WhaleCoreStake - ORBS KOREA - ": {
    "weight": 134901962,
    "nodeAddress": "0x8cd2a24f0c3f50bce2f12c846277491433b47ae0",
    "guardianAddress": "0xc5e624d6824e626a6f14457810e794e4603cfee2",
    "ip": "34.227.204.75",
    "currentNode": false
  }, 
}
....
*/
}
```

### Example

```javascript
// run every time there are new blocks on BNB Chain
engine.onBlocks(handler, { network: "bsc" });
```
