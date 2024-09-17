# status.json

To support monitoring by the community, your service should maintain a local `status.json` file that shares its current status with the outside world. The contents of this file are publicly available from every node running the service via the [network status page](https://status.orbs.network).

The status file must be written in the path `./status/status.json` in order to conform with the protocol. Since working directory of the container is always `/opt/orbs`, the absolute path of the status file is `/opt/orbs/status/status.json`. It is recommended to update the file frequently, somewhere between every 30 seconds to 5 minutes.

## JSON format

```json
{
    "Error": "Ether balance is running low, current value 0.123 ETH",
    "Status": "EthSyncStatus = operational, VcSyncStatus = in-sync, EtherBalance = 0.123 ETH",
    "Timestamp": "2020-03-19T11:50:21.0846185Z",
    "Payload": {
        "Version": {
            "Semantic": "v1.3.1"
        },
        "CustomFieldsGoHere": 17,
        "MoreCustomFields": "any data type"
    },
    "Config": {
        "InputArg1": "value1",
        "InputArg2": "value2"
    }
}
```

* **Error** - Human readable explanation of current error. This field should exist only if the status is erroneous. Make sure to remove this field from the JSON in the event that the error has expired or there is no error. If error exists, the service will appear in yellow in the network status page.\

* **Status** - Human readable explanation of current status. This field always exists. It is recommended to return a short sentence with comma-separated values indicating key metrics.\

* **Timestamp** - The latest time when the status file was updated in [ISO](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Date/toISOString) format. Used by the network status page to verify that statuses are kept up-to-date.\

* **Payload.Version.Semantic** - The semantic version of the code that the container is running. Used for verifying that there were no image upgrade issues on different nodes.\

* **Config** - It is recommended to display all input arguments given to the container on startup in this map. This is used mostly for debugging purposes.

## Node.js script example

In this example the main container process is a Node.js script implemented in JavaScript that is updating the status file every few minutes. Since the working directory of the container is `/opt/orbs`, the container writes the file at `./status/status.json`:

```javascript
writeFileSync('./status/status.json', JSON.stringify(myStatus));
```
