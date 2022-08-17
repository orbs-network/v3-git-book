# Writing your lambda function

Your Lambda is written as a regular JS function.

Upon runtime, the backend process invokes your task function with a set of parameters according to its trigger type:

```js
// This task is planned to run on a time-based trigger
function myScheduledTask(web3, storage, config) {
    // do hard work
}

// This task is planned to run as reaction to events being emitted
function myEventsTask(web3, storage, config, event) {
    // do hard work
}

// This task is planned to run on block ranges
function myBlocksTask(web3, storage, config, fromBlock, toBlock) {
    // do hard work
}
```

- `web3`: web3 api for interacting with the blockchain
- `storage`: storage handler. Supports 2 methods:
  - `set(key, value)`: sets a certain value into local storage, using a key.
  - `get(key)`: returns value by key, or `undefined` if such key doesn't exist.
- `config`: key:value object containing the configuration, which you supply when [defining the trigger](./lambda-triggers/README.md).
- `event` (_only relevant for onEvent_) : the [Event](https://github.com/orbs-network/orbs-lambda/blob/master/interfaces.ts#L29) object which was emitted.
- `fromBlock` (_only relevant for onBlocks_) : the first block in the range to be scanned for potential triggers
- `toBlock` (_only relevant for onBlocks_) : the last block in the range to be scanned for potential triggers