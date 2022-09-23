# Working Directory

```dockerfile
FROM node:16-alpine

# standard working directory
WORKDIR /opt/orbs
```

`WORKDIR /opt/orbs`

* It is mandatory to set your container to use this **WORKDIR** for the sake of unity and order, so that your requirements will be the same as the requirements of other services and ORBS-VMs. The orchestrator mounts this folder to a corresponding folder at the host machine for the sake of exporting status and logs via HTTP.

Read more about [HEALTHCHECK](health-check.md) and [Status](status.md)
