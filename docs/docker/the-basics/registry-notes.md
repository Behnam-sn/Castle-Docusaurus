# Registry

## Explanation

Now that you know what a container image is and how it works,  
You might wonder, where do you store these images?

Well you can store your container images on your computer system,  
But what if you want to share them with your friends?  
Or use them on another machine?  
That's where the image registry comes in.

An image registry is a centralized location for storing and sharing your container images.

It can be either public or private.

Docker Hub is a public registry that anyone can use and is the default registry.

While Docker Hub is a popular option,  
There are many other available container registries available today,  
Including:  
Amazon Elastic Container Registry(ECR),  
Azure Container Registry (ACR),  
And Google Container Registry (GCR).

You can even run your private registry on your local system or inside your organization.  
For example, Harbor, JFrog Artifactory, GitLab Container registry etc.

## Registry vs. repository

While you're working with registries,  
You might hear the terms registry and repository as if they're interchangeable.

Even though they're related,  
They're not quite the same thing.

A registry is a centralized location that stores and manages container images,  
Whereas a repository is a collection of related container images within a registry.

Think of it as a folder where you organize your images based on projects.

Each repository contains one or more container images.

## References

- [docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-registry/](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-registry/)
