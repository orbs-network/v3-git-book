# Health Check

To be a good citizen on the image orchestration protocol, your image must respond to [health check](https://docs.docker.com/engine/reference/builder/#healthcheck) queries. When an image fails to respond to health check with an appropriate exit code, it will be restarted. Images that fail to eventually start and reach a healthy state are at risk of non execution.

The standard health check mechanism for Docker involves specifying a command-line executable that returns exit code 0 if the container is healthy and a non-zero exit code if the container is unhealthy. This executable is executed by the system roughly every 30 seconds. If the executable returns a non-zero value 3 times in a row, the container will be restarted.

A possible practice is to use the health check executable to update the local [`status.json`](status.json.md) file with up-to-date information. Since this executable is polled continuously, this will make sure the status is always recent.

## Node.js script example

This example will use the shell script `healthcheck.sh` to run a JavaScript script using Node.js. In this example, we don't rely on the health check to update `status.json` - but the opposite - we assume that the container process is updating the status file continuously and the health check is going to verify that. The health check JavaScript script will parse the status file and if its last update timestamp is recent (up to 5 minutes ago), the health check will succeed.&#x20;

Create the file `healthcheck.sh` in the root of the image with the following content:

```shell
#!/bin/sh
node ./healthcheck.js
```

Then, in your Dockerfile, copy this script and use it for health check:

```docker
# install healthcheck based on status.json
COPY ./healthcheck.sh ./
COPY ./healthcheck.js ./
HEALTHCHECK CMD /opt/orbs/healthcheck.sh
```

And finally, implement the JavaScript script `healthcheck.js` in the root of the image:

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
