# Docker Notes

## The Docker Platform

Docker provides tooling and a platform to manage the lifecycle of your containers:

- Develop your application and its supporting components using containers.

- The container becomes the unit for distributing and testing your application.

- When you're ready,  
  Deploy your application into your production environment,  
  As a container or an orchestrated service.

  This works the same whether your production environment is a local data center, a cloud provider, or a hybrid of the two.

## What can I use Docker for?

### Fast, consistent delivery of your applications.

<!-- Docker streamlines the development lifecycle,
By allowing developers to work in standardized environments using local containers which provide your applications and services. -->

Containers are great for continuous integration and continuous delivery (CI/CD) workflows.

Consider the following example scenario:

- Developers write code locally and share their work with their colleagues using Docker containers.

- They use Docker to push their applications into a test environment and run automated and manual tests.

- When developers find bugs,  
  They can fix them in the development environment,  
  And redeploy them to the test environment for testing and validation.

- When testing is complete,  
  Getting the fix to the customer is as simple as pushing the updated image to the production environment.

### Responsive deployment and scaling

Docker's container-based platform allows for highly portable workloads.

Docker containers can run on a developer's local laptop,  
On physical or virtual machines in a data center,  
On cloud providers,  
Or in a mixture of environments.

Docker's portability and lightweight nature also make it easy to dynamically manage workloads,  
Scaling up or tearing down applications and services as business needs dictate, in near real time.

### Running more workloads on the same hardware

Docker is lightweight and fast.

It provides a viable, cost-effective alternative,  
To hypervisor-based virtual machines,  
So you can use more of your server capacity to achieve your business goals.

Docker is perfect for high density environments,  
And for small and medium deployments where you need to do more with fewer resources.

## Docker Architecture

Docker uses a client-server architecture.

The Docker client talks to the Docker daemon,  
Which does the heavy lifting of building, running, and distributing your Docker containers.

The Docker client and daemon can run on the same system,  
Or you can connect a Docker client to a remote Docker daemon.

The Docker client and daemon communicate using a REST API,  
Over UNIX sockets or a network interface.

Another Docker client is Docker Compose,  
That lets you work with applications consisting of a set of containers.

### The Docker Daemon

The Docker daemon (dockerd) listens for Docker API requests,  
And manages Docker objects such as images, containers, networks, and volumes.

A daemon can also communicate with other daemons to manage Docker services.

### The Docker Client

The Docker client (docker) is the primary way that many Docker users interact with Docker.

When you use commands such as docker run,  
The client sends these commands to dockerd,  
Which carries them out.

The docker command uses the Docker API.

The Docker client can communicate with more than one daemon.

### Docker Desktop

Docker Desktop is the all-in-one package to build images, run containers, and so much more.

Docker Desktop is an easy-to-install application,  
For your Mac, Windows or Linux environment,  
That enables you to build and share containerized applications and microservices.

Docker Desktop includes:

- the Docker daemon (dockerd)
- the Docker client (docker)
- Docker Compose
- Docker Content Trust
- Kubernetes
- and Credential Helper

Docker Desktop simplifies container management for developers by streamlining the setup, configuration, and compatibility of applications across different environments, thereby addressing the pain points of environment inconsistencies and deployment challenges.

### Docker Registries

A Docker registry stores Docker images.

Docker Hub is a public registry that anyone can use,  
And Docker looks for images on Docker Hub by default.

You can even run your own private registry.

When you use the `docker pull` or `docker run` commands,  
Docker pulls the required images from your configured registry.

When you use the `docker push` command,  
Docker pushes your image to your configured registry.

### Docker Objects

When you use Docker,  
You are creating and using images, containers, networks, volumes, plugins, and other objects.

This section is a brief overview of some of those objects.

#### Images

An image is a read-only template with instructions for creating a Docker container.

Often, an image is based on another image,  
With some additional customization.

For example,  
You may build an image which is based on the ubuntu image,  
But installs the Apache web server and your application,  
As well as the configuration details needed to make your application run.

You might create your own images,  
Or you might only use those created by others and published in a registry.

To build your own image,  
You create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it.

Each instruction in a Dockerfile creates a layer in the image.

When you change the Dockerfile and rebuild the image,  
Only those layers which have changed are rebuilt.

This is part of what makes images so lightweight, small, and fast,  
When compared to other virtualization technologies.

#### Containers

A container is a runnable instance of an image.

You can create, start, stop, move, or delete a container using the Docker API or CLI.

You can connect a container to one or more networks,  
Attach storage to it,  
Or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine.  
You can control how isolated a container's network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it.

When a container is removed,  
Any changes to its state that aren't stored in persistent storage disappear.

## Example

## The underlying technology

## References

- [docker.com](https://docs.docker.com/get-started/docker-overview/)

## More

- https://www.docker.com/why-docker/
