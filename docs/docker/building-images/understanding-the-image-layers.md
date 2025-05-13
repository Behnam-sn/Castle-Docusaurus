# Understanding the image layers

## Explanation

As you learned in What is an image,  
container images are composed of layers.

And each of these layers, once created, are immutable.

But what does that actually mean?  
And how are those layers used to create the filesystem a container can use?

## Image layers

Each layer in an image contains a set of filesystem changes:  
Additions, deletions, or modifications.

Let’s look at a theoretical image:

- The first layer adds basic commands and a package manager, such as apt.
- The second layer installs a Python runtime and pip for dependency management.
- The third layer copies in an application’s specific requirements.txt file.
- The fourth layer installs that application’s specific dependencies.
- The fifth layer copies in the actual source code of the application.

This is beneficial because it allows layers to be reused between images.

For example,  
Imagine you wanted to create another Python application.

Due to layering,  
You can leverage the same Python base.

This will make builds faster and reduce the amount of storage and bandwidth required to distribute the images.

Layers let you extend images of others by reusing their base layers,  
Allowing you to add only the data that your application needs.

## Stacking the layers

Layering is made possible by content-addressable storage and union filesystems.

While this will get technical,  
Here’s how it works:

- After each layer is downloaded,  
  It is extracted into its own directory on the host filesystem.

- When you run a container from an image,  
  A union filesystem is created where layers are stacked on top of each other,  
  Creating a new and unified view.

- When the container starts,  
  Its root directory is set to the location of this unified directory,  
  Using `chroot`.

When the union filesystem is created,  
In addition to the image layers,  
A directory is created specifically for the running container.

This allows the container to make filesystem changes,  
While allowing the original image layers to remain untouched.

This enables you to run multiple containers from the same underlying image.
