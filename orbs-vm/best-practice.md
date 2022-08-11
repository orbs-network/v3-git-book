# best practice

## intro
Not any docker image can run on an orbs node.
It must maintain a [dockerfile HEALTHCHECK](https://docs.docker.com/engine/reference/builder/) and may benefit from orbs [status page](http://status.orbs.network), with its own representation, if maintains a status.json file according to a certain format.

## Dockerfile best practice
consider a nodejs example of orbs-vm docker file:
```dockerfile
FROM node:16-alpine

# standard working directory
WORKDIR /opt/orbs

# install healthcheck based on status.json
COPY ./healthcheck.sh ./
COPY ./healthcheck.js ./
HEALTHCHECK CMD /opt/orbs/healthcheck.sh

# install your app
COPY package*.json ./
RUN npm install
COPY dist ./dist
CMD [ "npm", "start" ]
```

### WOKDIR
```WORKDIR /opt/orbs``` 
Its best to set your container to use this workdir for the sake of unity and order with other services and vms. The orchestrator than mounts this folder to a corseponding folder at t he host machine.

### HEALTHCHECK
```HEALTHCHECK CMD /opt/orbs/healthcheck``` 
the orchestrator runs this process in order to maintain if your orbs-vm instance is healthy.
A common way in orbs services and vm- to determind a container's health, is to access its ```/op/orbs/status.json``` (explain in details here) and make sure its not stale (has been updated in recent few minutes for instance...)

#### HEALTHCHECK example
let us write a simple check based o the existance of a status.json and its "uptime" field's recency.

1. create ```healthechek/healthechek.sh``` shell file containing the following
```bash
#!/bin/sh
node ./healthcheck.js
```
As long as the execution of this bash returns status code 0, the container is healthy. 
2. create ```healthecheck.js``` file with the health implementations:
```js
const fs = require('fs');

try {
  // read json file to JS Object
  const status = JSON.parse(fs.readFileSync('./status/status.json').toString());

  // check how many seconds ago since the file was written
  const updatedAgoSeconds = (new Date().getTime() - new Date(status.Timestamp).getTime()) / 1000;
  
  // return error in case it hasnt been written in the last 5 minutes
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

> Please notice that the healthcheck in the example, relayes on your VM to write a valid json file to ./status/status.json in the container/ read more about this [here](./status.md)

legacy orbs-v2 service installation spec can be found [here](https://github.com/orbs-network/orbs-spec/blob/ee181179ddf8ee57dc0b2bd1197a1b91054edd64/node-architecture/BOYAR.md)