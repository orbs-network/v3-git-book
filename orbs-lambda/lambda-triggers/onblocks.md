# onBlocks

This trigger runs on consecutive block ranges and lets you apply your own logic on this range.

Interface:
```js
onBlocks(
    fn, // function to execute
    network, // string representation of one of the supported networks
    config // key:value object
)
```