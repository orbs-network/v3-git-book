# index.js Implementation

The file `index.js` that is found in the top-level directory of your unique ID is the main entry point of your lambda function. This file should contain the majority of your JavaScript logic.

### Mandatory exports

The file must export in [CommonJs format](https://nodejs.org/docs/latest/api/modules.html#moduleexports) the function `register` which registers the [execution triggers](execution-triggers.md) that the lambda function is listening on.

```javascript
module.exports.register = function(engine) {
  // register all triggers here
}
```

### Importing dependencies

The file may import additional `.js` and `.json` dependencies that must be found in the same directory as the file `index.js` itself (or under a subdirectory next to it).

Importing must use the [CommonJs](https://nodejs.org/docs/latest/api/modules.html#requireid) `require()` syntax.

NPM packages may also be imported, subject to being in the [allowed list](allowed-packages.md).

```javascript
const { ContractAbi } = require("./abi.js");

const Config = require("./config.json");

const BigNumber = require("bignumber.js");
```

### Async await

Asynchronous code can and should use the modern `async await` syntax directly.

```javascript
async function doSomething(web3) {
  const contract = new web3.eth.Contract(abi, address);
  const res = await contract.methods.readState();
}
```

## Complete example

The following example monitors an [Aave](https://aave.com/) borrowing position every 10 minutes and if the position is close to liquidation, closes it using a contract that was deployed in advance for this lambda.

```javascript
const BigNumber = require("bignumber.js");

// config
const aaveAbi = [{/* ... */}];
const closingAbi = [{/* ... */}];
const positionAddress = "0xe93C0f419AF19297D320563214Adbb2f28EF4C0c";

// globals
let aaveContract; // the standard Aave contract
let closingContract; // contract for closing Aave positions, deployed for this lambda

async function checkAavePosition(args) {
  if (!aaveContract) aaveContract = new args.web3.eth.Contract(aaveAbi, "0x7d2768dE32b0b80b7a3454c06BdAc94A69DDc7A9");
  if (!closingContract) closingContract = new args.web3.eth.Contract(aaveAbi, "0xBB51bD166d68c3DC5860190844Dfe1056Cea3122");
  const position = await aaveContract.methods.getPositionData(positionAddress).call();
  if (new BigNumber(position.healthFactor).dividedBy("1e18").toNumber() < 1.05) {
    await closingContract.methods.closePosition(positionAddress).send();
  }
}

module.exports.register = function(engine) {
  engine.onInterval(checkAavePosition, {
    interval: "10m", 
    network: "ethereum"
  });
}
```
