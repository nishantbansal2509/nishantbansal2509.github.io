---
layout: post
title: Docker Commands
---

The container world is changing rapidly. Its hard to keep all the commands in memory. This is a refernce for me to take a quick glance whenever my memory acts up.

Another thing to keep in mind is the structure of the `docker` commands. Like a lot of command line utilities, `docker` commands form a heirarchy. `docker` is the root of the heirarchy. Then the commands are classified based on their usage into children commands. For instance, the `image` command is `docker`'s child. These child commands are invoked by appending them after their parent. The `image` command will be executed like `docker image` followed by `image`'s sub commands.

After the command heirarchy flags and parameters are passed just like any shell command.

1. `version`

    The `docker version` command will simply list the version of the docker.

    ```
    nishant@Nishants-MacBook-Air workdir % docker version
    Client: Docker Engine - Community
     Version:           19.03.8
     API version:       1.40
     Go version:        go1.12.17
     Git commit:        afacb8b
     Built:             Wed Mar 11 01:21:11 2020
     OS/Arch:           darwin/amd64
     Experimental:      false
    
    Server: Docker Engine - Community
     Engine:
      Version:          19.03.8
      API version:      1.40 (minimum version 1.12)
      Go version:       go1.12.17
      Git commit:       afacb8b
      Built:            Wed Mar 11 01:29:16 2020
      OS/Arch:          linux/amd64
      Experimental:     false
     containerd:
      Version:          v1.2.13
      GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
     runc:
      Version:          1.0.0-rc10
      GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
     docker-init:
      Version:          0.18.0
      GitCommit:        fec3683
    ```
