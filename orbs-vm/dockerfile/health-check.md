# Health check

Consider this line described in the [dockerfile](../docker-file.md)

```dockerfile
COPY ./healthcheck.sh ./
COPY ./healthcheck.js ./
HEALTHCHECK CMD /opt/orbs/healthcheck.sh
```

* The ORBS-NODE orchestrator runs this process in order to determine if your ORBS-VM instance is healthy.
* A common method used by the Orbs Network's services, including ORBS-VMs, to determine a container's health, is to access its `/op/orbs/status/status.json` (explained in detail [here](../status.md)) and make sure it is not stale (i.e., that it hasn't been updated in recent few minutes).

> HEALTHCHECK is mandatory for your docker container to run on the Orbs Guardian nodes. Do not skip the following instructions.

## HEALTHCHECK example

For example, let's write a simple check based on the existence of a status.json and its "uptime" field's recency.

1. Create `healthechek.sh` (sibling to Dockerfile) shell file containing the following:

```bash
#!/bin/sh
node ./healthcheck.js
```

As long as the execution of this batch returns status code 0, the container is healthy.

2\. create `healthecheck.js` file with the following health implementations:

```javascript
const fs = require('fs');

try {
  // read json file to JS Object
  const status = JSON.parse(fs.readFileSync('./status/status.json').toString());

  // check how many seconds ago since the file was written
  const updatedAgoSeconds = (new Date().getTime() - new Date(status.Timestamp).getTime()) / 1000;
  
  // return error in case it hasn't been written in the last 5 minutes
  if (updatedAgoSeconds > 5 * 60) {
    console.log(`Timestamp was not updated in status.json for ${updatedAgoSeconds} seconds.`);
    process.exit(128);
  }
} catch (err) {
  // exception throws in the following cases:
  // - status/status.json does not exist
  // - status/status.json does not follow expected json format
  console.log(err.stack);
  process.exit(0); // don't restart in this case, maybe service isn't ready
}
// all good
process.exit(0);
```

3\. Install HEALTHCHECK In dockerfile

```dockerfile
...
# install healthcheck based on status.json
COPY ./healthcheck.sh ./
COPY ./healthcheck.js ./
HEALTHCHECK CMD /opt/orbs/healthcheck.sh
...
```

4\. Build your docker file - now your VM is good to go on Orbs v3!

> Please notice that the healthcheck in the example, relays on your VM to write a valid json file to ./status/status.json in the container/ read more about this [here](status.md)

The legacy orbs-v2 service installation spec can be found [here](https://github.com/orbs-network/orbs-spec/blob/ee181179ddf8ee57dc0b2bd1197a1b91054edd64/node-architecture/BOYAR.md)
