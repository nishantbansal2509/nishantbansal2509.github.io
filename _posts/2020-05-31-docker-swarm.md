---
layout: post
title: Docker Swarm Commands
---

Docker Swarm is a container management utility provided with docker. It has commands which can help manage swarm of nodes running a pool of containers.

The docker CLI provides swarm functionalities as part of the management command `swarm`. It is a child command of `docker` and by default the swarm capabilities are disabled.

### `swarm`

The swarm command has sub commands which are primarily used for initializing a swarm, joining or leaving a swarm and  managing join tokens.

`docker swarm init` command initializes a node on your host which acts as a manager. This is the first command which should be invoked, as it is responsible for creating a swarm of nodes (arguably it creates __a__ node). The init command is responsible for security automation, creating certificates for manager, creating join tokens for other nodes to connect and initializing the Raft database which holds all the information about configs and secrets.

`docker swarm join-token (manager|worker)` command can be run on the manager nodes and outputs a `docker swarm join` command with a join token which can then be run on a new node in the network to connect it to the swarm.

`docker swarm join --token [TOKEN] [IP]` command can be run on any node to make it part of the swarm running at the supplied IP.

### `node`

The node command has sub commands which are primarily used for connecting or disconnecting a node to a swarm or promoting a worker node to a manager node or vice versa.

`docker node ls` command lists all the nodes which are part of the swarm along with their roles and availability. This command can only be run from a manager node in the swarm.

`docker node update [HOSTNAME]` command can be used to update node's role. The `--role` option defines the role which will be assigned to the host identified by the hostname.

### `service`

The service command has sub commands for managing service. This is like an alternative to the run command as in once a service is created it automatically ensures that the required number of containers are created and their lifecycle are controlled by the service.

`docker service create [IMAGE] [CMD]` command creates a new service based on the image passed on to it. The service is created and assigned a name based on the name option or an automatically assigned one. The containers are treated as "cattle" and are created with the service name followed by an instance number and a hash. This can be verified by running `docker container ls`. In case of a multi node swarm and `--replicas` option's value greater than one, the containers are automatically spawned on various nodes across the swarm.

`docker service ls` command lists all the services running in the swarm. The output also has the replica information which is essentially a count of containers running versus the target number of containers needed for that service.

`docker service ps [SERVICE]` command lists the tasks or containers running as part of that particular service.

`docker service update [SERVICE]` command helps updating the service supplied by the name.

1. The `--replicas` option is used to scale up the desired number of containers for that particular service. Additional containers will be spawned or deleted depending on whether its a scale up or scale down.
