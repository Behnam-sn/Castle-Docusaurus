# UML

## What is the UML?

The Unified Modeling Language (UML) is a family of graphical notations,  
Backed by single meta-model,  
That help in describing and designing software systems.  
Particularly software systems built using the object-oriented (OO) style.

That's a somewhat simplified definition.  
In fact, the UML is a few different things to different people.

This comes both from its own history,  
And from the different views that people have about what makes an effective software engineering process.

## Why Bother with the UML?

Graphical design notations have been with us for a while.  
Their primary value is in communication and understanding.

A good diagram can often help communicate ideas about a design,  
Particularly when you want to avoid a lot of details.

Diagrams can also help you understand either a software system or a business process.

As part of a team trying to figure out something,  
Diagrams both help understanding and communicate that understanding throughout a team.

The UML's importance comes from its wide use and standardization within the OO development community.  
The UML has become not only the dominant graphical notation within the OO world but also a popular technique in non-OO circles.

## What is the History of The UML?

Graphical modeling languages have been around in the software industry for a long time.

The fundamental driver behind them all is that,  
Programming languages are not at a high enough level of abstraction to facilitate discussions about design.

Despite the fact that graphical modeling languages have been around for a long time,  
There is an enormous amount of dispute in the software industry about their role.

These disputes play directly into how people perceive the role of the UML itself.

The UML is a relatively open standard,  
Controlled by the Object Management Group (OMG), an open consortium of companies.

The OMG was formed to build standards that supported interoperability, specifically the interoperability of object-oriented systems.  
The OMG is perhaps best known for the CORBA (Common Object Request Broker Architecture) standards.

The UML was born out of the unification of the many object-oriented graphical modeling languages,  
That thrived in the late 1980s and early 1990s.

Since its appearance in 1997,  
It has relegated that particular tower of Babel to history.

## What is New UML 2?

UML 2 has added a lot of new stuff,  
Including several new diagram types.

Even familiar diagrams have a lot of new notation,  
Such as interaction frames in sequence diagrams

## Ways of Using the UML

At the heart of the role of the UML in software development are the different ways in which people want to use it,  
Differences that carry over from other graphical modeling languages.

These differences lead to long and difficult arguments about how the UML should be used.

To untangle this, Steve Mellor and Martin Fowler independently came up  
With a characterization of the three modes in which people use the UML:

- Sketch
- Blueprint
- Programming Language

### UML as Sketch

By far the most common of the three, at least to my biased eye, is **UML as sketch**.

In this usage, developers use the UML to help communicate some aspects of a system.

As with blueprints, you can use sketches in a forward-engineering or reverse-engineering direction.  
Forward engineering draws a UML diagram before you write code,  
While reverse engineering builds a UML diagram from existing code in order to help understand it.

The essence of sketching is selectivity.  
With forward sketching,  
You rough out some issues in code you are about to write,  
Usually discussing them with a group of people an your team.

Your aim is to use the sketches to help communicate ideas and alternatives about what you're about to do.  
You don't talk about all the code you are going to work on,  
Only important issues that you want to run past your colleagues first or sections of the design that you want to visualize before you begin programming.

Sessions like this can be very short,  
A 10-minute session to discuss a few hours of programming or a day to discuss a 2-week iteration.

With reverse engineering,  
You use sketches to explain how some part of a system works.  
You don't show every class,  
Simply those that are interesting and worth talking about before you dig into the code.

Because sketching is pretty informal and dynamic,  
You need to do it quickly and collaboratively,  
So a common medium is a whiteboard.

Sketches are also useful in documents,  
In which case the focus is communication rather than completeness.

The tools used for sketching are lightweight drawing tools,  
And often people aren't too particular about keeping to every strict rule of the UML.

### UML as Blueprint

In contrast, UML as blueprint is about completeness.

In forward engineering,  
The idea is that blueprints are developed by a designer whose job is to build a detailed design for a programmer to code up.

That design should be sufficiently complete in that all design decisions are laid out,  
And the programmer should be able to follow it as a pretty straightforward activity that requires little thought.

The designer may be the same person as the programmer,  
But usually the designer is a more senior developer who designs for a team of programmers.

The inspiration for this approach is other forms of engineering in which Professional engineers create engineering drawings that are handed over to construction companies to build.

Blueprinting may be used for all details,  
Or a designer may draw blueprints to a particular area.

A common approach is for a designer to develop blueprint-level models as far as interfaces of subsystems but then let developers work out the details of implementing those details.

In reverse engineering,  
Blueprints aim to convey detailed information about the code either in paper documents or as an interactive graphical browser.  
The blueprints can show every detail about a class in a graphical form that's easier for developers to understand.

Blueprints require much more sophisticated tools than sketches do in order to handle the details required for the task.  
Specialized CASE (computer-aided software engineering) tools fall into this category,

Although the term CASE has become a dirty word, and vendors try to avoid it now.

Forward-engineering tools support diagram drawing and back it up with a repository to hold the information.  
Reverse-engineering tools read source code and Interpret from it into the repository and generate diagrams.  
Tools that can do both forward and reverse engineering like this are referred to as **round-trip** tools.

Some tools use the source code itself as the repository and use diagrams as a graphic viewport an the code.  
These tools tie muck more closely into programming and often integrate directly with programming editors.  
I like to think of these as **trip-less** tools .

The line between blueprints and Sketches is somewhat blurry,

But the distinction,  
Rests an the fact that sketches are deliberately incomplete,  
High-lighting important information.

While blueprints intend to be comprehensive,  
Often with the aim of reducing programming to a simple and fairly mechanical activity.

In a sound bite,  
Sketches are explorative,  
While blueprints are definitive.

### UML as Programming Language

As you do more and more in the UML and the programming gets increasingly mechanical,  
It becomes obvious that the programming should be automated.

Indeed, many CASE tools do some form of code generation,  
Which automates building a significant part of a system.

Eventually, however, you reach the point at which all the System can be specified in the UML,  
And you reach **UML as programming language**.

In this environment,  
Developers draw UML diagrams that are compiled directly to executable code,  
And the UML becomes the source code.

Obviously, this usage of UML demands particularly sophisticated tooling.

Also, the notions of forward and reverse engineering don't make any sense for this mode,  
As the UML and source code are the same thing.

#### What is the MDA?

When people talk about the UML,  
They also often talk about **Model Driven Architecture (MDA)**.

Essentially, MDA is a Standard Approach to using the UML as a programming language.

The standard is controlled by the OMG, as is the UML.  
By producing a modeling environment that conforms to the MDA,  
Vendors can create models that can also work with other MDA-compliant environments.

MDA is often talked about in the same breath as the UML,  
Because MDA uses the UNlL as its basic modeling language.  
But, of course, you don't have to be using MDA to use the UML.

MDA divides development work into two main areas.  
Modelers represent a particular application by creating a **Platform Independent Model (PIM)**.  
The PIM is a UML model that is independent of any particular technology.  
Tools can then turn a PIM into a **Platform Specific Model (PSM)**.

The PSM is a model of a system targeted to a specific execution environment.  
Further tools then take the PSM and generate code tor that platform.  
The PSM could be UML but doesn't have to be.

So if you want to build a warehousing system using MDA, you would start bv creating a single PIM of your warehousing system.

If you then wanted this warehousing system to run an J2EE and .NET, you would use some vendor tools to create two PSMs : one for each platform.  
Then further tools would generate code tor the two platforms.

If the process of going from PIM to PSM to final code is completely automated,  
We have the UML as programming language.  
If any of the steps is manual, we have blueprints.

#### Executable UML

Steve Mellor has long been active in this kind of work and has recently used the term **Executable UML**.
Executable UML is similar to MDA hut uses slightly different terms.

Similarly, You begin with a platform-independent model that is equivalent to MDA's PIM.
However, the next step is to use a Model Compiler to turn that UML model into a deployable system in a single step.  
hence, there's no need for the PSM.  
As the term compiler suggests, this step is completely automatic.

The model compilers are based ou reusable archetypes.  
An archetype describes how to take an executable UML model and turn it into a particular programming platform.
So for the warehousing example,  
You would buy a model compiler and two archetypes (J2FE and .NET).  
Run each archetype on your executable UML model, and you have your two versions of the warehousing system.

Executable UML does not use the full UML Standard;  
many constructs of UML are considered to be unnecessary and are therefore not used.  
As a result, Executable UML is simpler than Full UML.

All this Sounds good, but how realistic is it?  
In mv view, there are two issues here.  
First is the question of the tools:  
Whether they are mature enough to do the job.  
This is something that changes over time;  
Certainly, as I write this, they aren't widely used, and I haven't seen much of them in action.

A more fundamental issue iS the whole notion of the LTML as a programming language . In m y view, it's worth using the 1 hII . a s a programming language only if it results in something that's signihcaittly more
productive than using another programming language . 1'm not convinced
that it is, based an various graphical development enviromnents Pve
worked with in the Aast. Even if it is more productive, it still needs to get a
critical mass of users for it to make the mainstream . That's a big hurdle in
itself. Like many,old Smalltalkers, 1 consider Smalltalk to he rauch more
productive than current mainstream langvages . But as Sm illtalk is now
only a niche language, 1 don°t see tnany projects usiiig it . To > avoid Smalltalk's fate, the UML has to be luckier, even if it is superior.

## References

- UML Distilled 3rd Edition - Martin Fowler - Addison-Wesley
