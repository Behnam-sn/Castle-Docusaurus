# Software Engineering

## What is The Definition of Software Engineering?

Software engineering is a branch of both computer science and engineering,  
Focused on designing, developing, testing, and maintaining software applications.

It involves applying **engineering principles** and **computer programming expertise**,  
To develop software systems that meet user needs.

Notable definitions of software engineering include:

- The Bureau of Labor Statistics — IEEE Systems and software engineering – Vocabulary:

  > The systematic application of scientific and technological knowledge, methods, and experience to the design, implementation, testing, and documentation of software.

- IEEE Standard Glossary of Software Engineering Terminology:

  > The application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software.

- Ian Sommerville:

  > An engineering discipline that is concerned with all aspects of software production.

- Fritz Bauer:

  > The establishment and use of sound engineering principles,  
  > In order to economically obtain software that is reliable and works efficiently on real machines.

- Merriam-Webster:

  > A branch of computer science that deals with the design, implementation, and maintenance of complex computer programs.

- Software Engineering at Google:

  > Software engineering' encompasses not just the act of writing code,  
  > But all of the tools and processes an organization uses to build and maintain that code over time.  
  > Software engineering can be thought of as 'programming integrated over time.

The term has also been used less formally:

- As the informal contemporary term for the broad range of activities,  
  That were formerly called computer programming and systems analysis.

- As the broad term for all aspects of the practice of computer programming,  
  As opposed to the theory of computer programming,  
  Which is formally studied as a sub-discipline of computer science.

- As the term embodying the advocacy of a specific approach to computer programming,  
  One that urges that it be treated as an engineering discipline rather than an art or a craft,  
  And advocates the codification of recommended practices.

### Suitability

Individual commentators have disagreed sharply on,  
How to define software engineering,  
Or its legitimacy as an engineering discipline:

- David Parnas:

  > Software engineering is in fact, a form of engineering.

- Steve McConnell:

  > It is not, but that it should be.

- Donald Knuth:

  > Programming is an art and a science.

- Edsger W. Dijkstra:

  > The terms software engineering and software engineer have been misused in the United States.

## History

Beginning in the 1960s,  
Software engineering was recognized as a separate field of engineering.

### Origins

The origins of the term software engineering have been attributed to various sources.

#### Magazines

The term appeared in a list of services offered by companies in the June 1965 issue of _Computers and Automation_,  
And was used more formally in the August 1966 issue of _Communications of the ACM_ (Volume 9, number 8),  
In "President's Letter to the ACM Membership" by Anthony A. Oettinger.

#### NATO

It is also associated with the title of a NATO conference in 1968 by Professor Friedrich L. Bauer.

The development of software engineering was seen as a struggle.  
Problems included:  
Software that was over budget, exceeded deadlines,  
Required extensive debugging and maintenance,  
And unsuccessfully met the needs of consumers or was never even completed.

In 1968,  
NATO held the first software engineering conference,  
Where issues related to software were addressed.  
Guidelines and best practices for the development of software were established.

#### Margaret Hamilton

Margaret Hamilton described the discipline of "software engineering",  
During the Apollo missions to give what they were doing legitimacy.  
At the time there was perceived to be a "software crisis".

Hamilton details her use of the term:

> When I first came up with the term,  
> No one had heard of it before,  
> At least in our world.
>
> It was an ongoing joke for a long time.  
> They liked to kid me about my radical ideas.
>
> It was a memorable day when one of the most respected hardware gurus,  
> Explained to everyone in a meeting that he agreed with me,  
> That the process of building software should also be considered an engineering discipline,  
> Just like with hardware.
>
> Not because of his acceptance of the new "term" per se,  
> But because we had earned his and the acceptance of the others in the room,  
> As being in an engineering field in its own right.

### SEI

In 1984,  
The Software Engineering Institute (SEI) was established,  
As a federally funded research and development center,  
Headquartered on the campus of Carnegie Mellon University in Pittsburgh, Pennsylvania, United States.

Watts Humphrey founded the SEI Software Process Program,  
Aimed at understanding and managing the software engineering process.

The Process Maturity Levels introduced became the Capability Maturity Model Integration for Development (CMMI-DEV),  
Which defined how the US Government evaluates the abilities of a software development team.

Generally accepted best-practices for software engineering have been collected,  
By the ISO/IEC JTC 1/SC 7 subcommittee,  
And published as the Software Engineering Body of Knowledge (SWEBOK).

## Workload

### Requirements Analysis

Requirements engineering is about elicitation, analysis, specification, and validation of requirements for software.

Software requirements can be functional, non-functional or domain:

- #### Functional Requirements

  Describe expected behaviors (i.e. outputs).

- #### Non-functional Requirements

  Specify issues like portability, security, maintainability, reliability, scalability, performance, reusability, and flexibility.

  They are classified into the following types:

  - Interface constraints
  - Performance constraints (such as response time, security, storage space, etc.)
  - Operating constraints
  - Life cycle constraints (maintainability, portability, etc.)
  - And economic constraints

  Knowledge of how the system or software works is needed when it comes to specifying non-functional requirements.

- #### Domain Requirements

  They have to do with the characteristic of a certain category or domain of projects.

### Design

Software design is the process of making high-level plans for the software.

Design is sometimes divided into levels:

- #### Interface Design

  Plans the interaction between a system and its environment,  
  As well as the inner workings of the system.

- #### Architectural Design

  Plans the major components of a system,  
  Including their responsibilities, properties, and interfaces between them.

- #### Detailed Design

  Plans internal elements, including their properties, relationships, algorithms and data structures.

### Construction

Software construction typically involves programming, unit testing, integration testing, and debugging so as to implement the design.

:::note
Testing during this phase is generally performed by the programmer,  
And with the purpose to verify that the code behaves as designed,  
And to know when the code is ready for the next level of testing.
:::

### Testing

Software testing is an empirical, technical investigation,  
Conducted to provide stakeholders with information about the quality of the software under test.

When described separately from construction,  
Testing typically is performed by test engineers or quality assurance instead of the programmers who wrote it.

It is performed at the system level and is considered an aspect of software quality.

### Program Analysis

Program analysis is the process of analyzing computer programs,  
With respect to an aspect such as performance, robustness, and security.

### Maintenance

Software maintenance refers to supporting the software after release.

It may include but is not limited to:  
Error correction, optimization, deletion of unused and discarded features, and enhancement of existing features.

:::note
Usually, maintenance takes up 40% to 80% of project cost.
:::

## Criticism

Some call for licensing, certification and codified bodies of knowledge,  
As mechanisms for spreading the engineering knowledge and maturing the field.

Some claim that the concept of software engineering is so new that it is rarely understood,  
And it is widely misinterpreted,  
Including in software engineering textbooks, papers, and among the communities of programmers and crafters.

Some claim that a core issue with software engineering,  
Is that its approaches are not empirical enough because a real-world validation of approaches is usually absent,  
Or very limited and hence software engineering is often misinterpreted as feasible only in a theoretical environment.

Edsger Dijkstra, a founder of many of the concepts in software development today,  
Rejected the idea of "software engineering" up until his death in 2002,  
Arguing that those terms were poor analogies for what he called the "radical novelty" of computer science:

> A number of these phenomena have been bundled under the name "Software Engineering".  
> As economics is known as "The Miserable Science",  
> Software engineering should be known as "The Doomed Discipline",  
> Doomed because it cannot even approach its goal since its goal is self-contradictory.  
> Software engineering, of course, presents itself as another worthy cause,  
> But that is eyewash:  
> If you carefully read its literature and analyse what its devotees actually do,  
> You will discover that software engineering has accepted as its charter "How to program if you cannot."

## Reference

- [en.wikipedia.org/wiki/Software_engineering](https://en.wikipedia.org/wiki/Software_engineering)
- [www.mtu.edu/cs/undergraduate/software/what](https://www.mtu.edu/cs/undergraduate/software/what/)

### Read Further

- [en.wikipedia.org/wiki/Outline_of_software_engineering](https://en.wikipedia.org/wiki/Outline_of_software_engineering)
