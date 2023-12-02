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
