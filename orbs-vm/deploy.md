# Deployment

Deployment of a new ORBS-VM is done using a git **pull request** in the [orbs mainnet deployment repo](https://github.com/orbs-network/mainnet-deployment/blob/main/mainnet.json)

## Build docker image

Now that your Dapp has healthcheck installed, uses the correct workdir, and writes status, you can use docker build and push to any docker registry.

> Before you execute docker push!, it is very important to tag your ORBS-VM docker image in the following format: `v{Major}.{Minor}.{Patch}`

### Example

Run the following commands in the `.Dockerfile` folder :

```bash
docker build -t example-docker-registry.io/vm-example .

docker tag example-docker-registry.io/vm-example example-docker-registry.io/vm-example:v1.0.0

docker push example-docker-registry.io/vm-example:v1.0.0
```

## mainnet.json

Consider the mainnet.json file:

```json
{
  "Desc": "Stable and Canary versions for Orbs network",
  "SchemaVersion": 1,
  "ImageVersions": {
    "management-service-bootstrap": {
      "image": "orbsnetwork/management-service:bootstrap",
      "comment": "for use by a node deployment/installation tool"
    },
    "management-service": {
      "image": "orbsnetwork/management-service:v2.2.1"
    },
    "matic-reader": {
      "image": "orbsnetwork/management-service:v2.1.0"
    },
    "node": {
      "image": "orbsnetwork/node:v2.0.15"
    },
    "node-canary": {
      "image": "orbsnetwork/node:v2.0.15"
    },
    "signer": {
      "image": "orbsnetwork/signer:v2.4.0"
    },
    "ethereum-writer": {
      "image": "orbsnetwork/ethereum-writer:v1.3.0"
    },
    "matic-writer": {
      "image": "orbsnetwork/ethereum-writer:v1.3.0"
    },
    "logs-service": {
      "image": "orbsnetwork/logs-service:v1.1.4"
    },
    "vm-notifications": {
      "image": "orbsnetwork/vm-notifications:v1.0.2"
    },
    "vm-keepers": {
      "image": "orbsnetwork/keepers:v1.0.1"
    }
  }
}
```

The above holds a description of an ORBS node's containers.

In this file, you can see many of the Orbs Network's core components, and two instances of ORBS-VM.

> Please note that all images are tagged in the format of `v{Major}.{Minor}.{Patch}`. This is crucial when an upgrade is taking place.

```json
{
    {...},
    "vm-notifications": {
      "image": "orbsnetwork/vm-notifications:v1.0.2"
    },
    "vm-keepers": {
        "image": "orbsnetwork/keepers:v1.0.1"
    }
}
```

* Now, let us add "vm-example"
  * Docker Image is hosted on some `example-docker-registry.io`
  * The container listens to `port 3333`
  * It has some configurable variables which are displayed in the VMs `status.json`

```json
{
    {...},
    "vm-notifications": {
      "image": "orbsnetwork/vm-notifications:v1.0.2"
    },
    "vm-keepers": {
        "image": "orbsnetwork/keepers:v1.0.1"
    },
     "vm-example": {
        "image": "example-docker-registry.io/vm-example:v1.0.0",
        "port": 3333,
        "config":{
            "any":"config",
            "may":"go",
            "here": "!"
        }
    }
}
```

Once the above has been added to the file, submit this change as a PR to the [repo](https://github.com/orbs-network/mainnet-deployment)

The Orbs core team will then:

1. Review the validity of the json.
2. Check that the registry and image exist.
3. Deploy to 0xStaging.
4. Monitor Health and performance for a few hours or days, depending on the complexity of your Dapp.
5. Contact you to review the Dapp's performance on 0xStaging.

Once these steps are complete, your ORBS-VM will deploy to the network

## Upgrade your ORBS-VM

Upgrade can be as simple as editing your entry in mainnet.json. For example:

```json
{
    {...},
    "vm-notifications": {
      "image": "orbsnetwork/vm-notifications:v1.0.2"
    },
    "vm-keepers": {
        "image": "orbsnetwork/keepers:v1.0.1"
    },
     "vm-example": {
        "image": "orbsnetwork/vm-example:v1.0.1",
        "port": 4444,
        "config":{
            "new":"config"            
        }
    }
}
```

In the above example you can see that all parts of the ORBS-VM descriptor can be updated

* Image version
* Port
* Config

> Please make sure that the docker image tag version is advanced, or an upgrade won't be able to take place!
