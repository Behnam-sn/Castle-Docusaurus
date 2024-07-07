---
sidebar_position: 2
---

# Asynchronous Programming

## What is Asynchronous Programming?

Asynchronous in software refers to the occurrence of events,  
Independent of the main program flow;
And ways to deal with such events.

## Why Use Asynchronous Programming?

Asynchronous programming can make the program get more things done in a shorter amount of time.

By using asynchronous programming,  
You can avoid performance bottlenecks.  
And enhance the overall responsiveness of your application.

Asynchrony is essential for activities that are potentially blocking.

Such as web access:  
Accessing to a web resource sometimes is slow or delayed.

If such an activity is blocked in a synchronous process,
The entire application must wait.

In an asynchronous process,
The application can continue with other work that doesn't depend on the web resource,  
Until the potentially blocking task finishes.

## How Asynchronous Programming works?

Blocking methods, execute synchronously,  
And non-blocking methods, execute asynchronously.

A common way for dealing with asynchrony in programming is to:  
Provide subroutines,  
That return a future or promise,  
That represents the ongoing operation,  
And a synchronizing operation,  
That blocks until the future or promise is completed.

## References

- [en.wikipedia.org/wiki/Asynchrony\_(computer_programming)](<https://en.wikipedia.org/wiki/Asynchrony_(computer_programming)>)
- [developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing)
- [www.freecodecamp.org/news/asynchronous-programming-in-javascript/](https://www.freecodecamp.org/news/asynchronous-programming-in-javascript/)
