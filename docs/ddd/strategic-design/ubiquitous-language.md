---
sidebar_position: 4
---

# Ubiquitous Language

Effective communication and knowledge sharing are crucial for a successful software project.  
Software engineers have to understand the business domain in order to design and build a software solution.

## Business Problems

The software systems we are building are solutions to business problems.  
In this context, the word problem doesn’t resemble a mathematical problem or a riddle that you can solve and be done with.  
In the context of business domains, “problem” has a broader meaning.

A business problem can be challenges associated with optimizing workflows and processes, minimizing manual labor, managing resources, supporting decisions, managing data, and so on.  
Business problems appear both at the business domain and subdomain levels.

A company’s goal is to provide a solution for its customers’ problems.  
Going back to the FedEx example in Chapter 1, that company’s customers need to ship packages in limited time frames, so it optimizes the shipping process.

## Knowledge Discovery

To design an effective software solution, we have to grasp at least the basic knowledge of the business domain.  
this knowledge belongs to domain experts: it’s their job to specialize in and comprehend all the intricacies of the business domain.

By no means should we, nor can we, become domain experts.  
That said, it’s crucial for us to understand domain experts and to use the same business terminology they use.

To be effective, the software has to mimic the domain experts’ way of thinking about the problem (their mental models).  
Without an understanding of the business problem and the reasoning behind the requirements, our solutions will be limited to “translating” business requirements into source code.  
What if the requirements miss a crucial edge case?
Or fail to describe a business concept and limiting our ability to implement a model that will support future requirements?

As Alberto Brandolini says:

> Software development is a learning process; working code is a side effect.  
> A software project’s success depends on the effectiveness of knowledge sharing between domain experts and software engineers.  
> We have to understand the problem in order to solve it.

Effective knowledge sharing between domain experts and software engineers requires effective communication.  
Let’s take a look at the common impediments to effective communication in software projects.

## Communication

It’s safe to say that almost all software projects require the collaboration of stakeholders in different roles: domain experts, product owners, engineers, UI and UX designers, project managers, testers, analysts, and others.  
As in any collaborative effort, the outcome depends on how well all those parties can work together.  
For example, do all stakeholders agree on what problem is being solved?  
What about the solution they are building do they hold any conflicting assumptions about its functional and non-functional requirements?  
Agreement and alignment on all project-related matters are essential to a project’s success.

Research into why software projects fail has shown that effective communication is essential for knowledge sharing and project success.  
Yet, despite its importance, effective communication is rarely observed in software projects.  
Often, business people and engineers have no direct interaction with one another.  
Instead, domain knowledge is pushed down from domain experts to engineers.  
It is delivered through people playing the role of mediators, or “translators,” systems/business analysts, product owners, and project managers.

During the traditional software development lifecycle,  
the domain knowledge is “translated” into an engineer-friendly form known as an analysis model, which is a description of the system’s requirements rather than an understanding of the business domain behind it.  
While the intentions may be good, such mediation is hazardous to knowledge sharing.  
In any translation, information is lost; in this case, domain knowledge that is essential for solving business problems gets lost on its way to the software engineers.  
This is not the only such translation on a typical software project.  
The analysis model is translated into the software design model (a software design document, which is translated into an implementation model or the source code itself).  
As often happens, documents go out of date quickly.  
The source code is used to communicate business domain knowledge to software engineers who will maintain the project later.

Such a software development process resembles the children’s game Telephone:  
the message, or domain knowledge, often becomes distorted.  
The information leads to software engineers implementing the wrong solution, or the right solution but to the wrong problems.  
In either case, the outcome is the same: a failed software project.  
Domain-driven design proposes a better way to get the knowledge from domain experts to software engineers: by using a ubiquitous language.

The traditional software development lifecycle implies the following translations:

- Domain knowledge into an analysis model
- Analysis model into requirements
- Requirements into system design
- System design into source code

## What Is a Ubiquitous Language?

Domain-driven design’s ubiquitous language is an effective tool for bridging the knowledge gap between domain experts and software engineers.  
It fosters communication and knowledge sharing by cultivating a shared language that can be used by all the stakeholders throughout the project: in conversations, documentation, tests, diagrams, source code, and so on.

Using a ubiquitous language is the cornerstone practice of domain-driven design.  
The idea is simple and straightforward: if parties need to communicate efficiently, instead of relying on translations, they have to speak the same language.

Instead of continuously translating domain knowledge, domain-driven design calls for cultivating a single language for describing the business domain: the ubiquitous language.

All project-related stakeholders—software engineers, product owners, domain experts, UI/UX designers—should use the ubiquitous language when describing the business domain.  
Most importantly, domain experts must be comfortable using the ubiquitous language when reasoning about the business domain; this language will
represent both the business domain and the domain experts’ mental models.  
Only through the continuous use of the ubiquitous language and its terms can a shared understanding among all of the project’s stakeholders be cultivated.

### Language of the Business

It’s crucial to emphasize that the ubiquitous language is the language of the business.  
As such, it should consist of business domain–related terms only. No technical jargon!  
Teaching business domain experts about singletons and abstract factories is not your goal.  
The ubiquitous language aims to frame the domain experts’ understanding and mental models of the business domain in terms that are easy to understand.

### Example

Let’s say we are working on an advertising campaign management system.  
Consider the following statements:

- An advertising campaign can display different creative materials.
- A campaign can be published only if at least one of its placements is active.
- Sales commissions are accounted for after transactions are approved.

All of these statements are formulated in the language of the business.  
That is, they reflect the domain experts’ view of the business domain.  
On the other hand, the following statements are strictly technical and thus do not fit the notion of the ubiquitous language:

- The advertisement iframe displays an HTML file.
- A campaign can be published only if it has at least one associated record in the active-placements table.
- Sales commissions are based on correlated records from the transactions and approved-sales tables.  
  These latter statements are purely technical and will be unclear to domain experts.  
  Suppose engineers are only familiar with this technical, solution-oriented view of the business domain.  
  In that case, they won’t be able to completely understand the business logic or why it operates the way it does, which will limit their ability to model and implement an effective solution.

## What Problem is Ubiquitous Language Trying to Solve?

## What is Ubiquitous Language Solution?

To ensure effective communication, the ubiquitous language has to eliminate ambiguities and implicit assumptions.  
All of a language’s terms have to be consistent no ambiguous terms and no synonymous terms.

Cultivating a ubiquitous language is a continuous process.  
As the project evolves, more domain knowledge will be discovered.  
It’s important for such insights to be reflected in the ubiquitous language.

Tools such as wiki-based glossaries and Gherkin tests can greatly alleviate the process of documenting and maintaining a ubiquitous language. However, the main prerequisite for an effective ubiquitous language is usage: the language has to be used consistently in all project-related communications.

## Consistency

The ubiquitous language must be precise and consistent.  
It should eliminate the need for assumptions and should make the business domain’s logic explicit.  
Since ambiguity hinders communication, each term of the ubiquitous language should have one and only one meaning.  
Let’s look at a few examples of unclear terminology and how it can be improved.

### Ambiguous Terms

Let’s say that in some business domain, the term policy has multiple meanings:  
it can mean a regulatory rule or an insurance contract.  
The exact meaning can be worked out in human-to-human interaction, depending on the context.  
Software, however, doesn’t cope well with ambiguity, and it can be cumbersome and challenging to model the “policy” entity in code.

Ubiquitous language demands a single meaning for each term, so “policy” should be modeled explicitly using the two terms regulatory rule and insurance contract.

### Synonymous Terms

Two terms cannot be used interchangeably in a ubiquitous language.

For example, many systems use the term user.  
However, a careful examination of the domain experts’ lingo may reveal that user and other terms are used interchangeably: for example, user, visitor, administrator, account, etc.

Synonymous terms can seem harmless at first.  
However, in most cases, they denote different concepts.  
In this example, both visitor and account technically refer to the system’s users;  
however, in most systems, unregistered and registered users represent different roles and have different behaviors.  
For example, the “visitors” data is used mainly for analysis purposes, whereas “accounts” actually uses the system and its functionality.  
It is preferable to use each term explicitly in its specific context.  
Understanding the differences between the terms in use allows for building simpler and clearer models and implementations of the business domain’s entities.
