# onEvent

Listen to on-chain events and trigger your function whenever these are emitted.

Interface:
```js
onEvent(
    fn, // function to execute
    contract, // web3 contract object (https://web3js.readthedocs.io/en/v1.2.11/web3-eth-contract.html#web3-eth-contract)
    eventNames, // array of the contract's event names you wish to listen to
    network, // string representation of one of the supported networks
    config // key:value object
)
```