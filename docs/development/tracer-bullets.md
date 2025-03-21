# Tracer Bullets

## What are Tracer Bullets?

We often talk about hitting targets when we develop software.  
We’re not actually firing anything at the shooting range,  
But it’s still a useful and very visual metaphor.

In particular,  
It’s interesting to consider how to hit a target in a complex and shifting world.

The answer, of course,  
Depends on the nature of the device you’re aiming with.  
With many you only get one chance to aim,  
And then get to see if you hit the bullseye or not.

But there’s a better way.

You know all those movies, TV shows, and video games where people are shooting machine guns?  
In these scenes,  
You’ll often see the path of bullets as bright streaks in the air.  
These streaks come from tracer bullets.

Tracer bullets are loaded at intervals alongside regular ammunition.  
When they’re fired,  
Their phosphorus ignites and leaves a pyrotechnic trail from the gun to whatever they hit.

If the tracers are hitting the target,  
Then so are the regular bullets.

Soldiers use these tracer rounds to refine their aim:  
It’s pragmatic, real-time feedback, under actual conditions.

That same principle applies to projects,  
Particularly when you’re building something that hasn’t been built before.

We use the term tracer bullet development,  
To visually illustrate the need for immediate feedback,  
Under actual conditions with a moving goal.

Like the gunners,  
You’re trying to hit a target in the dark.

Because your users have never seen a system like this before,  
Their requirements may be vague.

Because you may be using algorithms, techniques, languages, or libraries you aren’t familiar with,  
You face a large number of unknowns.

And because projects take time to complete,  
You can pretty much guarantee the environment you’re working in will change before you’re done.

The classic response is to specify the system to death.  
Produce reams of paper itemizing every requirement,  
Tying down every unknown,  
And constraining the environment.

Fire the gun using dead reckoning.  
One big calculation up front,  
Then shoot and hope.

Pragmatic Programmers, however,  
Tend to prefer using the software equivalent of tracer bullets.

## Code That Glows in the Dark

Tracer bullets work,  
Because they operate in the same environment,  
And under the same constraints as the real bullets.

They get to the target fast,  
So the gunner gets immediate feedback.  
And from a practical standpoint they’re a relatively cheap solution.

To get the same effect in code,  
We look for something that gets us from a requirement to some aspect of the final system quickly, visibly, and repeatably.

Look for the important requirements,  
The ones that define the system.

Look for the areas where you have doubts,  
And where you see the biggest risks.

Then prioritize your development so that these are the first areas you code.

:::note
In fact,  
Given the complexity of today’s project setup,  
With swarms of external dependencies and tools,  
Tracer bullets become even more important.
:::

For us,  
The very first tracer bullet is simply create the project,  
Add a “hello world!”,  
And make sure it compiles and runs.

Then we look for areas of uncertainty in the overall application,  
And add the skeleton needed to make it work.

Have a look at the following diagram. This system has five architectural layers.
We have some concerns about how they’d integrate, so we look for a simple feature that lets us exercise them together.
The diagonal line shows the path that feature takes through the code.
To make it work, we just have to implement the solidly shaded areas in each layer: the stuff with the squiggles will be done later.

We once undertook a complex client-server database marketing project.
Part of its requirement was the ability to specify and execute temporal queries.
The servers were a range of relational and specialized databases.
The client UI, written in random language A, used a set of libraries written in a different language to provide an interface to the servers.
The user’s query was stored on the server in a Lisp-like notation before being converted to optimized SQL just prior to execution.

There were many unknowns and many different environments, and no one was too sure how the UI should behave.

This was a great opportunity to use tracer code.
We developed the framework for the front end, libraries for representing the queries, and a structure for converting a stored query into a database-specific query.
Then we put it all together and checked that it worked.
For that initial build, all we could do was submit a query that listed all the rows in a table, but it proved that the UI could talk to the libraries, the libraries could serialize and unserialize a query, and the server could generate SQL from the result.
Over the following months we gradually fleshed out this basic structure, adding new functionality by augmenting each component of the tracer code in parallel.
When the UI added a new query type, the library grew and the SQL generation was made more sophisticated.

Tracer code is not disposable: you write it for keeps.
It contains all the error checking, structuring, documentation, and self-checking that any piece of production code has.
It simply is not fully functional.
However, once you have achieved an end-to-end connection among the components of your system, you can check how close to the target you are, adjusting if necessary.
Once you’re on target, adding functionality is easy.

Tracer development is consistent with the idea that a project is never finished:
there will always be changes required and functions to add.
It is an incremental approach.

The conventional alternative is a kind of heavy engineering approach: code is divided into modules, which are coded in a vacuum.
Modules are combined into subassemblies, which are then further combined, until one day you have a complete application.
Only then can the application as a whole be presented to the user and tested.

The tracer code approach has many advantages:

- Users get to see something working early

If you have successfully communicated what you are doing your users will know they are seeing something immature.
They won’t be disappointed by a lack of functionality;
they’ll be ecstatic to see some visible progress toward their system.
They also get to contribute as the project progresses, increasing their buy-in.
These same users will likely be the people who’ll tell you how close to the target each iteration is.

- Developers build a structure to work in

The most daunting piece of paper is the one with nothing written on it.
If you have worked out all the end-to-end interactions of your application, and have embodied them in code, then your team won’t need to pull as much out of thin air.
This makes everyone more productive, and encourages consistency.

- You have an integration platform

As the system is connected end-to-end, you have an environment to which you can add new pieces of code once they have been unit-tested.
Rather than attempting a big-bang integration, you’ll be integrating every day (often many times a day).
The impact of each new change is more apparent, and the interactions are more limited, so debugging and testing are faster and more accurate.

- You have something to demonstrate

Project sponsors and top brass have a tendency to want to see demos at the most inconvenient times.
With tracer code, you’ll always have something to show them.

- You have a better feel for progress

In a tracer code development, developers tackle use cases one by one.
When one is done, they move to the next.
It is far easier to measure performance and to demonstrate progress to your user.
Because each individual development is smaller, you avoid creating those monolithic blocks of code that are reported as 95% complete week after week.

## Tracer Bullets Don’t Always Hit Their Target

Tracer bullets show what you’re hitting.
This may not always be the target.
You then adjust your aim until they’re on target.
That’s the point.

It’s the same with tracer code.
You use the technique in situations where you’re not 100% certain of where you’re going.
You shouldn’t be surprised if your first couple of attempts miss: the user says “that’s not what I meant,’’ or data you need isn’t available when you need it, or performance problems seem likely.
So change what you’ve got to bring it nearer the target, and be thankful that you’ve used a lean development methodology;
a small body of code has low inertia—it is easy and quick to change.
You’ll be able to gather feedback on your application and generate a new, more accurate version quickly and cheaply.
And because every major application component is represented in your tracer code, your users can be confident that what they’re seeing is based on reality, not just a paper specification.

## Tracer Code versus Prototyping

You might think that this tracer code concept is nothing more than prototyping under an aggressive name.
There is a difference.
With a prototype, you’re aiming to explore specific aspects of the final system.
With a true prototype, you will throw away whatever you lashed together when trying out the concept, and recode it properly using the lessons you’ve learned.

For example, say you’re producing an application that helps shippers determine how to pack odd-sized boxes into containers.
Among other problems, the user interface needs to be intuitive and the algorithms you use to determine optimal packing are very complex.

You could prototype a user interface for your end users in a UI tool.
You code only enough to make the interface responsive to user actions.
Once they’ve agreed to the layout, you might throw it away and recode it, this time with the business logic behind it, using the target language.
Similarly, you might want to prototype a number of algorithms that perform the actual packing.

You might code functional tests in a high-level, forgiving language such as Python, and code low-level performance tests in something closer to the machine.
In any case, once you’d made your decision, you’d start again and code the algorithms in their final environment, interfacing to the real world.
This is prototyping, and it is very useful.

The tracer code approach addresses a different problem.
You need to know how the application as a whole hangs together.
You want to show your users how the interactions will work in practice, and you want to give your developers an architectural skeleton on which to hang code.
In this case, you might construct a tracer consisting of a trivial implementation of the container packing algorithm (maybe something like first-come, first-served) and a simple but working user interface.
Once you have all the components in the application plumbed together, you have a framework to show your users and your developers.
Over time, you add to this framework with new functionality, completing stubbed routines.
But the framework stays intact, and you know the system will continue to behave the way it did when your first tracer code was completed.

The distinction is important enough to warrant repeating.
Prototyping generates disposable code.
Tracer code is lean but complete, and forms part of the skeleton of the final system.
Think of prototyping as the reconnaissance and intelligence gathering that takes place before a single tracer bullet is fired.

## References

- The Pragmatic Programmer 2nd Edition - Andrew Hunt, David Thomas - Addison-Wesley
