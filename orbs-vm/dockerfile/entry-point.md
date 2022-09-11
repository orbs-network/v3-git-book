# Entrypoint

Consider this line described in the [dockerfile](../docker-file.md)

```dockerfile
COPY ./entrypoint.sh /opt/orbs/service
```

* The ORBS-NODE docker orchestrator runs this executable when ORBS-VM instance is started.

> executable at /opt/orbs/service is Mandatory otherwise, the ORBS-VM container wont start. Please note that "service" is the name of the executable itself and thats how docker orchestrator starts the container.

## Entrypoint example

Let's write a simple entry point bash executable which starts a node process.

1. Create `entrypoint.sh` (sibling to Dockerfile) shell file containing the following:

```bash
#!/bin/sh
npm start
```

3\. Install Entrypoint in Dockerfile

```dockerfile
...
# install entry point executable
COPY ./entrypoint.sh /opt/orbs/service
...
```

4. Continue to [HEALTHCHECK](./health-check.md)

legacy orbs-v2 service installation spec can be found [here](https://github.com/orbs-network/orbs-spec/blob/ee181179ddf8ee57dc0b2bd1197a1b91054edd64/node-architecture/BOYAR.md)
