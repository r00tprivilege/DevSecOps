## Docker

### Getting Started with Docker Containers

In this session, you'll gain hands-on experience deploying and working with Docker containers. By the end of this lesson, you'll be familiar with several key concepts and practices that will help you integrate Docker into your DevSecOps workflows. Specifically, you'll learn the following:

- **Basic Docker Syntax**: Understand the fundamental commands to interact with Docker and manage containers.
- **Running and Deploying Containers**: How to launch and manage your first Docker container.
- **Container Distribution via Images**: Learn how Docker containers are packaged and shared as images.
- **Creating Custom Docker Images**: Use Dockerfiles to build your own images tailored to your needs.
- **Using Docker Compose**: Understand how to use Docker Compose to orchestrate multi-container applications.
- **Practical Application**: Apply everything you've learned in a hands-on scenario to reinforce your understanding.

#### Prerequisites
For this session, it’s recommended that you have a basic understanding of Linux commands (e.g., navigating directories, running commands, managing files) and familiarity with the file system structure. If you've completed a **Linux Fundamentals** module or have equivalent knowledge, you'll be well-prepared for this session! 

By the end of this lesson, you'll have a foundational grasp of Docker that you can begin applying in your own DevSecOps practices to create, deploy, and manage containers securely.

## Basic Docker Syntax

### Basic Docker Commands and Syntax

Docker can seem overwhelming at first, but the commands are straightforward, and with some practice, you’ll quickly become proficient in using Docker for container management. The basic Docker syntax can be grouped into four main categories:

1. **Running Containers**
2. **Managing and Inspecting Containers**
3. **Managing Docker Images**
4. **Docker Daemon Information and Stats**

In this section, we will dive into each category and focus on the **Managing Docker Images** section, which is essential for running and deploying containers.

### Managing Docker Images

Before running a Docker container, you need an **image**. Think of an image as the blueprint for the container—it's essentially a set of instructions about what the container should execute once it is running. 

#### Docker Pull
To start, you need to **pull** an image from a Docker registry to your local machine. You can use the `docker pull` command followed by the image name. For example:

```bash
docker pull nginx
```

This command will download the **Nginx** image from the Docker repository to your local system.

When Docker downloads the image, it will assign a **tag** to the image. Tags are used to represent different versions of an image. If no tag is specified, Docker assumes you want the **latest** version. Here’s a breakdown of how tags work:

| Docker Image | Tag     | Command Example              | Explanation                                    |
|--------------|---------|------------------------------|------------------------------------------------|
| ubuntu       | latest  | `docker pull ubuntu`          | Pulls the latest version of the "ubuntu" image. |
| ubuntu       | 20.04   | `docker pull ubuntu:20.04`    | Pulls version "20.04" of the "ubuntu" image.    |
| ubuntu       | 18.04   | `docker pull ubuntu:18.04`    | Pulls version "18.04" of the "ubuntu" image.    |

**Note**: When using a tag, always include a colon `:` between the image name and the tag, e.g., `ubuntu:20.04`.

#### Docker Image Command

Once you’ve pulled images, you can manage them with the `docker image` command. Here are some key options:

- **List images**: `docker image ls`
- **Remove an image**: `docker image rm <image_name>`
- **Build an image**: `docker image build`

For a full list of available commands, you can type:

```bash
docker image
```

Here are some of the common options for managing Docker images:

| Command         | Description                                                 |
|-----------------|-------------------------------------------------------------|
| `ls`            | Lists all images stored locally.                            |
| `rm`            | Removes one or more images from your local system.          |
| `build`         | Build an image from a Dockerfile (we’ll cover this later).  |
| `prune`         | Remove unused images to free up space.                      |

#### Docker Image ls

To see all the images stored on your local machine, use the `docker image ls` command. This command displays essential information about each image, including its repository, tag, image ID, creation date, and size.

Example:

```bash
docker image ls
```

```bash
REPOSITORY   TAG     IMAGE ID       CREATED         SIZE
nginx        latest  abcdef123456   2 weeks ago     142MB
ubuntu       20.04   78910abcdef    10 days ago     77.8MB
```

In the example above, we can see two images: **Nginx** and **Ubuntu**. 

#### Docker Image rm

If you no longer need an image, you can remove it using the `docker image rm` command. For example:

```bash
docker image rm ubuntu:20.04
```

This will remove the **Ubuntu 20.04** image from your local machine. After running the command, if you list the images again using `docker image ls`, you will see that the image has been removed.

Example:

```bash
docker image ls
```

```bash
REPOSITORY   TAG     IMAGE ID       CREATED         SIZE
nginx        latest  abcdef123456   2 weeks ago     142MB
```

As shown above, the **Ubuntu 20.04** image is no longer listed because it was successfully removed.

---

By mastering these basic Docker image management commands, you’ll be able to efficiently download, list, and remove images as part of your container deployment workflow. In the next section, you will learn how to create your own custom Docker images and orchestrate multi-container applications using Docker Compose.


## Running Your First Container

The `docker run` command is fundamental to Docker usage. It allows you to create and start containers from images. The `docker run` command runs the instructions specified in the Dockerfile and can also accept user-defined input at runtime.

The basic syntax for running a container is:

```bash
docker run [OPTIONS] IMAGE_NAME [COMMAND] [ARGUMENTS...]
```

Here, the options within the brackets are optional and depend on how you want the container to behave. Let's explore the syntax and the most commonly used options to get a container running.

#### Running a Container Interactively
Let’s start by running a simple container interactively. This means you’ll be able to access the container's shell and interact with it directly. Here's the syntax we’ll use:

```bash
docker run -it helloworld /bin/bash
```

- **`-it`**: This option tells Docker to run the container interactively (`-i`) and allocate a terminal (`-t`), giving you the ability to interact with the container's shell.
- **`helloworld`**: This is the name of the image we’re using to create the container.
- **`/bin/bash`**: This is the command to launch a shell inside the container.

Once you run this command, you'll be inside the container’s shell, with the prompt changing to something like:

```bash
root@30eff5ed7492:~#
```

Here, `root` is the user, and `30eff5ed7492` is the container ID. To verify the container is running, you can use the `docker ps` command to list running containers.

#### Common `docker run` Options

Docker containers can be started with various options depending on the use case. Here's a list of common `docker run` options that may be useful:

| Option  | Explanation | Example |
| ------- | ----------- | ------- |
| `-d`    | Detached mode: Runs the container in the background. | `docker run -d helloworld` |
| `-it`   | Interactive mode: Lets you interact with the container's terminal. | `docker run -it helloworld /bin/bash` |
| `-v`    | Mounts a volume from the host to the container. | `docker run -v /host/directory:/container/directory helloworld` |
| `-p`    | Maps a port on the host to a port in the container. | `docker run -p 80:80 webserver` |
| `--rm`  | Automatically removes the container once it finishes running. | `docker run --rm helloworld` |
| `--name`| Assigns a custom name to the container. | `docker run --name mycontainer helloworld` |

### Example Explained:
Let’s break down an example of running a container with some options:

```bash
docker run -d -p 8000:80 --name mywebserver nginx
```

- `-d`: Runs the container in the background.
- `-p 8000:80`: Maps port 8000 on the host to port 80 in the container (where the web server inside the container is listening).
- `--name mywebserver`: Assigns a name "mywebserver" to the container.
- `nginx`: The name of the image being used (in this case, an Nginx web server image).

This command will start an Nginx web server in the background, map port 8000 on your local machine to port 80 in the container, and give the container a custom name.

### Listing Running Containers

To see the containers that are currently running, use the `docker ps` command:

```bash
docker ps
```

Example output:

```bash
CONTAINER ID   IMAGE                COMMAND        CREATED        STATUS       PORTS          NAMES
a913a8f6e30f   cmnatic/helloworld   "sleep"        1 month ago    Up 3 days    0.0.0.0:8000->8000/tcp   helloworld
```

This shows details about the container, including:

- **Container ID**: The unique identifier for the running container.
- **Image**: The image used to start the container.
- **Command**: The command the container is running.
- **Created**: When the container was created.
- **Status**: The container’s current status (up, paused, etc.).
- **Ports**: Any ports exposed and their mappings.
- **Names**: The container’s name.

### Listing All Containers (Including Stopped Ones)

To list **all** containers, including those that have stopped, use:

```bash
docker ps -a
```

Example output:

```bash
CONTAINER ID   IMAGE                COMMAND               CREATED         STATUS      PORTS   NAMES
00ba1eed0826   gobuster:cmnatic     "./gobuster dir ..."   1 hour ago      Exited 1 hour ago   practical_khayyam
```

This shows all containers, including the ones that are no longer running.

---

By using these commands and options, you’ll be able to run, manage, and interact with containers effectively. Experimenting with different options, such as `-v` for mounting volumes and `-p` for port forwarding, will give you a good understanding of how to work with containers in various scenarios.


## Intro to Dockerfiles

### Introduction to Dockerfiles

Dockerfiles are a key part of working with Docker. A Dockerfile is a script that contains a series of instructions, telling Docker how to build a Docker image from scratch or a base image. Think of it as a recipe for creating a custom containerized environment. Each instruction in a Dockerfile creates a layer in the final image.

Here’s the basic structure of a Dockerfile:

```plaintext
INSTRUCTION argument
```

Let’s go over some common Dockerfile instructions and their use cases:

| Instruction  | Description | Example |
|--------------|-------------|---------|
| **FROM**     | Specifies the base image for the container, like an OS or application. The first instruction in every Dockerfile. | `FROM ubuntu:20.04` |
| **RUN**      | Executes commands during image build, often used to install software or configure the environment. | `RUN apt-get update && apt-get install -y nginx` |
| **COPY**     | Copies files or directories from the host system into the container's filesystem. | `COPY ./myapp /app` |
| **WORKDIR**  | Sets the working directory inside the container for subsequent instructions. | `WORKDIR /app` |
| **CMD**      | Specifies the default command that will be executed when the container starts. | `CMD ["python", "app.py"]` |
| **EXPOSE**   | Informs Docker that the container will listen on the specified network ports. | `EXPOSE 8080` |

### Building Your First Dockerfile

Let’s create a basic Dockerfile for a simple task. Here’s the goal for this container:

1. Use the "Ubuntu 20.04" operating system as the base.
2. Set the working directory to `/` (root directory).
3. Create a file named `helloworld.txt` inside the container.

Here’s what the Dockerfile would look like:

```dockerfile
FROM ubuntu:20.04
WORKDIR /
RUN echo "Hello, Docker!" > helloworld.txt
```

This Dockerfile will create an image based on Ubuntu 20.04, set the working directory to the root of the container, and create a text file `helloworld.txt` with the content "Hello, Docker!".

#### Building the Image

To build the image from the Dockerfile, you would use the `docker build` command:

```bash
docker build -t helloworld .
```

Here:

- `-t` is used to tag the image with a name (`helloworld` in this case).
- `.` tells Docker to look in the current directory for the Dockerfile.

After building, use `docker image ls` to verify that the image was created. You should see both your image (`helloworld`) and the base image (`ubuntu:20.04`) listed.

#### Running the Container

Now that the image is built, you can run it with the following command:

```bash
docker run helloworld
```

This will execute the default command specified in the Dockerfile (if any), or run an interactive shell if no `CMD` was specified.

### Expanding Your Dockerfile

Now that we’ve seen a simple Dockerfile, let’s expand on it by creating a more useful container. For example, let’s build a container that:

1. Uses **Ubuntu 20.04** as the base image.
2. Installs the **Apache2** web server.
3. Exposes **port 80** to allow access to the web server.
4. Starts the **Apache2** service when the container runs.

Here’s the Dockerfile for that:

```dockerfile
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y apache2
EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]
```

In this Dockerfile:

- **RUN** installs the Apache2 server.
- **EXPOSE 80** tells Docker to expose port 80 so you can access the web server.
- **CMD** starts the Apache2 server in the foreground when the container starts.

#### Building and Running the Web Server Container

To build the image:

```bash
docker build -t webserver .
```

Once the image is built, run the container:

```bash
docker run -d -p 80:80 --name mywebserver webserver
```

This runs the container in detached mode (`-d`), binds port 80 on the host to port 80 in the container, and names the container `mywebserver`.

Now, open your browser and navigate to the IP address of your Docker host. You should see the default Apache2 welcome page!

### Optimizing Your Dockerfile

Optimizing your Dockerfile can lead to faster builds and smaller images. Here are some tips for optimizing your Dockerfiles:

1. **Install Only Essential Packages**: Containers should only contain what’s necessary. By keeping your image lean, you can reduce the attack surface and speed up builds.
   
   Example: Instead of installing all of Ubuntu’s default packages, use a minimal base image, such as `ubuntu:20.04-minimal` or `alpine`.

2. **Remove Cache and Unnecessary Files**: After installing packages, the image might include unnecessary cached files, such as package manager caches. Removing these can shrink the image size.

   Example:
   ```dockerfile
   RUN apt-get update && apt-get install -y apache2 && apt-get clean
   ```

3. **Use Multi-Layer Instructions**: Each Dockerfile instruction creates a layer in the final image. To minimize the number of layers, you can combine multiple commands into a single `RUN` instruction.

   Before optimization:
   ```dockerfile
   RUN apt-get update
   RUN apt-get install -y apache2
   ```

   After optimization:
   ```dockerfile
   RUN apt-get update && apt-get install -y apache2
   ```

4. **Choose Minimal Base Images**: Using a minimal base image reduces the overall size of the image and the number of unnecessary dependencies. For example, consider using Alpine Linux, which is much smaller than Ubuntu.

   Example:
   ```dockerfile
   FROM alpine:3.13
   ```

   Alpine images are often less than 10MB, compared to Ubuntu's 100MB+.

5. **Minimize the Number of Layers**: Each instruction creates a separate layer, which can make the build slower and the image larger. You can minimize layers by combining instructions wherever possible.

   Before optimization:
   ```dockerfile
   RUN apt-get update
   RUN apt-get install -y apache2
   ```

   After optimization:
   ```dockerfile
   RUN apt-get update && apt-get install -y apache2
   ```

### Conclusion

Creating Dockerfiles is the key to building and maintaining efficient Docker images. By understanding the core instructions like `FROM`, `RUN`, `COPY`, and `CMD`, you can customize your containers to fit your needs. Optimizing Dockerfiles ensures your images are lean, efficient, and easier to maintain.

As you work with Docker, keep experimenting with different instructions, optimizing your images, and refining your Dockerfiles for better performance and security.


## Intro to Docker Compose

### Introduction to Dockerfiles

Dockerfiles are a key part of working with Docker. A Dockerfile is a script that contains a series of instructions, telling Docker how to build a Docker image from scratch or a base image. Think of it as a recipe for creating a custom containerized environment. Each instruction in a Dockerfile creates a layer in the final image.

Here’s the basic structure of a Dockerfile:

```plaintext
INSTRUCTION argument
```

Let’s go over some common Dockerfile instructions and their use cases:

| Instruction  | Description | Example |
|--------------|-------------|---------|
| **FROM**     | Specifies the base image for the container, like an OS or application. The first instruction in every Dockerfile. | `FROM ubuntu:20.04` |
| **RUN**      | Executes commands during image build, often used to install software or configure the environment. | `RUN apt-get update && apt-get install -y nginx` |
| **COPY**     | Copies files or directories from the host system into the container's filesystem. | `COPY ./myapp /app` |
| **WORKDIR**  | Sets the working directory inside the container for subsequent instructions. | `WORKDIR /app` |
| **CMD**      | Specifies the default command that will be executed when the container starts. | `CMD ["python", "app.py"]` |
| **EXPOSE**   | Informs Docker that the container will listen on the specified network ports. | `EXPOSE 8080` |

### Building Your First Dockerfile

Let’s create a basic Dockerfile for a simple task. Here’s the goal for this container:

1. Use the "Ubuntu 20.04" operating system as the base.
2. Set the working directory to `/` (root directory).
3. Create a file named `helloworld.txt` inside the container.

Here’s what the Dockerfile would look like:

```dockerfile
FROM ubuntu:20.04
WORKDIR /
RUN echo "Hello, Docker!" > helloworld.txt
```

This Dockerfile will create an image based on Ubuntu 20.04, set the working directory to the root of the container, and create a text file `helloworld.txt` with the content "Hello, Docker!".

#### Building the Image

To build the image from the Dockerfile, you would use the `docker build` command:

```bash
docker build -t helloworld .
```

Here:

- `-t` is used to tag the image with a name (`helloworld` in this case).
- `.` tells Docker to look in the current directory for the Dockerfile.

After building, use `docker image ls` to verify that the image was created. You should see both your image (`helloworld`) and the base image (`ubuntu:20.04`) listed.

#### Running the Container

Now that the image is built, you can run it with the following command:

```bash
docker run helloworld
```

This will execute the default command specified in the Dockerfile (if any), or run an interactive shell if no `CMD` was specified.

### Expanding Your Dockerfile

Now that we’ve seen a simple Dockerfile, let’s expand on it by creating a more useful container. For example, let’s build a container that:

1. Uses **Ubuntu 20.04** as the base image.
2. Installs the **Apache2** web server.
3. Exposes **port 80** to allow access to the web server.
4. Starts the **Apache2** service when the container runs.

Here’s the Dockerfile for that:

```dockerfile
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y apache2
EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]
```

In this Dockerfile:

- **RUN** installs the Apache2 server.
- **EXPOSE 80** tells Docker to expose port 80 so you can access the web server.
- **CMD** starts the Apache2 server in the foreground when the container starts.

#### Building and Running the Web Server Container

To build the image:

```bash
docker build -t webserver .
```

Once the image is built, run the container:

```bash
docker run -d -p 80:80 --name mywebserver webserver
```

This runs the container in detached mode (`-d`), binds port 80 on the host to port 80 in the container, and names the container `mywebserver`.

Now, open your browser and navigate to the IP address of your Docker host. You should see the default Apache2 welcome page!

### Optimizing Your Dockerfile

Optimizing your Dockerfile can lead to faster builds and smaller images. Here are some tips for optimizing your Dockerfiles:

1. **Install Only Essential Packages**: Containers should only contain what’s necessary. By keeping your image lean, you can reduce the attack surface and speed up builds.
   
   Example: Instead of installing all of Ubuntu’s default packages, use a minimal base image, such as `ubuntu:20.04-minimal` or `alpine`.

2. **Remove Cache and Unnecessary Files**: After installing packages, the image might include unnecessary cached files, such as package manager caches. Removing these can shrink the image size.

   Example:
   ```dockerfile
   RUN apt-get update && apt-get install -y apache2 && apt-get clean
   ```

3. **Use Multi-Layer Instructions**: Each Dockerfile instruction creates a layer in the final image. To minimize the number of layers, you can combine multiple commands into a single `RUN` instruction.

   Before optimization:
   ```dockerfile
   RUN apt-get update
   RUN apt-get install -y apache2
   ```

   After optimization:
   ```dockerfile
   RUN apt-get update && apt-get install -y apache2
   ```

4. **Choose Minimal Base Images**: Using a minimal base image reduces the overall size of the image and the number of unnecessary dependencies. For example, consider using Alpine Linux, which is much smaller than Ubuntu.

   Example:
   ```dockerfile
   FROM alpine:3.13
   ```

   Alpine images are often less than 10MB, compared to Ubuntu's 100MB+.

5. **Minimize the Number of Layers**: Each instruction creates a separate layer, which can make the build slower and the image larger. You can minimize layers by combining instructions wherever possible.

   Before optimization:
   ```dockerfile
   RUN apt-get update
   RUN apt-get install -y apache2
   ```

   After optimization:
   ```dockerfile
   RUN apt-get update && apt-get install -y apache2
   ```

### Conclusion

Creating Dockerfiles is the key to building and maintaining efficient Docker images. By understanding the core instructions like `FROM`, `RUN`, `COPY`, and `CMD`, you can customize your containers to fit your needs. Optimizing Dockerfiles ensures your images are lean, efficient, and easier to maintain.

As you work with Docker, keep experimenting with different instructions, optimizing your images, and refining your Dockerfiles for better performance and security.


##  Docker Socket

### Introduction to Docker Sockets

Docker operates using a client-server architecture, where two key components work together to manage containers and their lifecycle:

1. **The Docker Client**: The user-facing tool that allows you to interact with Docker.
2. **The Docker Server**: The core engine that handles container management, including creating, running, and stopping containers.

At the heart of this communication between the client and server lies **sockets**—a critical aspect of how Docker functions. In simple terms, a socket acts as a communication channel between different parts of a system, allowing processes to send and receive data. Docker leverages these sockets to communicate commands and responses between the Docker Client and the Docker Server.

To help illustrate, think of a chat application. When you send a message, the application uses a socket to store the outgoing message, and another socket to store incoming messages. Similarly, Docker uses a socket to manage interactions between the Docker Client (which sends requests) and the Docker Server (which processes them).

Sockets in Docker can either represent network connections (like a socket on a network port) or local files on the operating system, but both are used to facilitate **Interprocess Communication (IPC)**. IPC allows different processes or applications running on the same machine to talk to each other, a key element of Docker's ability to manage containers.

### Docker Socket and Its Role

In the case of Docker, the **Docker Server** functions as an API, waiting for requests from clients. The **Docker Client**, using commands like `docker run` or `docker ps`, sends requests to the server's API, which then processes these requests to perform container actions. 

For example, when you run a command like `docker run myimage`, the **Docker Client** sends a request to the **Docker Server** via the Docker socket, asking it to launch a container using the `myimage` image. The Docker Server will then execute this request and respond with the appropriate action, such as starting the container or displaying any errors.

While this overview simplifies the process, it provides the basic framework of how Docker works under the hood. Now, let's take a deeper look into this process with an example.

### Using Tools to Interact with Docker's API

Because the Docker Server communicates via an API, it's not just limited to the `docker` command-line tool. You can also use other tools to communicate with the Docker API, such as `curl` or API testing tools like Postman.

For example, you can use **Postman** to send requests to the Docker API. A typical use case might involve retrieving a list of all stored Docker images:

1. Use Postman or another API tool to make an HTTP request to the Docker server’s API endpoint that lists images.
2. The Docker Server processes the request and sends back a response, which contains details about the available images.

This opens up the possibility of interacting with Docker programmatically from other systems or applications, making automation and integration much more flexible.

### Security Implications: Exposing Docker Sockets

A crucial security consideration is that Docker can be configured to listen for commands from external devices. This is done by exposing the Docker socket to other machines, potentially allowing remote management of containers. 

**However, this can be a significant security risk if not configured correctly.** If someone gains unauthorized access to this exposed Docker socket, they could issue commands like starting or stopping containers, or even accessing sensitive data within containers. This is particularly dangerous if Docker is running on a production machine without proper security measures in place, as it could allow remote attackers to control and manipulate containers.

To avoid this, it's essential to secure the Docker socket and configure the host machine to only accept commands from trusted sources. Here are a few recommendations for securing Docker sockets:

- **Restrict Access**: Limit Docker socket access to trusted users and services. You can configure Docker to require authentication when interacting with the socket.
- **Use TLS**: Configure Docker to communicate over TLS (Transport Layer Security), which encrypts the communication and adds authentication.
- **Avoid Exposing the Socket**: If possible, do not expose the Docker socket to external networks or remote machines.

In summary, Docker uses sockets for communication between the client and server, facilitating the management of containers. However, this feature can introduce serious security vulnerabilities if exposed or misconfigured, as it can allow remote users to interact with Docker on the host machine. Therefore, securing the Docker socket is critical for protecting your environment.