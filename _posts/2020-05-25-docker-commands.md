---
layout: post
title: Docker Commands
---

The container world is changing rapidly. Its irksome to lookup documentation every time I need to use a command. This is a reference for me to take a quick glance at the most commonly used docker commands.

The `docker` commands are hierarchial. `docker` is the root of the hierarchy. These commands are classified based on their usage into sub commands. Docker calls `docker`'s child commands as __management__ commands. For instance, the `image` command is `docker`'s child and a management command. These management commands are invoked by appending them after `docker`. The `image` command will be executed like `docker image` followed by `image`'s sub command.

After the command hierarchy, flags and parameters are passed just like any other command.

## `version`

Every time a shell is fired, run this command to check whether docker is installed and what's the version. The `docker version` command will simply list the version of the docker. The client is corresponding to the docker cli version and server is corresponding to the docker engine running on the machine.

## `info`

The `docker info` command gives a more detailed view of configuration of docker engine.

## `container`

`docker container run --publish 80:80 --detach --name webhost nginx` command does several things on the host machine.

1. Locates the nginx file. If its not found locally docker will download it from hub.
2. Spawns a container running inside docker engine from the nginx image.
3. The publish provides the port information. The left port or the host port is the port on machine whose traffic is forwarded to the right port or the container port.
4. `--detach` flag runs the container and returns back to shell and returns the container id. The detach flag actually sets certain properties in the container so that when its restarted using `start` it will abide by those properties.
5. `--name` parameter supplies the name for the container.

`docker container ls` command lists all the containers running in the docker engine. If `-a` flag is attached, stopped containers are also displayed.

`docker container stop [ID/NAME]` command stops the container with the supplied container id or name. Only first few characters which can uniquely identify the container are required.

`docker container logs [ID/NAME]` command displays the recent logs from the particular container.

`docker container top [ID/NAME]` command lists the processes running within the container.

`docker container rm [ID/NAME]` command deletes the container if its stopped. If -f flag is attached, the container is forcefully deleted.

`docker container inspect [ID/NAME]` command low level information about the particular container.

`docker container stats` command list the container(s) resource usage statistics. Optionally a container id or name can be supplied to monitor that container's resource usage.

`docker container exec -ti [ID/NAME] [COMMAND]` runs the command in the supplied container. The -t flag gives a TTY while -i flag gives an interactive environment.

`docker container port [ID/NAME]` command lists the networking port being used at the host and the container.

## `network`

`docker network ls` command lists all the networks which have been created.

1. The bridge is the default docker virtual network which is NATed behind the host IP.
2. The host network is the machine's default network interface. A container can be directly connected to host network but it will sacrifice the container security.

`docker network inspect [ID/NAME] --format [GOTEMPLATE]` command displays detailed information about the network in a json object. This command also supports a format option where a go template can be supplied to parse the json object.

1. The json object contains the list of containers attached to that network. The corresponding template option is `--format '{{ "{{ .Containers " }}}}'`.

`docker network create` command cerates a new virtual network. The default driver used is bridge. The IP range is incremented as more virtual networks are added. A container can be added to a subnet while creating it and specifying the `--network` option.

`docker network connect [NETWORK] [CONTAINER]` command connects the container to the network supplied. An IP address is assigned to the container on the network. A container can be part of multiple networks and a NIC is created for each new network container is part of.

`docker network disconnect [NETWORK] [CONTAINER]` command disconnects the container from the supplied network.

## `image`

`docker image ls` lists all the image present locally along with some information on version and size.

`docker image pull [IMAGE]` pulls the latest image of the supplied project.

`docker image history [IMAGE]` command lists the layered history of image with summary of changes at each layer.

`docker image inspect [IMAGE]` command gives the details of the image stored in the local system. This only works for a image that has already been pulled from the repository. Just like any other `inspect` command, it spits out json and supports go templates via the `--format` option.

`docker image tag [SOURCE:TAG] [TARGET:TAG]` command creates a new image with the target identifier and respective tag from the source image.

`docker image push [IMAGE:TAG]` command pushes an image onto a remote docker repository along with the tags. The repository configured can be viewed in the $HOME/.docker/config.json file. This command won't work until the user is logged in using the `docker login` command. To logout the command is `docker logout`.

`docker image build -t [IMAGE:TAG] [DOCKERFILE]` command builds an image from the docker file supplied and assigns it the tags provided by the `-t` option. The `-f` option can be used to pass a custom docker file. By default docker builds image from $PATH/Dockerfile.

`docker image rm [IMAGE]` command removes an image from the local repository.

`docker image prune` command removes all the dangling images from the repository. `-f` flag forces deletion without confirmation. `-a` flag removes all unused images.

## `volume`

The `docker container run` can create a volume if `VOLUME` is used in the Dockerfile or a volume is supplied using the `-v` flag while creating the container. So if the volume option is not used but Dockerfile has one, volume will be created. If the volume option is passed as well as the Dockerfile has `VOLUME` two volumes will be created. If the path passes with `-v` option is same aas that in Dockerfile only one volume will be created. Also optionally in the run command `-v` flag can contain a name followed by `:` and path to create a named volume.

`docker volume ls` command to list all the volumes present.

`docker volume prune` command will delete all the unused volumes d=from the host machine.

`docker volume create` command will create a volume which can then be linked to a container while creating it by using `-v` option. Although the container run command will automatically create a volume supplied by the `-v` option, the `create` command can help specify the driver and options for creating a volume.

## `system`

`docker system df` command lists the storage being used by docker on the host. The storage usage may belong to local images, volumes, containers or build cache.'

`docker system prune` command removes all the unused data. This does not include volumes as they are supposed to be persistent data store.

## Dockerfile

Each command forms a layer i.e. a set of operations carried out sequentially upon the base image to build the final image.

`FROM` specifies the base image upon which the new image will be built.

`ENV` specifies key value pairs which will be setup as environment variables.

`RUN` specifies the command to be ran upon the previous layer.

`EXPOSE` specifies the port to be exposed on the docker virtual network. This does not mean that when a container is run it will automatically forward to these ports. The forwarding needs to be controlled by the `-p` option while running the container.

`CMD` specifies the command which will run when a container from the image is deployed.

`WORKDIR` changes directory within the container.

`VOLUME` specifies a path where a persistent data in form of a volume is created any time a container is spawned. This volume's lifecycle is not dependent on the container and once the container is cleaned the volume still exists and can be reattached to another container.
