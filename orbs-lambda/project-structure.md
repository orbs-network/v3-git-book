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
const abi = require('./abi.js')

// TODO - contract 

// The task functions you wish to run on Lambda, as well as other helper functions you may implement.
async function myScheduledTask(web3, config) {
    web3.eth.sendTransaction({to: config.toAddress, value: web3.utils.toWei("1", "ether")} )
}

async function myEventTask(web3, config, event) {
    console.log("Event emitted!", event)
}

// A registeration function with binds between task functions and triggers
module.exports.register = function (engine) {
    engine.onSchedule(myScheduledTask, "1d", 'ethereum', conf) // -> run myScheduledTask every day on Ethereum network, with "conf" as configuration
    engine.onEvent(myEventsTask, myContract, ["event1", "event2"], 'polygon', conf) // -> run myEventTask whenwver event1 or event2 on myContract are emitted
}
```


That's it! This is the minimal format you need to follow in order to trigger your tasks however you wish!
