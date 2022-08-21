# Writing your lambda function

Your Lambda should be written as a regular JS function.

Upon runtime, the backend process invokes your task function with a set of parameters according to its trigger type:

```javascript
// This task is planned to run on a time-based trigger
function myScheduledTask(web3, storage, guardians, config) {
    // do hard work
}

// This task is planned to run as reaction to events being emitted
function myEventsTask(web3, storage, guardians, config, event) {
    // do hard work
}

// This task is planned to run on block ranges
function myBlocksTask(web3, storage, guardians, config, fromBlock, toBlock) {
    // do hard work
}
```

## web3
Initialized [web3.js](https://web3js.readthedocs.io/) object for interacting with the blockchain. Comes with pre-injected RPC provider, aw well as account credentials for signing transactions.

## storage
storage handler. Supports the following methods:
#### set(key, value, [options])
Set key to hold the string value. If key already holds a value, it is overwritten. Any previous time to live (ttl) associated with the key is discarded on successful SET operation. Max value size is 1 KB.

`options`: 
- `ttl`: Set the specified expire time, in seconds.
#### get(key)
Get the value of key. If the key does not exist the special value `undefined` is returned.
#### remove(key)
Removes the specified keys. A key is ignored if it does not exist.
## guardians
Array of guardians (executors) addresses.
## config
key:value object containing the configuration, which you supply when [defining the trigger](./lambda-triggers/README.md).
## event
(_only relevant for onEvent_)

The [Event](https://github.com/orbs-network/orbs-lambda/blob/master/interfaces.ts#L29) object which was emitted.
## fromBlock
(_only relevant for onBlocks_)

The first block in the range to be scanned for potential triggers.
## toBlock
(_only relevant for onBlocks_)

The last block in the range to be scanned for potential triggers.