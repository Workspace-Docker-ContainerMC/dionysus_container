## Docker container JDK with Dionysus ##
### About container: ###

This container is based on [ubi9-minimal](https://hub.docker.com/r/redhat/ubi9-minimal), and uses [graalvm-ce 17 JDK](https://www.graalvm.org).
The container is built specifically for use as a minecraft server. [This issues](https://github.com/graalvm/container/issues/73) has been fixed in it.
This allows you to fully use it as a server container without errors related to some plugins.

All builds take place automatically without human intervention.

### About configuration: ###

In ```entrypoint.sh``` the start [flags](https://docs.papermc.io/paper/aikars-flags) from Aikar's are specified. You can get them by following the link or on [this website](https://flags.sh/). ```entrypoint.sh``` it has one variable - ```MEMORYSIZE```, which indicates how much will be allocated memory to the server (in this case, velocity) in -Xms and -Xmx. It is located [here](https://github.com/Workspace-Docker-ContainerMC/dionysus_container/blob/18ff9a55b86c509063299d5c05068f6695712040/entrypoint.sh#L19).

**It is important!** If you limit the container's memory using ``--memory`` in the docker command, or ``memory`` in ``docker-compose``, keep in mind that you need to allocate memory with a margin. If you specified 1G in MEMORYSIZE, then you need to specify at least 2G for the docker container.If you specify less, the JVM uses all the RAM, and your process will be stopped by OOMKiller. Multiply your allocated memory number by 2-3. This will help to avoid problems with stopping the container.

**If you need to change the JDK or flags,** you need to create the container yourself. You can find out how to do this in the how to [build section](https://github.com/Workspace-Docker-ContainerMC/dionysus_container?tab=readme-ov-file#build).

## Download ##
### How to download ###

Get docker image you can take [here](https://hub.docker.com/r/workspacedockermc/el9-java17-dionysus-1.12.2)

Get the latest version сontainer:
```bash
docker pull workspacedockermc/el9-java17-dionysus-1.12.2:latest
```

## Use ##
### How to use ###
You can run container with the docker command:
```
docker run --detach --name=main --interactive \
    --tty --restart=unless-stopped --env MEMORYSIZE=2G \
    --cpus=2 --memory 5G --volume /home/$USER/server/main:/main:rw,Z \
    docker.io/workspacedockermc/el9-java17-dionysus-1.12.2:latest
```

Or use [this](https://github.com/WolfAURman/minecraft_containers/tree/master/compose-files) docker-composes files:
```
docker-compose -f <NAME_DOCKER_COMPOSE_FILES> up -d
```

## Build ##
### How to build ###
Clone repo
```bash
git clone https://github.com/Workspace-Docker-ContainerMC/dionysus_container
```

Go to directory
```bash
cd dionysus_container
```

Get started build
```bash
docker build -t docker.io/$USER/el9-java17-dionysus-1.12.2:latest .
```

## Contributer's & Credit's ##
### I express my gratitude to these projects: ###
- [Red Hat](https://github.com/RedHatOfficial)
- [GraalVM](https://github.com/graalvm)
- [Docker](https://docker.com)