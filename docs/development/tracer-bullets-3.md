# Tracer Bullet Development 3

## What Are Tracer Bullets in Software Development?

### Navigating Uncertainty with Tracer Bullets

We often talk about hitting targets when developing software.  
We’re not actually firing anything at a shooting range,  
but it’s still a useful and visual metaphor.

In particular, it’s interesting to consider how to hit a target in a complex and shifting world.

The answer, of course, depends on the nature of the device you’re aiming with.  
With many, you only get one chance to aim,  
and then you see if you hit the bullseye or not.

But there’s a better way.

### Learning from Real-World Feedback

You know all those movies, TV shows, and video games where people shoot machine guns?  
In these scenes, you often see bright streaks in the air—those are tracer bullets.

Tracer bullets are loaded at intervals alongside regular ammunition.  
When fired,  
Their phosphorus ignites,  
Leaving a pyrotechnic trail from the gun to whatever they hit.

If the tracers are hitting the target,  
Then so are the regular bullets.

Soldiers use these tracer rounds to refine their aim:  
it’s pragmatic, real-time feedback, under actual conditions.

That same principle applies to software projects,  
particularly when you’re building something that hasn’t been built before.

We use the term _tracer bullet development_ to visually illustrate the need for immediate feedback,  
under actual conditions, with a moving goal.

Like the gunners,  
you’re trying to hit a target in the dark.

Because your users have never seen a system like this before,  
Their requirements may be vague.

Because you may be using algorithms, techniques, languages, or libraries you aren’t familiar with,  
You face a large number of unknowns.

And because projects take time to complete,  
you can pretty much guarantee that the environment will change before you’re done.

The classic response is to specify the system to death.  
Produce reams of paper itemizing every requirement,  
Tying down every unknown,  
And constraining the environment.

Fire the gun using dead reckoning.  
One big calculation up front,  
Then shoot and hope.

Pragmatic Programmers, however,  
Prefer using the software equivalent of tracer bullets.

## Why Use Tracer Bullet Development?

### Gaining Immediate Feedback in Real-World Conditions

Tracer bullets work because they operate in the same environment,  
and under the same constraints as real bullets.

They reach the target fast,  
Providing immediate feedback.

From a practical standpoint,  
They’re also a relatively cheap solution.

To achieve the same effect in code,  
We look for something that gets us from a requirement,  
To some aspect of the final system quickly, visibly, and repeatably.

### Reducing Uncertainty and Managing Risks

- Identify the most critical requirements, those that define the system.
- Focus on areas with the most uncertainty and biggest risks.
- Prioritize development in these areas first.

:::note  
With modern projects filled with external dependencies and tools,  
Tracer bullets become even more important.  
:::

For us, the first tracer bullet is simply creating the project,  
adding a “hello world”,  
and ensuring it compiles and runs.

Then we identify uncertainties in the overall application,  
And build the necessary skeleton to make it work.

### Example

In a complex client-server database marketing project,  
we faced many unknowns:

- The client UI used a different language than the backend.
- Queries were stored in Lisp-like notation and converted to SQL.
- The required user experience was unclear.

This was a great opportunity to use tracer code.  
We developed the framework for the front end,  
Libraries for representing the queries,  
And a structure for converting a stored query into a database-specific query.

Then we put it all together and checked that it worked.  
For that initial build,  
All we could do was submit a query that listed all the rows in a table,  
But it proved that the UI could talk to the libraries,  
The libraries could serialize and unserialize a query,  
And the server could generate SQL from the result.

Over the following months we gradually fleshed out this basic structure,  
Adding new functionality by augmenting each component of the tracer code in parallel.

When the UI added a new query type,  
The library grew and the SQL generation was made more sophisticated.

### Tracer Code Is Not Disposable

Unlike prototypes, tracer code is written for keeps.  
It contains all the necessary error handling, structuring, and documentation.  
It’s simply not fully functional yet.

Once you establish an end-to-end connection,  
You can evaluate your accuracy and adjust accordingly.

Once you're on target,  
Adding functionality is easy.

## How to Implement Tracer Bullet Development?

### Establishing an End-to-End Skeleton Early

Instead of building modules in isolation,  
The tracer bullet approach ensures early integration.

By implementing a simple but complete skeleton of the application,  
You create a foundation that allows for incremental improvements.

### Refining Iteratively for Continuous Improvement

This approach is consistent with the idea,  
That a project is never truly finished,  
There will always be changes and new features.

The conventional alternative is a kind of heavy engineering approach:  
Code is divided into modules,  
Which are coded in a vacuum.

Modules are combined into sub-assemblies,  
Which are then further combined,  
Until one day you have a complete application.

Only then can the application as a whole be presented to the user and tested.

## What Are the Benefits of Tracer Bullet Development?

- **Users see progress early**  
  If you have successfully communicated what you are doing,  
  Your users will know they are seeing something immature.  
  They won’t be disappointed by a lack of functionality;  
  They’ll be ecstatic to see some visible progress toward their system.

- **Developers build a structured workflow**  
  If you have worked out all the end-to-end interactions of your application,  
  Then your team won’t need to pull as much out of thin air.

- **Easier integration and debugging**  
  As the system is connected end-to-end,  
  You have an environment to which you can add new pieces of code,  
  Once they have been unit-tested.

  Rather than attempting a big-bang integration,  
  You’ll be integrating every day (often many times a day).

  The impact of each new change is more apparent,  
  And the interactions are more limited,  
  So debugging and testing are faster and more accurate.

- **Always have a working demo**  
  With tracer code,  
  You’ll always have something to show stakeholders and sponsors.

- **Better progress tracking**  
  Developers tackle use cases one by one,  
  making it easier to measure performance and progress.

## What If Tracer Bullets Miss the Target?

### Adapting to Real-World Feedback

Tracer bullets don’t guarantee a perfect hit,  
They show what you’re hitting.

If the first few attempts miss,  
Adjust your aim and refine your approach.

This is the whole point.

By using a lean development methodology,  
You keep changes small,  
So course corrections are easy and quick.

Also users can trust what they see,  
Because every major component is based on reality,  
Not just a theoretical specification.

## Tracer Bullet Development vs. Prototyping

You might think that this tracer code concept,  
Is nothing more than prototyping under an aggressive name.

There is a difference.

### Prototypes: Exploring Ideas, Then Discarding Code

A prototype is meant to test a concept,  
Not serve as the foundation of the final system.

For example:

- You prototype a UI in a visual tool,  
  Then discard it after user feedback.
- You test algorithms in a high-level language,  
  Then rewrite them for performance in a lower-level language.

Prototypes are useful, but they are throwaway experiments.

### Tracer Bullet Development: A Lean and Evolving Foundation

Tracer bullet development, on the other hand,  
Creates a minimal but functional version of the system.

For example, you might implement:

- A simple, first-come, first-served packing algorithm  
  for a shipping application.
- A basic UI that works with the backend,  
  even if it lacks full functionality.

Once all components are connected,  
you refine each piece over time.

The key difference?

- _Prototyping generates disposable code._
- _Tracer code is lean but complete and evolves into the final system._

Think of prototyping as reconnaissance and gathering intelligence before firing the first tracer bullet.

## References

- The Pragmatic Programmer, 2nd Edition – Andrew Hunt & David Thomas
