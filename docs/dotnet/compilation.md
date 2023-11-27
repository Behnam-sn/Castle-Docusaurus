# Compilation

.NET apps (as written in a high-level language like C#) are compiled into an Intermediate Language (IL).

IL is a compact code format that can be supported on any operating system or architecture.  
Most .NET apps use APIs that are supported in multiple environments, requiring only the .NET runtime to run.

IL needs to be compiled to native code to execute on a CPU, for example, Arm64 or x64.

.NET supports both Ahead-Of-Time (AOT) and Just-In-Time (JIT) compilation models:

- On Android, macOS, and Linux, JIT compilation is the default, and AOT is optional (for example, with ReadyToRun).
- On iOS, AOT is mandatory (except when running in the simulator).
- In WebAssembly (Wasm) environments, AOT is mandatory.

## What is The Advantage of JIT?

The advantage of the JIT is that it can compile an app (unmodified) to the CPU instructions and calling conventions in a given environment, per the underlying operating system and hardware.  
It can also compile code at higher or lower levels of quality to enable better startup and steady-state throughput performance.

## What is The Advantage of AOT?

The advantage of AOT is that it provides the best app startup and can (in some cases) result in smaller deployments.  
The primary downside is that binaries must be built for each separate deployment target (the same as any other native code).  
AOT code is not compatible with some reflection patterns.
