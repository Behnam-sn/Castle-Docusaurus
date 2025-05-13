# Writing a Dockerfile

## Explanation

A Dockerfile is a text-based document that's used to create a container image.

It provides instructions to the image builder on the commands to run, files to copy, startup command, and more.

As an example,  
The following Dockerfile would produce a ready-to-run Python application:

```dockerfile
FROM python:3.12
WORKDIR /usr/local/app

# Install the application dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Copy in the source code
COPY src ./src
EXPOSE 5000

# Setup an app user so the container doesn't run as the root user
RUN useradd app
USER app

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8080"]
```

## Common instructions

Some of the most common instructions in a Dockerfile include:

- `FROM <image>`
  This specifies the base image that the build will extend.

- `WORKDIR <path>`
  This instruction specifies the "working directory",  
  Or the path in the image,  
  Where files will be copied and commands will be executed.

- `COPY <host-path> <image-path>`
  This instruction tells the builder to copy files from the host,  
  And put them into the container image.

- `RUN <command>`  
  This instruction tells the builder to run the specified command.

- `ENV <name> <value>`  
  This instruction sets an environment variable that a running container will use.

- `EXPOSE <port-number>`  
  This instruction sets configuration on the image that indicates a port the image would like to expose.

- `USER <user-or-uid>`  
  This instruction sets the default user for all subsequent instructions.

- `CMD ["<command>", "<arg1>"]`  
  This instruction sets the default command a container using this image will run.

## Reference

- [docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/](https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/)

## More

- https://docs.docker.com/reference/dockerfile/
- https://docs.docker.com/build/building/best-practices/
- https://docs.docker.com/build/building/base-images/
- https://docs.docker.com/reference/cli/docker/init/
