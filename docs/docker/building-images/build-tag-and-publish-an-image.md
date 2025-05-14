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
