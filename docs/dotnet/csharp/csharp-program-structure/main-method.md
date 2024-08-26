# Main Method

The `Main` method is the entry point of a C# application.

When the application is started,  
The `Main` method is the first method that is invoked.

There can only be one entry point in a C# program.

If you have more than one class that has a `Main` method,  
You must compile your program with the `StartupObject` compiler option to specify which `Main` method to use as the entry point.

```cs
class TestClass
{
    static void Main(string[] args)
    {
        // Display the number of command line arguments.
        Console.WriteLine(args.Length);
    }
}
```

## Overview

- The `Main` method is the entry point of an executable program;  
  It is where the program control starts and ends.

- `Main` must be declared inside a class or struct.  
  The enclosing class can be static.

- `Main` method must be static.

- `Main` can have any access modifier.  
  Except file.

- `Main` can either have a `void`, `int`, `Task`, or `Task<int>` return type.

- If and only if `Main` returns a Task or `Task<int>`,  
  The declaration of `Main` may include the `async` modifier.  
  This specifically excludes an `async void Main` method.

- The `Main` method can be declared with or without a `string[]` parameter,  
  That contains command-line arguments.

  You can add the parameter manually,  
  Or use the `GetCommandLineArgs()` method to obtain the command-line arguments.  
  Parameters are read as zero-indexed command-line arguments.

## Main Method return values

You can return an `int` from the `Main` method by defining the method in one of the following ways:

```cs
static int Main() { }
static int Main(string[] args) { }
static async Task<int> Main() { }
static async Task<int> Main(string[] args) { }
```

If the return value from Main is not used,  
Returning `void` or `Task` allows for slightly simpler code.

```cs
static void Main() { }
static void Main(string[] args) { }
static async Task Main() { }
static async Task Main(string[] args) { }
```

However, returning `int` or `Task<int>` enables the program to communicate status information to other programs or scripts that invoke the executable file.

<!-- The preceding examples don't specify an access modifier,
So they're implicitly private by default.

That's typical, but it's possible to specify any explicit access modifier. -->
