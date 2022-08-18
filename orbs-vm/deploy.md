# ORBS-VM Deploy 
Deployment of a new ORBS_VM is done using a git **pull request** in [orbs mainnet deployment repo](https://github.com/orbs-network/mainnet-deployment/blob/main/mainnet.json)

## Build docker image
Now that your app has healthceck installed, uses the correct workdir, and writes status, you can use docker build, push to any docker registry

> Before docker push! its very important to tag your ORBS-VM docker image in the following format ```v{Major}.{Minor}.{Patch}```

### example 
In the ```.Dockerfile``` folder run the following commands:

```bash
docker build -t example-docker-registry.io/vm-example .

docker tag example-docker-registry.io/vm-example example-docker-registry.io/vm-example:v1.0.0

docker push example-docker-registry.io/vm-example:v1.0.0
```

## mainnet.json
let us consider mainnet.json
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

It holds a description of a ORBS node's containers

In this file you can see many orbs core components, and two instances of ORBS-VM

> Please notice all images are tagged in the format of ```v{Major}.{Minor}.{Patch}```. This is crucial when upgrade is taking place.

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

Now let us add "vm-example" which is hosted on some example docker repo, and listens on port 3333 with some configurable variables that
will be displayed in the VMs ```status.json``` page
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

Once has been added to the file, submit this change as a PR to the [repo](https://github.com/orbs-network/mainnet-deployment)

orbs core team then will:
1. Review the validity of the json.
2. Check the registry and image exist.
3. Deploy to 0xStaging.
4. Monitor Health and performance for a few hours or days, depending on complexity.
5. Contact you to be able to review its performance on 0xStaging.

Once everything is completed, you VM will deploy to the network

## Upgrade your ORBS-VM

Upgrade can be as simple as editing your entry in mainnet.json
e.g

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

In the example you can see all parts of the VM descriptor can be updated
- Image version
- Port
- Config

> Please make sure the docker image tag version is advanced or else, an upgrade wont take place! 