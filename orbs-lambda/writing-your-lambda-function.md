# Writing your lambda function

Your Lambda is written as a regular JS function, which receives the following arguments:

```ts
interface ExecutionArgs {
    // key:value configuration
    config: {[key: string]: any};
    // List of guardians addresses
    // guardians: string[]
    // web3 api for interacting with the blockchain
    web3: any;
    // the first block in the range to be scanned for potential triggers - only relevant for onBlocks
    fromBlock? : number;
    // the last block in the range to be scanned for potential triggers - only relevant for onBlocks
    toBlock? : number;
    // array of events matching the criteria - only relevant for onEvent
    events? : Event[];
}
 ```

upon runtime, the backend process invokes your task function with the parameters above.

As you can see, some of them are only relevant when bound to certain types of triggers. 

Example:

```js
// This task is planned to run on a time-based trigger
function myScheduledTask(web3, config) {
    // do hard work
}

// This task is planned to run on block ranges
function myBlocksTask(web3, config, fromBlock, toBlock) {
    // do hard work
}

// This task is planned to run on block ranges
function myEventsTask(web3, config, events) {
    // do hard work
}
```