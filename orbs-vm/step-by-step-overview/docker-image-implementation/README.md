# Docker Image Implementation

Any standard Docker image can be executed on the Orbs Network. The image must adhere to certain requirements to support efficient orchestration by the protocol.

## Dockerfile

The most important part of a Docker image is the [Dockerfile](https://docs.docker.com/engine/reference/builder/). Orbs VM supports the standard file format as interpreted by orchestrators like [Docker Swarm](https://docs.docker.com/engine/swarm/).

### Best practices

To make sure your image as efficient as possible, be sure to follow the [best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile\_best-practices/). It is recommended to base your docker image on the official [Alpine Linux](https://hub.docker.com/\_/alpine).

### Health check and status

To be a good citizen on the image orchestration protocol, your image must respond to [health check](https://docs.docker.com/engine/reference/builder/#healthcheck) queries. When an image fails to respond to health check with an appropriate exit code, it will be restarted. Images that fail to eventually start and reach a healthy state are at risk of non execution.

To support monitoring by the community, your service should maintain a local [`status.json`](status.json.md) file that shares its current status with the outside world. The contents of this file are publicly available from every node running the service via the [network status page](https://status.orbs.network).

## Complete example

The following Dockerfile example creates a Node.js service based on Alpine Linux. The service uses a shell script that executes a Node.js script for performing the health check and updating `status.json` periodically.

```docker
FROM node:16-alpine

# standard working directory
WORKDIR /opt/orbs

# install your app
COPY package*.json ./
RUN npm install
COPY dist ./dist
CMD [ "npm", "start" ]

# install healthcheck based on status.json
COPY ./healthcheck.sh ./
COPY ./healthcheck.js ./
HEALTHCHECK CMD /opt/orbs/healthcheck.sh

# install entry point executable
COPY ./entrypoint.sh /opt/orbs/service
```
