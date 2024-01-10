# Most used docker commands

1. **Managing Images**
   - `docker pull [image]`: Download an image from a registry (like Docker Hub).
   - `docker build -t [tag] .`: Build an image from a Dockerfile in the current directory.
   - `docker images`: List all images on your system.
   - `docker rmi [image]`: Remove an image.

2. **Running Containers**
   - `docker run [options] [image] [command]`: Create and start a container. Common options include `-d` for detached mode, `-p` for port mapping, and `--name` to name the container.
   - `docker ps`: List running containers. Use `-a` to show all containers.
   - `docker stop [container]`: Stop a running container.
   - `docker start [container]`: Start a stopped container.
   - `docker restart [container]`: Restart a container.
   - `docker rm [container]`: Remove a stopped container.

3. **Interacting with Running Containers**
   - `docker exec -it [container] [command]`: Run a command in a running container, often used to open a shell with `/bin/bash` or `/bin/sh`.
   - `docker logs [container]`: Fetch the logs of a container.

4. **Data Management**
   - `docker volume create [name]`: Create a volume.
   - `docker volume ls`: List all volumes.
   - `docker volume rm [volume]`: Remove a volume.

5. **Networking**
   - `docker network ls`: List networks.
   - `docker network create [options] [name]`: Create a network.
   - `docker network rm [network]`: Remove a network.

6. **Image and Container Inspection**
   - `docker inspect [container/image]`: Get detailed information about a container or image.
   - `docker stats`: Display a live stream of container(s) resource usage statistics.

7. **Tagging and Pushing to Repositories**
   - `docker tag [image] [repository:tag]`: Tag an image for a repository.
   - `docker push [repository:tag]`: Push an image to a remote repository.

These commands are fundamental for daily Docker tasks like managing containers and images, setting up networks, handling volumes for persistent storage, and more. While Docker has many more specialized commands and options, familiarity with these should enable you to handle a vast majority of typical Docker use cases.
