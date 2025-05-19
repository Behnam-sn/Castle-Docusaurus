# Persisting container data

## Explanation

When a container starts,  
It uses the files and configuration provided by the image.

Each container is able to create, modify, and delete files,  
And does so without affecting any other containers.

When the container is deleted,  
These file changes are also deleted.

While this ephemeral nature of containers is great,  
It poses a challenge when you want to persist the data.

For example,  
If you restart a database container,  
You might not want to start with an empty database.

So, how do you persist files?

## Container volumes

Volumes are a storage mechanism,  
That provide the ability to persist data,  
Beyond the lifecycle of an individual container.

Think of it like providing a shortcut or symlink from inside the container to outside the container.

As an example,  
Imagine you create a volume named `log-data`.

```bash
docker volume create log-data
```

When starting a container with the following command,  
The volume will be mounted (or attached) into the container at `/logs`:

```bash
docker run -d -p 80:80 -v log-data:/logs docker/welcome-to-docker
```

If the volume `log-data` doesn't exist,  
Docker will automatically create it for you.

When the container runs,  
All files it writes into the `/logs` folder will be saved in this volume,  
Outside of the container.

If you delete the container and start a new container using the same volume, the files will still be there.
