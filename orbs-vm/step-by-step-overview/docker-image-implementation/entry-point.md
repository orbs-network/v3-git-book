# Entry Point

The executable inside your container that is launched by the orchestrator is `/opt/orbs/service` - this file must exist and must be executable. Failing to provide this file will prevent your container from starting.

## Shell script example

This example will use the shell script `entrypoint.sh` to run the primary process of your service. Let's assume the service is implemented with Node.js and starts with the command `npm start`.&#x20;

Create the file `entrypoint.sh` in the root of the image with the following content:

```shell
#!/bin/sh
npm start
```

Then, in your Dockerfile, copy this script over the required name:

```docker
# install entry point executable
COPY ./entrypoint.sh /opt/orbs/service
```
