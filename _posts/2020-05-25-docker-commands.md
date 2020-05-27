---
layout: post
title: Docker Commands
---

The container world is changing rapidly. Its irksome to lookup documentation every time I need to use a command. This is a reference for me to take a quick glance whenever my memory acts up.

The `docker` commands are hierarchial. `docker` is the root of the hierarchy. These commands are classified based on their usage into sub commands. For instance, the `image` command is `docker`'s child. These child commands are invoked by appending them after their parent. The `image` command will be executed like `docker image` followed by `image`'s sub command.

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
4. `--detach` flag runs the container and returns back to shell and returns the container id.
5. `--name` parameter supplies the name for the container.

`docker container ls` command lists all the containers running in the docker engine. If `-a` flag is attached, stopped containers are also displayed.

`docker container stop <id/name>` command stops the container with the supplied container id or name. Only first few characters which can uniquely identify the container are required.

`docker container logs <id/name>` command displays the recent logs from the particular container.

`docker container top <id/name>` command lists the processes running within the container.

`docker container rm <id/name>` command deletes the container if its stopped. If -f flag is attached, the container is forcefully deleted.

`docker container inspect <id/name>` command low level information about the particular container.

`docker container stats` command list the container(s) resource usage statistics.
