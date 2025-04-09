# Good-Enough Software

> Striving to better, oft we mar what’s well.
> Shakespeare, King Lear 1.4

There’s an old(ish) joke about a company that places an order for 100,000 ICs with a Japanese manufacturer.

Part of the specification was the defect rate:  
One chip in 10,000.

A few weeks later the order arrived:  
One large box containing thousands of ICs,  
And a small one containing just ten.

Attached to the small box was a label that read:  
_These are the faulty ones._

If only we really had this kind of control over quality.  
But the real world just won’t let us produce much that’s truly perfect,  
Particularly not bug-free software.

Time, technology, and temperament all conspire against us.

However, this doesn’t have to be frustrating.

As Ed Yourdon described in an article in IEEE Software,  
When good-enough software is best,  
You can discipline yourself to write software that’s good enough,  
Good enough for your users,  
For future maintainers,  
For your own peace of mind.

You’ll find that you are more productive and your users are happier.  
And you may well find that your programs are actually better for their shorter incubation.

Before we go any further,  
We need to qualify what we’re about to say.

The phrase _good enough_ does not imply sloppy or poorly produced code.

All systems must meet their users’ requirements to be successful,  
And meet basic performance, privacy, and security standards.

We are simply advocating that users be given an opportunity to participate in the process of deciding when what you’ve produced is good enough for their needs.

## Involve Your Users in the Trade-Off

Normally you’re writing software for other people.

Often you’ll remember to find out what they want.

But do you ever ask them how good they want their software to be?  
Sometimes there’ll be no choice.

If you’re working on pacemakers, an autopilot, or a low-level library that will be widely disseminated,  
The requirements will be more stringent and your options more limited.

However, if you’re working on a brand-new product,  
You’ll have different constraints.

The marketing people will have promises to keep,  
The eventual end users may have made plans based on a delivery schedule,  
And your company will certainly have cash-flow constraints.

It would be unprofessional to ignore these users’ requirements,  
Simply to add new features to the program,  
Or to polish up the code just one more time.

We’re not advocating panic:  
It is equally unprofessional to promise impossible time scales and to cut basic engineering corners to meet a deadline.

The scope and quality of the system you produce should be discussed as part of that system’s requirements.

## Make Quality a Requirements Issue

Often you’ll be in situations where trade-offs are involved.

Surprisingly, many users would rather use software with some rough edges today,  
Than wait a year for the shiny with bells-and-whistles version.  
And in fact what they will need a year from now may be completely different anyway.

Many IT departments with tight budgets would agree;  
Great software today is often preferable to the fantasy of perfect software tomorrow.

If you give your users something to play with early,  
Their feedback will often lead you to a better eventual solution.

## Know When to Stop

In some ways, programming is like painting.  
You start with a blank canvas and certain basic raw materials.  
You use a combination of science, art, and craft to determine what to do with them.  
You sketch out an overall shape,  
Paint the underlying environment,  
Then fill in the details.

You constantly step back with a critical eye to view what you’ve done.

Every now and then you’ll throw a canvas away and start again.

But artists will tell you that all the hard work is ruined if you don’t know when to stop.  
If you add layer upon layer, detail over detail, the painting becomes lost in the paint.

Don’t spoil a perfectly good program by over-embellishment and over-refinement.  
Move on, and let your code stand in its own right for a while.

It may not be perfect.  
Don’t worry:  
It could never be perfect.

Challenges
• Look at the software tools and operating systems that you use regularly.
Can you find any evidence that these organizations and/or developers
are comfortable shipping software they know is not perfect? As a user,
would you rather (1) wait for them to get all the bugs out, (2) have complex
software and accept some bugs, or (3) opt for simpler software with fewer
defects?
• Consider the effect of modularization on the delivery of software. Will it
take more or less time to get a tightly coupled monolithic block of software
to the required quality compared with a system designed as very loosely
coupled modules or microservices? What are the advantages or disadvan-
tages of each approach?
• Can you think of popular software that suffers from feature bloat? That
is, software containing far more features than you would ever use, each
feature introducing more opportunity for bugs and security vulnerabilities,
and making the features you do use harder to find and manage. Are you
in danger of falling into this trap yourself?

## References

- The Pragmatic Programmer 2nd Edition - Andrew Hunt, David Thomas - Addison-Wesley
