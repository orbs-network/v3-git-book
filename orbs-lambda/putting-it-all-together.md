# Project structure

Submitted projects should respect to following structure:

* A new dir with the project name, containing:
* index.js file
* Optional: additional files to be imported into index.js, such as config JSON, ABIs etc.

## index.js
This is the JS file containing the function(s) you wish to run on Orbs Lambda, as well as the triggers definitions.

### General structure

```js
// imports of local files and [supported dependencies]
const {conf} = require("./config.js");

// The task function you wish to run on Lambda, as well as other helper functions you wish to implement.
async function doHarkWork(web3, config) {
    web3.eth.sendTransaction({to: config.toAddress, value: web3.utils.toWei("1", "ether")} )
}

// A registeration function with binds between task functions and triggers
module.exports = function (engine) {
    engine.onSchedule(doHarkWork, "1d", 'ethereum', conf) // -> run doHarkWork every day on Ethereum network, with "conf" as configuration
}
```
That's it! This is the minimal format you need to follow in order to trigger your task whenever you wish!
