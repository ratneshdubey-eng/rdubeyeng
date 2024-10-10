# Docker Commands Cheat Sheet

A comprehensive cheat sheet for Docker commands, organized by categories to help you easily find and use commands for managing images, containers, volumes, networks, and more.

## Table of Contents
1. [System Information Commands](#system-information-commands)
2. [Container Management Commands](#container-management-commands)
3. [Image Management Commands](#image-management-commands)
4. [Network Management Commands](#network-management-commands)
5. [Volume Management Commands](#volume-management-commands)
6. [Docker Compose Commands](#docker-compose-commands)
7. [Docker System Management Commands](#docker-system-management-commands)
8. [Docker Security Commands](#docker-security-commands)
9. [Docker Swarm Commands](#docker-swarm-commands)

---

## System Information Commands

| Command | Description |
|---------|-------------|
| `docker --version` | Show Docker version information. |
| `docker info` | Display system-wide Docker information. |
| `docker system df` | Show Docker disk usage. |

---

## Container Management Commands

| Command | Description |
|---------|-------------|
| `docker ps` | List running containers. |
| `docker ps -a` | List all containers, including stopped ones. |
| `docker run <image>` | Run a new container from an image. |
| `docker run -d --name <container_name> <image>` | Run a container in detached mode with a specified name. |
| `docker start <container_id_or_name>` | Start a stopped container. |
| `docker stop <container_id_or_name>` | Stop a running container gracefully. |
| `docker kill <container_id_or_name>` | Force stop a running container. |
| `docker restart <container_id_or_name>` | Restart a running container. |
| `docker rm <container_id_or_name>` | Remove a stopped container. |
| `docker rm -f <container_id_or_name>` | Force remove a container. |
| `docker logs <container_id_or_name>` | Show logs for a container. |
| `docker exec -it <container_id_or_name> /bin/bash` | Run commands in a running container interactively. |
| `docker attach <container_id_or_name>` | Attach to a running container's terminal. |
| `docker rename <old_name> <new_name>` | Rename a Docker container. |
| `docker top <container_id_or_name>` | Display running processes in a container. |
| `docker inspect <container_id_or_name>` | Show detailed information about a container in JSON format. |
| `docker stats <container_id_or_name>` | Show real-time resource usage statistics for a container. |
| `docker cp <container_id_or_name>:<src_path> <dest_path>` | Copy files/folders between a container and the local filesystem. |
| `docker pause <container_id_or_name>` | Pause all processes in a container. |
| `docker unpause <container_id_or_name>` | Unpause a paused container. |

---

## Image Management Commands

| Command | Description |
|---------|-------------|
| `docker images` | List all images. |
| `docker pull <image>` | Pull an image from a Docker registry. |
| `docker build -t <image_name>:<tag> <path_to_dockerfile>` | Build a Docker image from a Dockerfile. |
| `docker rmi <image_id_or_name>` | Remove one or more images. |
| `docker tag <image_id_or_name> <new_image_name>:<new_tag>` | Tag an image to a new repository. |
| `docker push <image_name>:<tag>` | Push an image to a Docker registry. |
| `docker history <image_id_or_name>` | Show history of an image. |
| `docker save -o <filename.tar> <image_name>` | Save an image to a `.tar` archive. |
| `docker load -i <filename.tar>` | Load an image from a `.tar` archive. |
| `docker image prune` | Remove unused images. |

---

## Network Management Commands

| Command | Description |
|---------|-------------|
| `docker network ls` | List all networks. |
| `docker network create <network_name>` | Create a new network. |
| `docker network rm <network_name>` | Remove a specified network. |
| `docker network inspect <network_name>` | Show detailed information about a network. |
| `docker network connect <network_name> <container_name>` | Connect a container to a specified network. |
| `docker network disconnect <network_name> <container_name>` | Disconnect a container from a specified network. |

---

## Volume Management Commands

| Command | Description |
|---------|-------------|
| `docker volume ls` | List all volumes. |
| `docker volume create <volume_name>` | Create a new volume. |
| `docker volume rm <volume_name>` | Remove a specified volume. |
| `docker volume inspect <volume_name>` | Show detailed information about a volume. |
| `docker volume prune` | Remove all unused volumes. |

---

## Docker Compose Commands

| Command | Description |
|---------|-------------|
| `docker-compose up -d` | Start services defined in a `docker-compose.yml` file in detached mode. |
| `docker-compose down` | Stop and remove containers, networks, and volumes defined in a compose file. |
| `docker-compose ps` | List services defined in the compose file. |
| `docker-compose build` | Build or rebuild services defined in a compose file. |
| `docker-compose logs <service_name>` | Show logs for a specified service. |
| `docker-compose restart` | Restart services defined in a compose file. |

---

## Docker System Management Commands

| Command | Description |
|---------|-------------|
| `docker system prune` | Remove unused containers, networks, images, and build cache. |
| `docker system df` | Show Docker disk usage. |
| `docker system events` | Show real-time Docker events. |
| `docker update <container_id_or_name> --memory <value>` | Update container resource limits. |

---

## Docker Security Commands

| Command | Description |
|---------|-------------|
| `docker scan <image>` | Scan an image for vulnerabilities. |
| `docker trust inspect <image>` | Inspect signatures of a trusted image. |
| `docker trust sign <image>` | Sign an image using Docker Content Trust. |

---

## Docker Swarm Commands

| Command | Description |
|---------|-------------|
| `docker swarm init` | Initialize a new swarm. |
| `docker swarm join --token <token> <manager_ip>:<port>` | Join a node to an existing swarm. |
| `docker node ls` | List nodes in the swarm. |
| `docker service create --name <service_name> <image>` | Create a new service in the swarm. |
| `docker service ls` | List services in the swarm. |
| `docker service rm <service_name>` | Remove a service from the swarm. |
| `docker stack deploy -c <compose_file> <stack_name>` | Deploy a new stack using a compose file. |
| `docker stack rm <stack_name>` | Remove a stack. |

