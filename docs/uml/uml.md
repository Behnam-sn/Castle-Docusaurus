# UML

## Why Bother with the UML?

Graphical design notations have been with us for a while.  
For me, their primary value is in communication and understanding.

A good diagram can often help communicate ideas about a design,  
Particularly when you want to avoid a lot of details .

Diagrams can also help you understand either a software system or a business process.

As part of a team trying to figure out something, diagrams both help understanding and communicate that understanding throughout a team.

The UML's importance comes from its wide use and standardization within the OO development community.  
The UML has become not only the dominant graphical notation within the OO world but also a popular technique in non-00 circles.

## UML 2

UML 2 has added a lot of new stuff, including several new diagram types.  
Even familiar diagrams have a lot of new notation, such as interaction frames in sequence diagrams

## What is the UML?

The Unified Modeling Language (UML) is a family of graphical notations, backed by single meta-model, that help in describing and designing software systems, particularly software systems built using the object-oriented (OO) style.

That's a somewhat simplified definition.  
In fact, the UML is a few different things to different people.

This comes both from its own history and from the different views that people have about what makes an effective software engineering process.

Graphical modeling languages have been around in the software industry for a long time.  
The fundamental driver behind them all is that programming languages are not at a high enough level of abstraction to facilitate discussions about design.

Despite the fact that graphical modeling languages have been around for a long time, there is an enormous amount of dispute in the software industry about their role.  
These disputes play directly into how people perceive the role of the UML itself.

The UML is a relatively open standard, controlled by the Object Management Group (OMG), an open consortium of companies.  
The OMG was formed to build standards that supported interoperability, specifically the interoperability of object-oriented systems.  
The OMG is perhaps best known for the CORBA (Common Object Request Broker Architecture) standards.

The UML was born out of the unification of the many object-oriented graphical modeling languages that thrived in the late 1980s and early 1990s.  
Since its appearance in 1997, it has relegated that particular tower of Babel to history.  
That's a service I, and many other developers, am deeply thankful for.

## Ways of Using the UML

At the heart of the role of the UML in software development are the different ways in which people want to use it, differences that carry over from other graphical modeling languages.  
These differences lead to long and difficult arguments about how the UML should be used.

To untangle this, Steve Mellor and I independently came up with a characterization of the three modes in which people use the UML : sketch, blueprint, and programming language .

By far the most common of the three, at least to my biased eye, is **UML as sketch**.

In this usage, developers use the UML to help communicate some aspects of a system.  
As with blueprints, you can use sketches in a forward-engineering or reverse-engineering direction. Forward engineering draws a UML diagram before you write code, while reverse engineering builds a
UML diagram from existing code in order to help understand it.

The essence of sketching is selectivity .  
With forward sketching, you rough out some issues in code you are about to write, usually discussing them with a group of people an your team.  
Your aim is to use the sketches to help communicate ideas and alternatives about what you're about to do.  
You don't talk about all the code you are going to work on, only important issues that you want to run past your colleagues first or sections of the design that you want to visualize before you begin programming.  
Sessions like this can be very short : a 10-minute session to discuss a few hours of programming or a day to discuss a 2-week iteration.

With reverse engineering, you use sketches to explain how some part of a system works.  
You don't show every class, simply those that are interesting and worth talking about before you dig into the code.

Because sketching is pretty informal and dynamic,  
You need to do it quickly and collaboratively,  
So a common medium is a whiteboard.

Sketches are also useful in documents,  
In which case the focus is communication rather than completeness.

The tools used for sketching are lightweight drawing tools,  
And often people aren't too particular about keeping to every strict rule of the UML.

In contrast, UML as blueprint is about completeness.  
In forward engineering, the idea is that blueprints are developed by a designer whose job is to build a detailed design for a programmer to code up.  
That design should be sufficiently complete in that all design decisions are laid out, and the programmer should be able to follow it as a pretty straightforward activity that requires little thought.  
The designer may be the same person as the programmer, but usually the designer is a more senior developer who designs for a team of programmers.
The inspiration for this approach is other forms of engineering in which Professional engineers create engineering drawings that are handed over to construction companies to build.

Blueprinting may be used for all details,  
Or a designer may draw blueprints to a particular area.  
A common approach is for a designer to develop blueprint-level models as far as interfaces of subsystems but then let developers work out the details of implementing those details.

In reverse engineering, blueprints aim to convey detailed information about the code either in paper documents or as an interactive graphical browser.  
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

But I think the distinction, rests an the fact that sketches are deliberately incomplete,  
High-lighting important information.

While blueprints intend to be comprehensive,  
Often with the aim of reducing programming to a simple and fairly mechanical activity.

In a sound bite, I'd say that sketches are explorative, while blueprints are definitive.

### UML as programming language

As you do more and more in the UML and the programming gets increasingly mechanical,  
It becomes obvious that the programming should be automated.

Indeed, many CASE tools do some form of code generation, which automates building a significant part of a system.  
Eventually, however, you reach the point at which all the System can be specified in the UML,  
And you reach **UML as programming language**.  
In this environment, developers draw UML diagrams that are compiled directly to executable code, and the UML becomes the source code.  
Obviously, this usage of UML demands particularly sophisticated tooling. (Also, the notions of forward and reverse engineering don't make any sense for this mode, as the UML and source code are the same thing.)
