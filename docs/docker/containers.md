---
sidebar_position: 1
---

# Containers

## What Problem Containers Are Trying To Solve?

Imagine you're developing a killer web app that has three main components:

- A React frontend
- A Python API
- And a PostgreSQL database

If you wanted to work on this project,  
You'd have to install Node, Python, and PostgreSQL.

How do you make sure you have the same versions as the other developers on your team?  
Or your CI/CD system?  
Or what's used in production?

How do you ensure the version of Python or Node or the database your app needs isn't affected by what's already on your machine?  
How do you manage potential conflicts?

Simply put, containers are isolated processes for each of your app's components.

Each component runs in its own isolated environment,  
Completely isolated from everything else on your machine.

## What Is A Container?

Docker provides the ability to package and run an application,  
In a loosely isolated environment called a container.

The isolation and security lets you run many containers simultaneously on a given host.

Containers are lightweight and contain everything needed to run the application,  
So you don't need to rely on what's installed on the host.

You can share containers while you work,  
And be sure that everyone you share with,  
Gets the same container,  
That works in the same way.

<!-- ## What Makes Them Awesome? -->

Containers are:

- ### Self-Contained

  Each container has everything it needs to function,  
  With no reliance on any pre-installed dependencies on the host machine.

- ### Isolated

  Since containers are run in isolation,  
  They have minimal influence on the host and other containers,  
  Increasing the security of your applications.

- ### Independent

  Each container is independently managed.  
  Deleting one container won't affect any others.

- ### Portable

  Containers can run anywhere!  
  The container that runs on your development machine,  
  Will work the same way in a data center or anywhere in the cloud!

## Containers Vs. Virtual Machines

Without getting too deep,  
A VM is an entire operating system,  
With its own kernel, hardware drivers, programs, and applications.

Spinning up a VM only to isolate a single application is a lot of overhead.  
A container is simply an isolated process with all of the files it needs to run.

If you run multiple containers,  
They all share the same kernel,  
Allowing you to run more applications on less infrastructure.

## Using Virtual Machines And Containers Together

Quite often,  
You will see containers and VMs used together.

As an example,  
In a cloud environment,  
The provisioned machines are typically VMs.

However,  
Instead of provisioning one machine to run one application,  
A VM with a container runtime can run multiple containerized applications,  
Increasing resource utilization and reducing costs.

## References

- [docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/)

## More

- [docker.com/resources/what-container/](https://www.docker.com/resources/what-container/)
