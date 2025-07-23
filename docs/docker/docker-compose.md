---
sidebar_position: 4
---

# Docker Compose

## What Is Docker Compose?

So far you've been working with single container applications.

But, now you're wanting to do something more complicated,  
Run databases, message queues, caches, or a variety of other services.

Do you install everything in a single container?  
Run multiple containers?  
If you run multiple, how do you connect them all together?

One best practice for containers is that each container should do one thing and do it well.

While there are exceptions to this rule,  
Avoid the tendency to have one container do multiple things.

You can use multiple docker run commands to start multiple containers.

But, you'll soon realize you'll need to manage networks,  
All of the flags needed to connect containers to those networks, and more.

And when you're done,  
Cleanup is a little more complicated.

With Docker Compose,  
You can define all of your containers and their configurations in a single YAML file.

If you include this file in your code repository,  
Anyone that clones your repository can get up and running with a single command.

It's important to understand that Compose is a declarative tool,  
You simply define it and go.

You don't always need to recreate everything from scratch.

If you make a change,  
Run docker compose up again and Compose will reconcile the changes in your file and apply them intelligently.

## Dockerfile versus Compose file

A Dockerfile provides instructions to build a container image,  
While a Compose file defines your running containers.

Quite often,  
A Compose file references a Dockerfile to build an image to use for a particular service.

## References

- [docs.docker.com/get-started/docker-concepts/the-basics/what-is-docker-compose/](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-docker-compose/)
