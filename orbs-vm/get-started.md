# ORBS-VM Get Started 
All docker images can run on orbs network, but they need to be slightly adjusted to be able to run smoothly on the network.

## Docker image Prerequistis and Specs and Best Practice

### CPU architecture
- Currently all ORBS permissionless nodes are running on x64-86 cpu architecture platforms
- Make sure you build your docker image to support this architecture for the least

### Storage 
- Orbs nodes are not designed to support big disk with big of data storage.
- Most of ORBS nodes are 50-100 GB Disk size.
- If you Docker container is going to use lots of disk space, ORBS-VM might not be the right choice.

### Load and CPU consumption
- Make your Docker image app as moderate cpu consumer as possible as your instance shares CPU time iwth ORBS core containers and other ORBS-VM instances.
- Try to design your app to perform actions periodically in order to yield cpu consumption between executions.
- Avoid long computation loops and actions which may take cpu time for human notable periods.
- Avoid heavy IO operations that make take too long e.g writing and loading Huge JSON files to disk. 

### orchestration

### contract with swarm

### communication and ports

It should maintain a [dockerfile HEALTHCHECK](https://docs.docker.com/engine/reference/builder/) and may benefit from orbs [status page](http://status.orbs.network), with its own representation, if maintains a status.json file according to a certain format.





