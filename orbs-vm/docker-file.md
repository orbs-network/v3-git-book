# Dockerfile

The first thing you will need to do is to "dockerize" your Dapp. Once your Dapp has been "dockerized", there are a few additional changes you will need to implement.

## Example

Consider a nodejs example of ORBS-VM docker file:

```dockerfile
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

* This dockerfile describes a common nodejs application
* In this case, the only two changes your ORBS-VM docker is required to contain are: WOKDIR and HEALTHCHECK.
