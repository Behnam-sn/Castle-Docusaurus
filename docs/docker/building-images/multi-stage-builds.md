# Multi-stage builds

## Explanation

In a traditional build,  
All build instructions are executed in sequence,  
And in a single build container:  
Downloading dependencies, compiling code, and packaging the application.

All those layers end up in your final image.

This approach works,  
But it leads to bulky images carrying unnecessary weight and increasing your security risks.

This is where multi-stage builds come in.

Multi-stage builds introduce multiple stages in your Dockerfile,  
Each with a specific purpose.

Think of it like the ability to run different parts of a build in multiple different environments, concurrently.

By separating the build environment from the final runtime environment,  
You can significantly reduce the image size and attack surface.

This is especially beneficial for applications with large build dependencies.

Multi-stage builds are recommended for all types of applications:

- For interpreted languages,  
  Like JavaScript or Ruby or Python,  
  You can build and minify your code in one stage,  
  And copy the production-ready files to a smaller runtime image.

  This optimizes your image for deployment.

- For compiled languages,  
  Like C or Go or Rust,  
  Multi-stage builds let you compile in one stage,  
  And copy the compiled binaries into a final runtime image.

  No need to bundle the entire compiler in your final image.

Here's a simplified example of a multi-stage build structure using pseudo-code.

Notice there are multiple `FROM` statements and a new AS `<stage-name>`.  
In addition, the `COPY` statement in the second stage is copying --from the previous stage.

```dockerfile
# Stage 1: Build Environment
FROM builder-image AS build-stage
# Install build tools (e.g., Maven, Gradle)
# Copy source code
# Build commands (e.g., compile, package)

# Stage 2: Runtime environment
FROM runtime-image AS final-stage
#  Copy application artifacts from the build stage (e.g., JAR file)
COPY --from=build-stage /path/in/build/stage /path/to/place/in/final/stage
# Define runtime configuration (e.g., CMD, ENTRYPOINT)
```

This Dockerfile uses two stages:

- The build stage uses a base image containing build tools needed to compile your application.  
  It includes commands to install build tools, copy source code, and execute build commands.

- The final stage uses a smaller base image suitable for running your application.  
  It copies the compiled artifacts (a JAR file, for example) from the build stage.  
  Finally, it defines the runtime configuration (using CMD or ENTRYPOINT) for starting your application.

## References

- [https://docs.docker.com/get-started/docker-concepts/building-images/multi-stage-builds/](https://docs.docker.com/get-started/docker-concepts/building-images/multi-stage-builds/)
