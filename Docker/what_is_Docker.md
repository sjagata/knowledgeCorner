
# What is Docker?

Docker is an open-source platform that automates the deployment, scaling, and management of applications using containerization. It allows developers to package applications and their dependencies into containers, ensuring consistency across different environments.

| Component         | Description                                      |
|--------------------|--------------------------------------------------|
| Docker Engine      | The core component that runs and manages containers. |
| Docker Hub         | A cloud-based repository for sharing Docker images.  |
| Docker Compose     | A tool for defining and running multi-container Docker applications. |
| Docker Swarm       | A native clustering and orchestration tool for managing a cluster of Docker engines. |
| Docker Desktop     | A desktop application that provides an easy-to-use interface for managing Docker containers. |
| Docker CLI         | The command-line interface to interact with Docker and its components. |

## Docker Image
A Docker image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, and environment variables. Images are read-only and serve as the blueprint for creating containers.

An Image is a single file with all dependencies and configurations that are required to run a program or application.

| File System Snapshot                          | Startup Command(s)                  |
|-----------------------------------------------|-------------------------------------|
| `app.jar` <br> `web_service` <br> `dependency` | > Start web_service <br> > Run app.jar |


## Docker Container
A Docker container is a runtime instance of a Docker image. It is a lightweight and portable environment that allows you to run applications in isolation from the host system. Containers can be started, stopped, and managed without affecting the underlying system.

A container is a single instance of an image. The container is in charge of running the program or application.

```
+------------------------------------+
|             Container              |
|                                    |
|        +-------------------+       |
|        |Running Process(es)|       |
|        +-------------------+       |
|                  |                 |
|                  v                 |
|          +----------------+        |
|          |    OS Kernel   |        |
|          +----------------+        |
|                  |                 |
|        +---------+---------+       |
|        |                   |       |
|   +----------+      +-----------+  |
|   |   RAM    |      |    CPU    |  |
|   +----------+      +-----------+  |
|   | Hard Drive |    |  Network  |  |
|   +----------+      +-----------+  |
+------------------------------------+
```

## Putting Together Docker Image and Container
1. **Build an Image:** You create a Docker image using a Dockerfile, which contains instructions on how to build the image, including the base operating system, software dependencies, and application code.
2. **Run a Container:** Once the image is built, you can create and run a container based on that image. The container will execute the application as specified in the image.
3. **Manage Containers:** You can start, stop, delete, and manage containers using Docker CLI commands or Docker Desktop.

## Putting Together Both Images and Containers

1. The **Image** is installed on the allocated Hard Drive.
2. The **Container** then runs the startup commands.
3. The services and/or applications are started.
4. Running applications and services are then given resources from the allocated pool.

```
+---------------------------------------------------+
|                      Container                    |
|                                                   |
|   +--------------------+      +----------------+  |
|   |    web_service     |      |    app.jar     |  |
|   +--------------------+      +----------------+  |
|                  |                                |
|                  |                                |
|   +--------------+---------------+                |
|   |      Running Process(es)     |                |
|   +------------------------------+                |
|                      |                            |
|                      v                            |
|            +--------------------+                 |
|            |     OS Kernel      |                 |
|            +--------------------+                 |
|                      |                            |
|       +--------------+---------------+            |
|       |                              |            |
|   +------------+                +----------+      |
|   |     RAM    |                |   CPU    |      |
|   +------------+                +----------+      |
|                                 |  Network |      |
|   +--- Image --+                +----------+      |
|   | app.jar    |                                  |
|   | dependency |                                  |
|   | web_service|                                  |
|   +------------+                                  |
+---------------------------------------------------+
```
### Explanation
- **Image:** The blueprint that gets installed on the hard drive.
- **Container:** The execution environment that runs applications based on the image.
- **Running Process(es):** The processes executing within the container.
- **OS Kernel:** The core component that manages system resources.
- **Allocated Resources:** The specific resources assigned to the container:
  - **RAM**
  - **CPU**
  - **Network**



## Docker Desktop Setup
1. **Download Docker Desktop:**
   - Visit the [Docker Desktop download page](https://www.docker.com/products/docker-desktop) and download the installer for your operating system (Windows or macOS).

2. **Install Docker Desktop:**
   - Run the installer and follow the prompts to install Docker Desktop on your machine.

3. **Run Docker Desktop:**
   - After installation, launch Docker Desktop. You should see the Docker icon in your system tray or menu bar.

4. **Verify Installation:**
   - Open a terminal (or command prompt) and run the following command to verify that Docker is installed correctly:
     ```
     docker --version
     ```

5. **Pull an Image:**
   - You can pull a Docker image from Docker Hub using the command:
     ```
     docker pull image_name
     ```

6. **Run a Container:**
   - To run a container from the pulled image, use the command:
     ```
     docker run -d image_name
     ```

## Images
Docker images can be managed and shared via Docker Hub or other container registries, allowing teams to collaborate and streamline their development processes.

![Docker Setup](https://www.docker.com/sites/default/files/d8/2019-07/docker-desktop-overview_1.png)  <!-- Example image URL for Docker Desktop setup -->

![Docker Image and Container](https://imgur.com/u9lG8RZ.png)  <!-- Placeholder for the Docker image illustration -->


# Docker CLI Commands

Docker provides a command-line interface (CLI) to manage containers, images, networks, and more. Below is a list of commonly used Docker CLI commands:

## General Commands
- **Check Docker Version:**
  ```bash
  docker --version
  ```

- **Get Help:**
  ```bash
  docker --help
  ```

## Image Commands
- **List Images:**
  ```bash
  docker images
  ```

- **Pull an Image from Docker Hub:**
  ```bash
  docker pull image_name
  ```

- **Remove an Image:**
  ```bash
  docker rmi image_name
  ```

- **Build an Image from a Dockerfile:**
  ```bash
  docker build -t image_name:tag .
  ```

## Container Commands
- **List Running Containers:**
  ```bash
  docker ps
  ```

- **List All Containers (including stopped):**
  ```bash
  docker ps -a
  ```

- **Run a Container:**
  ```bash
  docker run -d --name container_name image_name
  ```

- **Stop a Running Container:**
  ```bash
  docker stop container_name
  ```

- **Start a Stopped Container:**
  ```bash
  docker start container_name
  ```

- **Remove a Container:**
  ```bash
  docker rm container_name
  ```

- **Exec into a Running Container:**
  ```bash
  docker exec -it container_name /bin/bash
  ```

## Network Commands
- **List Networks:**
  ```bash
  docker network ls
  ```

- **Create a Network:**
  ```bash
  docker network create network_name
  ```

- **Remove a Network:**
  ```bash
  docker network rm network_name
  ```

## Volume Commands
- **List Volumes:**
  ```bash
  docker volume ls
  ```

- **Create a Volume:**
  ```bash
  docker volume create volume_name
  ```

- **Remove a Volume:**
  ```bash
  docker volume rm volume_name
  ```

## Docker Compose Commands
- **Start Services Defined in `docker-compose.yml`:**
  ```bash
  docker-compose up
  ```

- **Stop Services:**
  ```bash
  docker-compose down
  ```

- **View Logs:**
  ```bash
  docker-compose logs
  ```

- **Build Services:**
  ```bash
  docker-compose build
  ```

- **Execute a Command in a Running Service:**
  ```bash
  docker-compose exec service_name command
  ```


