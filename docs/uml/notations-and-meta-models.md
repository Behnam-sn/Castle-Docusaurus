# Notations and Meta-Models

The UML, in its current state, defines a notation and a meta-model.

The **notation** is the graphical stuff you see in models.  
It is the graphical syntax of the modeling language.  
For instance, class diagram notation defines how items and concepts, such as class, association, and multiplicity, are represented.

Of course, this leads to the question of what exactly is meant by an association or multiplicity or even a class.  
Common usage suggests some informal definitions, but many people want more rigor than that.

The idea of rigorous specification and design languages is most prevalent in the field of formal methods.  
In such techniques, designs and specifications are represented using some derivative of predicate calculus.  
Such definitions are mathematically rigorous and allow no ambiguity.  
However, the value of these definitions is by no means universal.  
Even if you can prove that a program satisfies a mathematical specification, there is no way to prove that the mathematical specification meets the real requirements of the system.

Most graphical modeling languages have very little rigor;  
Their notation appeals to intuition rather than to formal definition.  
On the whole, this does not seem to have done much harm.  
These methods may be informal, but many people still find them useful, and it is usefulness that counts.

However, methodologists are looking for ways to improve the rigor of methods without sacrificing their usefulness.  
One way to do this is to define a meta-model: a diagram, usually a class diagram, that defines the concepts of the language.

How muck does the meta-model affect a user of the modeling notation?  
The answer depends mostly an the mode of usage.  
A sketcher usually doesn't care too much.  
A blueprinter should care rather more.  
It's vitally important to those who use the UML as a programming language,  
As it defines the abstract syntax of that language.

Many of the people who are involved in the ongoing development of the UML are interested primarily in the meta-model,  
Particularly as this is important to the usage of the UML and a programming language.  
Notational issues often tun second place,  
Which is important to bear in mind if you ever try to get familiar with the standards documents themselves.

As you get deeper into the more detailed usage of the UML,  
You realize that you need much more than the graphical notation.  
This is why UML tools are so complex.
