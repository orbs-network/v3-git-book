# Status

## introduction

<img src="../.gitbook/assets/status.png" alt="" data-size="original">

* All docker containers on each Orbs Guardian node are monitored by the [orbs status page](https://status.orbs.network/).
* Each ORBS-VM gets its own visual representation according to the `status.json` exported by the ORBS-VM.
* Your ORBS-VM should write its own `/status/status.json` (container's path) every 5 minutes in order to be monitored and for the HEALTHCHECK ([described here](best-practice.md)) to work properly.

## json format

```json
{
    "Error": "Human readable explanation of current error, field exists only if the status is erroneous.",
    "Status": "Human readable explanation of current status, field always exists.",
    "Timestamp": "2020-03-19T11:50:21.0846185Z",
    "Payload": {
        "Version": {
            "Semantic": "v1.3.1"
        },
        "CustomFieldsGoHere": 17,
        "MoreCustomFields": "any data type"
    },
    "config":{...}
}
```

### Error

* Human readable explanation of current error, field exists only if the status is erroneous.
* Make sure to remove this field from the json in the event that the error has expired or is not informative
* Upon an error, the status page responds in yellow color for the ORBS-VM representation box and shows text about the error.

### Status

* Human readable explanation of current status; this field always exists.

### Timestamp

* Shows the latest write time of the file
* Used by status to determined validity of a ORBS-VM status

### Payload.Version.Semantic

* Shows which ORBS-VM version is running, and on which node.

### config

* It is advised to export whatever external config is used by the ORBS-VM instance for debug and monitoring purposes.

## json folder

Since the working folder of the ORBS-VM is `/opt/orbs,` the fill path of the status, in the container's terms is `/opt/orbs/status/status.json`

In your code, you should simply write to `./status/status.json`

e.g

```js
    writeFileSync('./status/status.json', JSON.stringify(myStatus));
```

> Noe that once status is implemented, you should make sure your HEALTHCECK manages to read it properly and calculate it's recency in the **Timestamp** field

The legacy orbs-v2  service can be found [here](https://github.com/orbs-network/orbs-spec/blob/ee181179ddf8ee57dc0b2bd1197a1b91054edd64/node-architecture/BOYAR.md)
