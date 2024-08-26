# C# Program Structure

## General Structure Of A C# Program

C# programs consist of one or more files.  
Each file contains zero or more namespaces.

A namespace contains types,  
Such as classes, structs, interfaces, enumerations, and delegates, or other namespaces.

The following example is the skeleton of a C# program that contains all of these elements:

```cs
using System;

// Your program starts here:
Console.WriteLine("Hello world!");

namespace YourNamespace
{
    class YourClass
    {
    }

    struct YourStruct
    {
    }

    interface IYourInterface
    {
    }

    delegate int YourDelegate();

    enum YourEnum
    {
    }

    namespace YourNestedNamespace
    {
        struct YourStruct
        {
        }
    }
}
```

The preceding example uses top-level statements for the program's entry point.  
Only one file can have top-level statements.

The program's entry point is the first line of program text in that file.

You can also create a static method named Main as the program's entry point,  
As shown in the following example:

```cs
// A skeleton of a C# program
using System;

namespace YourNamespace
{
    class YourClass
    {
    }

    struct YourStruct
    {
    }

    interface IYourInterface
    {
    }

    delegate int YourDelegate();

    enum YourEnum
    {
    }

    namespace YourNestedNamespace
    {
        struct YourStruct
        {
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            //Your program starts here...
            Console.WriteLine("Hello world!");
        }
    }
}
```

## References

- [learn.microsoft.com/en-us/dotnet/csharp/fundamentals/program-structure/](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/program-structure/)
