# Image

## Explanation

Seeing a container is an isolated process,  
Where does it get its files and configuration?  
How do you share those environments?

That's where container images come in.  
A container image is a standardized package that includes all of the files, binaries, libraries, and configurations to run a container.

For a PostgreSQL image,  
That image will package the database binaries, config files, and other dependencies.

For a Python web app,  
It'll include the Python runtime, your app code, and all of its dependencies.

There are two important principles of images:

- Images are immutable.  
  Once an image is created, it can't be modified.

  You can only make a new image or add changes on top of it.

- Container images are composed of layers.  
  Each layer represents a set of file system changes that add, remove, or modify files.

These two principles let you to extend or add to existing images.

For example,  
If you are building a Python app,  
You can start from the Python image and add additional layers to install your app's dependencies and add your code.

This lets you focus on your app,  
Rather than Python itself.

## Finding images

Docker Hub is the default global marketplace for storing and distributing images.

It has over 100,000 images created by developers that you can run locally.

You can search for Docker Hub images and run them directly from Docker Desktop.

Docker Hub provides a variety of Docker-supported and endorsed images known as _Docker Trusted Content_.

These provide fully managed services or great starters for your own images.

These include:

- Docker Official Images
  A curated set of Docker repositories,  
  Serve as the starting point for the majority of users,  
  And are some of the most secure on Docker Hub.

- Docker Verified Publishers
  high-quality images from commercial publishers verified by Docker.

- Docker-Sponsored Open Source
  Images published and maintained by open-source projects sponsored by Docker through Docker's open source program.

For example, Redis and Memcached are a few popular ready-to-go Docker Official Images.  
You can download these images and have these services up and running in a matter of seconds.

There are also base images,  
Like the Node.js Docker image,  
That you can use as a starting point and add your own files and configurations.

## References

- [docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/)
