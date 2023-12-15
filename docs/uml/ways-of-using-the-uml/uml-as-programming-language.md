---
sidebar_position: 3
---

# UML as Programming Language

As you do more and more in the UML and the programming gets increasingly mechanical,  
It becomes obvious that the programming should be automated.

Indeed, many CASE tools do some form of code generation,  
Which automates building a significant part of a system.

Eventually, you reach the point at which all the System can be specified in the UML,  
And you reach **UML as programming language**.

In this environment,  
Developers draw UML diagrams that are compiled directly to executable code,  
And the UML becomes the source code.

Obviously, this usage of UML demands particularly sophisticated tooling.

Also, the notions of forward and reverse engineering don't make any sense for this mode,  
As the UML and source code are the same thing.

## What is the MDA?

When people talk about the UML,  
They also often talk about **Model Driven Architecture (MDA)**.

Essentially MDA is a Standard Approach to using the UML as a programming language.

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

## Executable UML

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
