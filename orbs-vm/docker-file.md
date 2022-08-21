# Dockerfile

First thing you need to do is to "dockerise" your app
If it is already "dockerised", there are some few changed you'll need to support.

## Example
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

- This dockerfile describes a common nodejs application
- The only two changes your ORBS-VM docker has to consider is WOKDIR and HEALTHCHECK