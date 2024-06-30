# Deployment

## Deployment Models

.NET apps can be published in two different modes:

- Self-contained apps include the .NET runtime and dependent libraries.  
  They can be single-file or multi-file. Users of the application can run it on a machine that doesn't have the .NET runtime installed.  
  Self-contained apps always target a single operating system and architecture configuration.

- Framework-dependent apps require a compatible version of the .NET runtime, typically installed globally.  
  Framework-dependent apps can be published for a single operating system and architecture configuration or as "portable," targeting all supported configurations.

.NET apps are launched with a native executable, by default.  
The executable is both operating-system and architecture-specific.  
Apps can also be launched with the dotnet command.

Apps can be deployed in containers.  
Microsoft provides container images for various target environments.
