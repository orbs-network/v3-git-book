# Entry point

Consider the following line described in the [dockerfile](../docker-file.md):

```dockerfile
COPY ./entrypoint.sh /opt/orbs/service
```

* The ORBS-NODE docker orchestrator runs this executable when an ORBS-VM instance is started.

> Running the executable at /opt/orbs/service is mandatory. If it is not run, the ORBS-VM container will not start. Please note that "service" is the name of the executable itself, and that is how the docker orchestrator starts the container.

## Entrypoint example

As an example, let's write a simple entry point bash executable, which starts a node process.

1. Create `entrypoint.sh` (sibling to Dockerfile) shell file containing the following:

```bash
#!/bin/sh
npm start
```

2.. Install Entrypoint in Dockerfile

```dockerfile
...
# install entry point executable
COPY ./entrypoint.sh /opt/orbs/service
...
```

3\. Continue to [HEALTHCHECK](health-check.md)

The legacy orbs-v2 service installation spec can be found [here](https://github.com/orbs-network/orbs-spec/blob/ee181179ddf8ee57dc0b2bd1197a1b91054edd64/node-architecture/BOYAR.md)
