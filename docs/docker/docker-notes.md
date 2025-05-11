# Docker

## What is Docker?

Docker is an open platform for developing, shipping, and running applications.

Docker enables you to separate your applications from your infrastructure,  
So you can deliver software quickly.

With Docker, you can manage your infrastructure in the same ways you manage your applications.

By taking advantage of Docker's methodologies for shipping, testing, and deploying code,  
You can significantly reduce the delay between writing code and running it in production.

## What is a Container?

Docker provides the ability to package and run an application,  
In a loosely isolated environment called a container.

The isolation and security lets you run many containers simultaneously on a given host.

Containers are lightweight and contain everything needed to run the application,  
So you don't need to rely on what's installed on the host.

You can share containers while you work,  
And be sure that everyone you share with gets the same container that works in the same way.

## The Docker platform

Docker provides tooling and a platform to manage the lifecycle of your containers:

- Develop your application and its supporting components using containers.

- The container becomes the unit for distributing and testing your application.

- When you're ready,  
  Deploy your application into your production environment,  
  As a container or an orchestrated service.

  This works the same whether your production environment is a local data center, a cloud provider, or a hybrid of the two.

## What can I use Docker for?

Fast, consistent delivery of your applications.

Docker streamlines the development lifecycle,  
By allowing developers to work in standardized environments using local containers which provide your applications and services.

Containers are great for continuous integration and continuous delivery (CI/CD) workflows.

Consider the following example scenario:

- Developers write code locally and share their work with their colleagues using Docker containers.

- They use Docker to push their applications into a test environment and run automated and manual tests.

- When developers find bugs,  
  They can fix them in the development environment,  
  And redeploy them to the test environment for testing and validation.

- When testing is complete,  
  Getting the fix to the customer is as simple as pushing the updated image to the production environment.

## Responsive deployment and scaling

Docker's container-based platform allows for highly portable workloads.

Docker containers can run on a developer's local laptop,  
On physical or virtual machines in a data center,  
On cloud providers,  
Or in a mixture of environments.

Docker's portability and lightweight nature also make it easy to dynamically manage workloads,  
Scaling up or tearing down applications and services as business needs dictate, in near real time.

## Running more workloads on the same hardware

Docker is lightweight and fast.

It provides a viable, cost-effective alternative,  
To hypervisor-based virtual machines,  
So you can use more of your server capacity to achieve your business goals.

Docker is perfect for high density environments,  
And for small and medium deployments where you need to do more with fewer resources.

## Docker architecture

Docker uses a client-server architecture.

The Docker client talks to the Docker daemon,  
Which does the heavy lifting of building, running, and distributing your Docker containers.

The Docker client and daemon can run on the same system,  
Or you can connect a Docker client to a remote Docker daemon.

The Docker client and daemon communicate using a REST API,  
Over UNIX sockets or a network interface.

Another Docker client is Docker Compose,  
That lets you work with applications consisting of a set of containers.

## References

- [docker.com](https://docs.docker.com/get-started/docker-overview/)
