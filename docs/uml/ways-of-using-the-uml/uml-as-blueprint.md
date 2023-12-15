---
sidebar_position: 2
---

# UML as Blueprint

In contrast to sketching, UML as blueprint is about completeness.

In forward engineering,  
The idea is that blueprints are developed by a designer,  
Whose job is to build a detailed design for a programmer to code up.

That design should be sufficiently complete in that all design decisions are laid out.  
And the programmer should be able to follow it as a pretty straightforward activity that requires little thought.

The designer may be the same person as the programmer,  
But usually the designer is a more senior developer who designs for a team of programmers.

The inspiration for this approach is other forms of engineering in which Professional engineers create engineering drawings that are handed over to construction companies to build.

Blueprinting may be used for all details,  
Or a designer may draw blueprints to a particular area.

A common approach is for a designer to develop blueprint-level models as far as interfaces of subsystems,  
But then let developers work out the details of implementing those details.

In reverse engineering,  
Blueprints aim to convey detailed information about the code either in paper documents or as an interactive graphical browser.

The blueprints can show every detail about a class in a graphical form that's easier for developers to understand.

Blueprints require much more sophisticated tools than sketches do in order to handle the details required for the task.  
Specialized CASE (computer-aided software engineering) tools fall into this category.

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

## References

- UML Distilled 3rd Edition - Martin Fowler - Addison-Wesley
