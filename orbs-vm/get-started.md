# Get started

Any docker image can be run on the Orbs Network. However, they may require some slight adjustments in order to allow them to be able to run smoothly on the network.

## Docker image Specs

### CPU architecture

* Currently all of the Orbs Network's permissionless Guardian nodes run on x64-86 cpu architecture platforms
* Therefore, you should ensure that your docker image can, at minimum, support this architecture.&#x20;

### Storage

* Orbs Guardian nodes are not designed to support large disks requiring high levels of data storage.
* Most Orbs Guardian nodes are 50-100 GB Disk size.
* If you expect that your docker container will require a large amount of disk space, ORBS-VM might not be the right choice for your application.

### Load and CPU consumption

* To the extent possible, configure your Docker image app so that it will consume a moderate amount of CPU. Keep in mind that your instance shares CPU time with both the Orbs Network's core containers and other ORBS-VM instances.
* Try to design your app to perform actions periodically in order to yield CPU consumption between executions.
* Avoid long computation loops and actions which may take CPU time for human notable periods.
* Avoid heavy IO operations that may take a long time to process (e.g writing and loading large JSON files to disk).

### Communication and ports

* Should your ORBS-VM listens on a container port that needs to be mapped to the host node, it needs to be specidied during [deployment](deploy.md)

### Sign transactions

* If your ORBS-VM application needs to be able to sign Web3 transactions, this function can be added using the Node's Signer. This must be specified during [deployment](deploy.md).
* More on the Orbs node signer service can be found [here](https://github.com/orbs-network/signer-service).

### Orchestration in Docker swarm environment

* Orbs Guardian nodes run docker swarm. They also run a process which utilizes swarm in order to orchestrate the Orbs Network's core components, as well as Dapps utilizing ORBS-VM. For your container to run smoothly, you will need to implement the following:
  * Maintain a [dockerfile HEALTHCHECK](https://docs.docker.com/engine/reference/builder/)
  * Benefit from the Orbs [status page](http://status.orbs.network), with its own representation, if maintains a status.json file according to a certain format.

Click to read more about ORBS-VM [Healthcheck](health-check.md) and [Status](status.md)
