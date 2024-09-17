# Working Directory

The working directory of your container is required to be `/opt/orbs` in order to conform with the protocol and allow the nodes to serve logs and status from the correct location. The orchestrator mounts this path explicitly.

You are allowed to create subdirectories inside this directory.

## Dockerfile example

The working directory should be defined in your Dockerfile like this:

```docker
# standard working directory
WORKDIR /opt/orbs
```
