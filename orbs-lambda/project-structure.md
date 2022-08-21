# Project structure

Submitted projects should respect to following structure:

* A new dir under `projects` named after your project, containing:
* `index.js`: consists of 2 mandatory parts - task function(s) and exported `register` function, containing the triggers (see below).
* Optional: additional files to be imported into index.js, such as config JSON, ABIs etc.


```
v3-orbs-lambda/
├─ projects/
│  ├─ myCoolProject/
│  │  ├─ index.js
│  │  ├─ abis.js
│  │  ├─ config.js
│  ├─ myAwesomeProject/
│  │  ├─ index.js
│  │  ├─ conf.json

```
## index.js
This is the JS file containing the function(s) you wish to run on Orbs Lambda, as well as the triggers definitions.

### General structure

```javascript
// imports of local files and [supported dependencies]
const {conf} = require("./config.js");
const abi = require('./abi.js') // [{"inputs":[...]...}...]

// The task functions you wish to run on Lambda, as well as other helper functions you may implement.
async function myScheduledTask(web3, storage, guardians, config) {
    const contract = new web3.eth.Contract(abi, config.contractAddress)
    contract.methods.myMethod(config.methodParams).send()
}

async function myEventTask(web3, storage, guardians, config, event) {
    console.log("Event emitted!", event)
    const sender = web3.eth.abi.decodeParameter('address', event.topics[1]);
    if (guardians.include(sender)) storage.set(new Date().getTime(), event) // save the event in local storage if it was emitted by one of Orbs guardians
}

// A registration function with binds between task functions and triggers
module.exports.register = function (engine) {
    // run myScheduledTask every day on Ethereum network, with "conf" as configuration
    engine.onSchedule(myScheduledTask, "1d", 'ethereum', conf)
    // run myEventTask whenever event1 or event2 on myContract are emitted
    engine.onEvent(myEventsTask, myContractAddress, abi, ["event1", "event2"], 'polygon', conf)
}
```
That's it! This is the minimal format you need to follow in order to trigger your tasks however you wish!
