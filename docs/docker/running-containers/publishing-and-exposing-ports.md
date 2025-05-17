# Publishing and exposing ports

## Explanation

If you've been following the guides so far,  
You understand that containers provide isolated processes,  
For each component of your application.

Each component - a React frontend, a Python API, and a Postgres database - runs in its own sandbox environment,  
Completely isolated from everything else on your host machine.

This isolation is great for security and managing dependencies,  
But it also means you can’t access them directly.

For example,  
You can’t access the web app in your browser.

That’s where port publishing comes in.

## Publishing ports

Publishing a port provides the ability to break through a little bit of networking isolation by setting up a forwarding rule.

As an example,  
You can indicate that requests on your host’s port `8080`,  
Should be forwarded to the container’s port `80`.

Publishing ports happens during container creation using the -p (or --publish) flag with docker run.

The syntax is:

```bash
docker run -d -p HOST_PORT:CONTAINER_PORT nginx
```

- `HOST_PORT`
  The port number on your host machine where you want to receive traffic.

- `CONTAINER_PORT`
  The port number within the container that's listening for connections.

For example,  
To publish the container's port `80` to host port `8080`:

```bash
docker run -d -p 8080:80 nginx
```

Now, any traffic sent to port `8080` on your host machine,  
Will be forwarded to port `80` within the container.

:::warning
When a port is published,  
It's published to all network interfaces by default.

This means any traffic that reaches your machine can access the published application.

Be mindful of publishing databases or any sensitive information.
:::

## Publishing To Ephemeral Ports

At times,  
You may want to simply publish the port but don’t care which host port is used.

In these cases,  
You can let Docker pick the port for you.

To do so,  
Simply omit the `HOST_PORT` configuration.

For example,  
The following command will publish the container’s port `80` onto an ephemeral port on the host:

```bash
docker run -p 80 nginx
```

Once the container is running,  
Using `docker ps` will show you the port that was chosen:

```bash
docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS          PORTS                    NAMES
a527355c9c53   nginx         "/docker-entrypoint.â¦"   4 seconds ago    Up 3 seconds    0.0.0.0:54772->80/tcp    romantic_williamson
```

In this example,  
The app is exposed on the host at port `54772`.

## Publishing All Ports

When creating a container image,  
The `EXPOSE` instruction is used to indicate the packaged application will use the specified port.

These ports aren't published by default.

With the `-P` or `--publish-all` flag,  
You can automatically publish all exposed ports to ephemeral ports.

This is quite useful when you’re trying to avoid port conflicts in development or testing environments.

For example,  
The following command will publish all of the exposed ports configured by the image:

```bash
docker run -P nginx
```

## References

- [https://docs.docker.com/get-started/docker-concepts/running-containers/publishing-ports/](https://docs.docker.com/get-started/docker-concepts/running-containers/publishing-ports/)
