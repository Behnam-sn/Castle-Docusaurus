# Overriding Container Defaults

## Explanation

When a Docker container starts,  
It executes an application or command.

The container gets this executable (script or file) from its image’s configuration.

Containers come with default settings that usually work well,  
But you can change them if needed.

These adjustments help the container's program run exactly how you want it to.

For example,  
If you have an existing database container that listens on the standard port,  
And you want to run a new instance of the same database container,  
Then you might want to change the port settings the new container listens on,  
So that it doesn’t conflict with the existing container.

Sometimes you might want to increase the memory available to the container,  
If the program needs more resources to handle a heavy workload,  
Or set the environment variables to provide specific configuration details the program needs to function properly.

The `docker run` command offers a powerful way to override these defaults,  
And tailor the container's behavior to your liking.

The command offers several flags that let you to customize container behavior on the fly.

Here's a few ways you can achieve this.

## Overriding The Network Ports

Sometimes you might want to use separate database instances for development and testing purposes.

Running these database instances on the same port might conflict.

You can use the `-p` option in `docker run` to map container ports to host ports,  
Allowing you to run the multiple instances of the container without any conflict.

```bash
docker run -d -p HOST_PORT:CONTAINER_PORT postgres
```

## Setting Environment Variables

This option sets an environment variable `foo` inside the container with the value `bar`.

```bash
docker run -e foo=bar postgres env
```

You will see output like the following:

```bash
HOSTNAME=2042f2e6ebe4
foo=bar
```

:::tip
The `.env` file acts as a convenient way to set environment variables for your Docker containers without cluttering your command line with numerous `-e` flags.

To use a `.env` file,  
You can pass `--env-file` option with the docker run command.
:::

```bash
docker run --env-file .env postgres env
```

## Restricting The Container To Consume The Resources

You can use the `--memory` and `--cpus` flags with the `docker run` command,  
To restrict how much CPU and memory a container can use.

For example,  
You can set a memory limit for the Python API container,  
Preventing it from consuming excessive resources on your host.

Here's the command:

```bash
docker run -e POSTGRES_PASSWORD=secret --memory="512m" --cpus="0.5" postgres
```

This command limits container memory usage to 512 MB and defines the CPU quota of 0.5 for half a core.

:::note
Monitor the real-time resource usage

You can use the `docker stats` command to monitor the real-time resource usage of running containers.

This helps you understand whether the allocated resources are sufficient or need adjustment.
:::

By effectively using these `docker run` flags,  
You can tailor your containerized application's behavior to fit your specific requirements.

## References

- [https://docs.docker.com/get-started/docker-concepts/running-containers/overriding-container-defaults/](https://docs.docker.com/get-started/docker-concepts/running-containers/overriding-container-defaults/)
