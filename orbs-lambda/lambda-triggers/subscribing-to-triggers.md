# Subscribing to triggers
In order to subscribe to one or more of the triggers above, one must implement and export a "register" function.

```js
module.exports.register = function (engine) {
    engine.onSchedule(myEthTask, "0 0 * * 1", 'ethereum', configEth)
    engine.onSchedule(myPolygonTask, "12h", 'polygon', configPolygon)
    engine.onBlocks(....)
```

In the above example, after implementing `myEthTask` and `myPolygonTask` functions, we bind them to trigger handlers.
- Don't worry about the `engine` object. It is provided by the backend process on run-time.
- You may bind each of your task functions to one or more handlers. This gives you the flexibility, for example, to run the same task on different networks with different configuration.