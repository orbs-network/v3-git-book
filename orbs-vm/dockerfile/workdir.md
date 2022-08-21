# WOKDIR

```dockerfile
FROM node:16-alpine

# standard working directory
WORKDIR /opt/orbs
```

```WORKDIR /opt/orbs``` 

- Its mandatory to set your container to use this **WORKDIR** for the sake of unity and order same as other other services and ORBS-VMs. The orchestrator would mounts this folder to a corresponding folder at the host machine for the sake of exporting status and logs via HTTP.

Read more about [HEALTHCHECK](./health-check.md) and [Status](./status.md) 