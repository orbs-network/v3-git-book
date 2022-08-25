# onBlocks

This trigger runs on consecutive block ranges and lets you apply your own logic on this range.

The interface is as follows:

```javascript
engine.onBlocks(
    fn, // function to execute
    network, // string representation of one of the supported networks
    config // key:value object
)
```
