# Dockerfile

First thing you need to do is to "dockerise" your app
If it is already "dockerised", there are some few changed you'll need to support.

## example
Consider a nodejs example of orbs-vm docker file:
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

## WOKDIR
```WORKDIR /opt/orbs``` 
Its best to set your container to use this **workdir** for the sake of unity and order with other services and vms. The orchestrator than mounts this folder to a corresponding folder at the host machine.

Read more about [HEALTHCHECK](./health-check.md) and [Status](./status.md) 