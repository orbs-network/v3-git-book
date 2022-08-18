# HEALTHCHECK

consider this line described in the [dockerfile](./docker-file.md)

```HEALTHCHECK CMD /opt/orbs/healthcheck``` 

- the ORBS-NODE orchestrator runs this process in order to determined if your orbs-vm instance is healthy.
- A common way in orbs services and ORBS-VMs to determined a container's health, is to access its ```/op/orbs/status.json``` (explain in details here) and make sure its not stale (has been updated in recent few minutes for instance...)

## HEALTHCHECK example
let us write a simple check based o the existence of a status.json and its "uptime" field's recency.

1. create ```healthechek/healthechek.sh``` shell file containing the following
```bash
#!/bin/sh
node ./healthcheck.js
```
As long as the execution of this bash returns status code 0, the container is healthy. 
2. create ```healthecheck.js``` file with the health implementations:
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
3. install HEALTHCHECK In dockerfile
```dockerfile
...
# install healthcheck based on status.json
COPY ./healthcheck.sh ./
COPY ./healthcheck.js ./
HEALTHCHECK CMD /opt/orbs/healthcheck.sh
...
```

4. build your docker file - and now your VM is good to go on orbs v3!

> Please notice that the healthcheck in the example, relays on your VM to write a valid json file to ./status/status.json in the container/ read more about this [here](./status.md)

legacy orbs-v2 service installation spec can be found [here](https://github.com/orbs-network/orbs-spec/blob/ee181179ddf8ee57dc0b2bd1197a1b91054edd64/node-architecture/BOYAR.md)