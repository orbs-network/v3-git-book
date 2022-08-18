# onEvent

Listen to on-chain events and trigger your function whenever these are emitted.

Interface:
```javascript
engine.onEvent(
    fn, // function to execute
    contractAddress, // smart contract address
    abi, // Application Binary Interface (ABI) for an Ethereum smart contract. (array)
    eventNames, // array of the contract's event names you wish to listen to
    network, // string representation of one of the supported networks
    config // your custom configuration. key:value object
)
```