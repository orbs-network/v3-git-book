## WOKDIR
```WORKDIR /opt/orbs``` 
Its best to set your container to use this **workdir** for the sake of unity and order with other services and vms. The orchestrator than mounts this folder to a corresponding folder at the host machine.

Read more about [HEALTHCHECK](./health-check.md) and [Status](./status.md) 