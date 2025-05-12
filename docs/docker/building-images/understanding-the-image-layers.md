# Understanding the image layers

## Explanation

As you learned in What is an image?, container images are composed of layers.

And each of these layers, once created, are immutable.

But, what does that actually mean?  
And how are those layers used to create the filesystem a container can use?

## Image layers

Each layer in an image contains a set of filesystem changes - additions, deletions, or modifications.

Let’s look at a theoretical image:

The first layer adds basic commands and a package manager, such as apt.
The second layer installs a Python runtime and pip for dependency management.
The third layer copies in an application’s specific requirements.txt file.
The fourth layer installs that application’s specific dependencies.
The fifth layer copies in the actual source code of the application.
This example might look like:
