# Test Types

Automated tests are a great way to ensure that the application code does what its authors intend.

## Unit Tests

A unit test is a test that exercises individual software components or methods,  
Also known as a "unit of work."

Unit tests should only test code within the developer's control.  
They don't test infrastructure concerns.

Infrastructure concerns include:

- Interacting with Databases
- File Systems
- Network Resources

## Integration Tests

An integration test differs from a unit test,  
In that it exercises two or more software components' ability to function together,  
Also known as their **Integration**.

These tests operate on a broader spectrum of the system under test,  
Whereas unit tests focus on individual components.

Often, integration tests do include infrastructure concerns.

## Load Tests

A load test aims to determine whether or not a system can handle a specified load.

For example, the number of concurrent users using an application,  
And the app's ability to handle interactions responsively.

## References

- [learn.microsoft.com/en-us/dotnet/core/testing](https://learn.microsoft.com/en-us/dotnet/core/testing/)
