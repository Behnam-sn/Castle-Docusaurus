# Runtime

The Common Language Runtime (CLR) is the foundation all .NET apps are built on.

The fundamental features of the runtime are:

- Garbage collection
- Memory safety and type safety
- High level support for programming languages
- Cross-platform design

.NET is sometimes called a "managed code" runtime.  
It's called managed primarily because it uses a garbage collector for memory management and because it enforces type and memory safety.

The CLR virtualizes (or abstracts) various operating system and hardware concepts, such as memory, threads, and exceptions.

The CLR was designed to be a cross-platform runtime from its inception.  
It has been ported to multiple operating systems and architectures.  
Cross-platform .NET code typically does not need to be recompiled to run in new environments.  
Instead, you just need to install a different runtime to run your app.

The runtime exposes various diagnostics services and APIs for debuggers, dumps and tracing tools, and observability.  
The observability implementation is primarily built around OpenTelemetry, enabling flexible application monitoring and site reliability engineering (SRE).

The runtime offers low-level C-style interop functionality, via a combination of P/Invoke, value types, and the ability to blit values across the native/managed-code boundary.

## Runtime Libraries

.NET has a comprehensive standard set of class libraries.  
These libraries provide implementations for many general-purpose and workload-specific types and utility functionality.

Here are some examples of types defined in the .NET runtime libraries:

<!-- - Every .NET type derives from the System.Object type.
- Primitive value types, such as System.Boolean and System.Int32.
- Collections, such as System.Collections.Generic.List<T> and System.Collections.Generic.Dictionary<TKey,TValue>.
- Data types, such as System.Data.DataSet and System.Data.DataTable.
- Network utility types, such as System.Net.Http.HttpClient.
- File and stream I/O utility types, such as System.IO.FileStream and System.IO.TextWriter.
- Serialization utility types, such as System.Text.Json.JsonSerializer and System.Xml.Serialization.XmlSerializer.
- High-performance types, such as System.Span<T>, System.Numerics.Vector, and Pipelines. -->

For more information, see the Runtime libraries overview.

## CLR

Common Language Runtime.

The exact meaning depends on the context. Common Language Runtime usually refers to the runtime of .NET Framework or the runtime of .NET 5 (and .NET Core) and later versions.

A CLR handles memory allocation and management. A CLR is also a virtual machine that not only executes apps but also generates and compiles code on-the-fly using a JIT compiler.

The CLR implementation for .NET Framework is Windows only.

The CLR implementation for .NET 5 and later versions (also known as the Core CLR) is built from the same code base as the .NET Framework CLR. Originally, the Core CLR was the runtime of Silverlight and was designed to run on multiple platforms, specifically Windows and OS X. It's still a cross-platform runtime, now including support for many Linux distributions.

See also runtime.

CoreRT
In contrast to the CLR, CoreRT is not a virtual machine, which means it doesn't include the facilities to generate and run code on-the-fly because it doesn't include a JIT. It does, however, include the GC and the ability for run-time type identification (RTTI) and reflection. However, its type system is designed so that metadata for reflection isn't required. Not requiring metadata enables having an AOT tool chain that can link away superfluous metadata and (more importantly) identify code that the app doesn't use. CoreRT is in development.

See Intro to CoreRT and .NET Runtime Lab.
