# Notes

Unlike .NET Framework, .NET 8 assemblies never have a .exe
extension. The .exe that you see after building a .NET 8
application is a platform-specific native loader responsible for
starting your application’s .dll assembly.
.NET 8 also allows you to create a self-contained deployment
that includes the loader, your assemblies, and the required
portions of the .NET runtime—all in a single .exe file. .NET
8 also allows ahead-of-time (AOT) compilation, where the
executable contains precompiled native code for faster startup
and reduced memory consumption.

<!-- ## Default Values

All type instances have a default value.

The default value for the predefined types is the result of a bitwise zeroing of memory:

| Type Default                               | value |
| :----------------------------------------- | :---- |
| Reference types (and nullable value types) | null  |
| Numeric and enum types                     | 0     |
| char type                                  | '\0'  |
| bool type                                  | false |

You can obtain the default value for any type via the default keyword:

```cs
Console.WriteLine(default(decimal)); // 0
```

You can optionally omit the type when it can be inferred:

```cs
decimal d = default;
```

The default value in a custom value type (i.e., struct),
Is the same as the default value for each field defined by the custom type. -->
