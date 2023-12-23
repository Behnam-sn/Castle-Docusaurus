---
sidebar_position: 2
---

# Iterative

## What is Iterative Software Development Process?

The **iterative** style breaks down a project by subsets of functionality.

You might take a year and break it into 3-month iterations.  
In the first iteration, you'd take a quarter of the requirements,  
And do the complete software life cycle for that quarter:  
Analysis, design, code, and test.

At the end of the first iteration, you'd have a system that does a quarter of the needed functionality.  
Then you'd do a second iteration so that at the end of 6 months,  
You'd have a system that does half the functionality.

With iteration,  
You usually see some form of exploration activity before the true iterations begin.

At the very least, this will get a high-level view of the requirements.  
At least enough to break the requirements down into the iterations that will follow.  
Some high-level design decisions may occur during exploration too.

At the other end,  
Although each iteration should produce production-ready integrated software,  
It often doesn't quite get to that point and needs a stabilization period to iron out the last bugs.

Also, some activities, such as user training, are left to the end.

You may well not put the system into production at the end of each iteration,  
But the system should be of production quality.

However, often you can put the system into production at regular intervals.  
This is good because you get value from the system earlier and you get better-quality feedback.

In this situation,  
You often hear of a project having multiple **releases**,  
Each of which is broken down into several **iterations**.

## Variations

Iterative development has come under many names:  
Incremental, spiral, evolutionary, and jacuzzi spring to mind.

Various people make distinctions among them,  
But the distinctions are neither widely agreed an nor that important compared to the iterative/waterfall dichotomy.

## Hybrid

You can have hybrid approaches.

McConnell describes the staged delivery life cycle,  
Whereby analysis and high-level design are done first, in a waterfall style.  
And then the coding and testing are divided up into iterations.

Such a project might have 4 months of analysis and design followed by four 2 month iterative builds of the System.

## Time Boxing

In iterative development,  
It is particularly important that each iteration produces tested, integrated code that is as close to production quality as possible.

Testing and integration are the hardest activities to estimate,  
So it's important not to have an open-ended activity like that at the end of the project.

A common technique with iterations is to use **time boxing**.  
This forces an iteration to be a fixed length of time.

If it appears that you can't build all you intended to build during an iteration,  
You must decide to slip some functionality from the iteration.  
You must not slip the date of the iteration.

Most projects that use iterative development use the same iteration length throughout the project.  
That way, you get a regular rhythm of builds.

Time boxing is challenging,  
Because people usually have difficulty slipping functionality.

By practicing slipping function regularly,  
They are in a better Position to make an intelligent choice at a big release between slipping a date and slipping function.

Slipping function during iterations is also effective at helping people learn what the real requirements priorities are.

## Rework

One of the most common concerns about iterative development is the issue of rework.  
Iterative development explicitly assumes that you will be reworking and deleting existing code during the later iterations of a project.

In many domains, such as manufacturing, rework is seen as a waste.  
But software isn't like manufacturing.  
As a result, it often is more efficient to rework existing code than to patch around code that was poorly designed.

A number of technical practices can greatly help make rework be more efficient.

- **Automated regression tests** help by allowing you to quickly detect any defects that may have been introduced when you are changing things.  
  A good rule of thumb is that the size of your unit test code should be about the same size as your production code.

- **Refactoring** is a disciplined technique for changing existing software.  
  Refactoring works by using a series of small behavior preserving transformations to the code base.  
  Many of these transformations can be automated.

- **Continuous integration** keeps a team in sync to avoid painful integration cycles.  
  At the heart of this lies a fully automated build process that can be kicked off automatically whenever any member of the team checks code into the code base.  
  Developers are expected to check in daily,  
  So automated builds are done many times a day.  
  The build process includes running a large block of automated regression tests so that any inconsistencies are caught quickly so they can be fixed easily.

All these technical practices have been popularized recently by **Extreme Programming**,  
Although they were used before and can, and should, be used whether or not you use XP or any other agile process.

## Iterative and Waterfall Processes

One of the biggest debates about process is that between waterfall and iterative styles.  
The terms often get misused, particularly as iterative is seen as fashionable,  
While the waterfall process seems to wear plaid trousers.  
As a result, many projects claim to do iterative development but are really doing waterfall.

The essential difference between the two is how you break up a project into smaller chunks.  
If you have a project that you think will take a year,  
Fewer people are comfortable telling the team to go away for a year and to come back when done.  
Some breakdown is needed so that people can approach the problem and track progress.

## References

- UML Distilled 3rd Edition - Martin Fowler - Addison-Wesley
