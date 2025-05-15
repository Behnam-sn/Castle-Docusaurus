# Using the build cache

## Explanation

Consider the following Dockerfile that you created for the getting-started app:

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "./src/index.js"]
```

When you run the docker build command to create a new image,  
Docker executes each instruction in your Dockerfile,  
Creating a layer for each command and in the order specified.

For each instruction,  
Docker checks whether it can reuse the instruction from a previous build.

If it finds that you've already executed a similar instruction before,  
Docker doesn't need to redo it.

Instead, it’ll use the cached result.

This way, your build process becomes faster and more efficient,  
Saving you valuable time and resources.

In order to maximize cache usage,  
And avoid resource-intensive,  
And time-consuming rebuilds,  
It's important to understand how cache invalidation works.

Here are a few examples of situations that can cause cache to be invalidated:

- Any changes to the command of a RUN instruction invalidates that layer.

  Docker detects the change and invalidates the build cache,  
  If there's any modification to a `RUN` command in your Dockerfile.

- Any changes to files copied into the image with the `COPY` or `ADD` instructions.

  Docker keeps an eye on any alterations to files within your project directory.

  Whether it's a change in content or properties like permissions,  
  Docker considers these modifications as triggers to invalidate the cache.

- Once one layer is invalidated,  
  all following layers are also invalidated.

  If any previous layer,  
  Including the base image or intermediary layers,  
  Has been invalidated due to changes,  
  Docker ensures that subsequent layers relying on it are also invalidated.

  This keeps the build process synchronized and prevents inconsistencies.

When you're writing or editing a Dockerfile,  
Keep an eye out for unnecessary cache misses,  
To ensure that builds run as fast and efficiently as possible.

## References

- [https://docs.docker.com/get-started/docker-concepts/building-images/using-the-build-cache/](https://docs.docker.com/get-started/docker-concepts/building-images/using-the-build-cache/)
