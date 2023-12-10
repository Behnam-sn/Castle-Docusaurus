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

A more fundamental issue is the whole notion of the UML as a programming language.  
In m y view, it's worth using the UML as a programming language only if it results in something that's significantly more productive than using another programming language.  
I'm not convinced that it is, based an various graphical development environments I've worked with in the Past.  
Even if it is more productive, it still needs to get a critical mass of users for it to make the mainstream.  
That's a big hurdle in itself.  
Like many old Smalltalkers, I consider Smalltalk to be much more productive than current mainstream languages.  
But as Smalltalk is now only a niche language, I don't see many projects using it.  
To avoid Smalltalk's fate, the UML has to be luckier, even if it is superior.

One of the interesting questions around the UML as programming language is how to model behavioral logic.  
UML 2 offers three ways of behavioral modeling:  
Interaction diagrams, state diagrams, and activity diagrams.

All have their proponents for programming in.  
If the UML does gain popularity as a programming language,  
It will be interesting to see which of these techniques become successful.

Another way in which people look at the UML is the range between using it for conceptual and for software modeling.  
Most people are familiar with the UML used for Software modeling.  
In this **software perspective**, the elements of the UML map pretty directly to elements in a software system.  
As we shall see, the mapping is by no means prescriptive, but when we use the UML, we are talking about software elements.

With the **conceptual perspective**, the UML represents a description of the concepts of a domain of study.  
Here, we aren't talking about software elements so much as we are building a vocabulary to talk about a particular domain.

There are no hard-and-fast rules about perspective;  
As it turns out, there's really quite a large range of usage.  
Some tools automatically turn source code into the UML diagrams,  
Treating the UML as an alternative view of the source.

That's very much a software perspective.  
If you use UML diagrams to try and understand the various meanings of the terms asset Pool with a bunch of accountants,  
You are in a much more conceptual frame of mind.

review:
In previous editions of this book, 1 split the Software perspective into specifi-
cation (interface) and implementation . In practice, 1 found that it was too hard
to draw a precise line between the two, so 1 feel that the distinction is no longer
worth making a fuss about . However, I'm always inclined to emphasize inter-
face rather than implementation in my diagrams .

These different ways of using the UML lead to a host of arguments about
what UML diagrams mean and what their relationship is to the rest of the
world . In particular, it affects the relationship between the UML and source
code . Some people hold the view that the UML should be used to create a
design that is independent of the programming language that's used for imple-
mentation . Others believe that language-independent design is an oxymoron,
with a strong emphasis an the moron.

Another difference in viewpoints is what the essence of the UML is . In my
view, most users of the UML, particularly sketchers, see the essence of the UML
to be the diagrams . However, the creators of the UML see the diagrams as sec-
ondary; the essence of the UML is the meta-model . Diagrams are simply a pre-
sentation of the meta-model . This view also makes sense to blueprinters and
UML programming language users .
So whenever you read anything involving the UML, it's important to under-
stand the point of view of the author. Only then can you make sense of the
often fierce arguments that the UML encourages .

1 find the UML sketches useful with forward and
reverse engineering and in both conceptual and software perspectives .

I'm not a fan of detailed forward-engineered blueprints ; 1 believe that it's too
difficult to do well and slows down a development effort . Blueprinting to a level
of subsystem interfaces is reasonable, but even then you should expect to
change those interfaces as developers implement the interactions across the
interface . The value of reverse-engineered blueprints is dependent an how the
tool works . If it's used as a dynamic browser, it can be very helpful ; if it gener-
ates a large document, all it does is kill trees .

1 see the UML as programming language as a nice idea but doubt that it will
ever see significant usage . I'm not convinced that graphical forms are more pro-
ductive than textual forms for most programming tasks and that even if they
are, it's very difficult for a language to be widely accepted .

## References

- UML Distilled 3rd Edition - Martin Fowler - Addison-Wesley
