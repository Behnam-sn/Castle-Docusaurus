# Build, tag, and publish an image

## Explanation

In this guide,  
You will learn the following:

- Building images  
  The process of building an image based on a Dockerfile.

- Tagging images
  The process of giving an image a name,  
  Which also determines where the image can be distributed.

- Publishing images  
  The process to distribute or share the newly created image using a container registry.

## Building images

Most often,  
Images are built using a Dockerfile.

The most basic docker build command might look like the following:

```bash
docker build .
```

The final `.` in the command provides the path or URL to the build context.

At this location,  
The builder will find the `Dockerfile` and other referenced files.

When you run a build,  
The builder pulls the base image, if needed,  
And then runs the instructions specified in the `Dockerfile`.

With the previous command,  
The image will have no name,  
But the output will provide the ID of the image.

As an example,  
The previous command might produce the following output:

```bash
docker build .
[+] Building 3.5s (11/11) FINISHED                                              docker:desktop-linux
 => [internal] load build definition from Dockerfile                                            0.0s
 => => transferring dockerfile: 308B                                                            0.0s
 => [internal] load metadata for docker.io/library/python:3.12                                  0.0s
 => [internal] load .dockerignore                                                               0.0s
 => => transferring context: 2B                                                                 0.0s
 => [1/6] FROM docker.io/library/python:3.12                                                    0.0s
 => [internal] load build context                                                               0.0s
 => => transferring context: 123B                                                               0.0s
 => [2/6] WORKDIR /usr/local/app                                                                0.0s
 => [3/6] RUN useradd app                                                                       0.1s
 => [4/6] COPY ./requirements.txt ./requirements.txt                                            0.0s
 => [5/6] RUN pip install --no-cache-dir --upgrade -r requirements.txt                          3.2s
 => [6/6] COPY ./app ./app                                                                      0.0s
 => exporting to image                                                                          0.1s
 => => exporting layers                                                                         0.1s
 => => writing image sha256:9924dfd9350407b3df01d1a0e1033b1e543523ce7d5d5e2c83a724480ebe8f00    0.0s
```

With the previous output,  
You could start a container by using the referenced image:

```bash
docker run sha256:9924dfd9350407b3df01d1a0e1033b1e543523ce7d5d5e2c83a724480ebe8f00
```

That name certainly isn't memorable,  
Which is where tagging becomes useful.

## Tagging images

Tagging images is the method to provide an image with a memorable name.  
However, there is a structure to the name of an image.

A full image name has the following structure:

```bash
[HOST[:PORT_NUMBER]/]PATH[:TAG]
```

- `HOST`
  The optional registry hostname where the image is located.  
  If no host is specified,  
  Docker's public registry at `docker.io` is used by default.

- `PORT_NUMBER`
  The registry port number if a hostname is provided.

- `PATH`
  The path of the image,  
  Consisting of slash-separated components.

  For Docker Hub,  
  The format follows `[NAMESPACE/]REPOSITORY`,  
  Where namespace is either a user's or organization's name.

  If no namespace is specified,  
  Library is used,  
  Which is the namespace for Docker Official Images.

- `TAG`  
  A custom and human-readable identifier,  
  That's typically used to identify different versions or variants of an image.

  If no tag is specified,  
  Latest is used by default.

Some examples of image names include:

- `nginx` equivalent to `docker.io/library/nginx:latest`:

  This pulls an image from the `docker.io` registry,  
  The `library` namespace,  
  The `nginx` image repository,  
  And the `latest` tag.

- `docker/welcome-to-docker` equivalent to `docker.io/docker/welcome-to-docker:latest`:

  This pulls an image from the `docker.io` registry,  
  The `docker` namespace,  
  The `welcome-to-docker` image repository,  
  And the `latest` tag.

- `ghcr.io/dockersamples/example-voting-app-vote:pr-311`:

  this pulls an image from the `GitHub Container` Registry,  
  the `dockersamples` namespace,  
  The `example-voting-app-vote` image repository,  
  And the `pr-311` tag.

To tag an image during a build,  
Add the `-t` or `--tag` flag:

```bash
docker build -t my-username/my-image .
```

If you've already built an image,  
You can add another tag to the image,  
By using the docker image tag command:

```bash
docker image tag my-username/my-image another-username/another-image:v1
```

## Publishing images

Once you have an image built and tagged,  
You're ready to push it to a registry.

To do so, use the `docker push` command:

```bash
docker push my-username/my-image
```

Within a few seconds,  
All of the layers for your image will be pushed to the registry.

## References

- [https://docs.docker.com/get-started/docker-concepts/building-images/build-tag-and-publish-an-image/](https://docs.docker.com/get-started/docker-concepts/building-images/build-tag-and-publish-an-image/)
