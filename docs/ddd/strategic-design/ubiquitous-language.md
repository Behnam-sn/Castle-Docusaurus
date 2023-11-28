---
sidebar_position: 4
---

# Ubiquitous Language

## What is Ubiquitous Language?

Effective communication and knowledge sharing are crucial for a successful software project.  
Software engineers have to understand the business domain in order to design and build a software solution.

Domain-driven design’s ubiquitous language is an effective tool for bridging the knowledge gap between domain experts and software engineers.

Ubiquitous language fosters communication and knowledge sharing,  
By cultivating a shared language,  
That can be used by all the stakeholders throughout the project,  
In conversations, documentation, tests, diagrams, source code, and so on.

## What Problem Ubiquitous Language is Trying to Solve?

### Knowledge Discovery

The software systems we are building are solutions to business problems.

To design an effective software solution,  
We have to grasp at least the basic knowledge of the business domain.

This knowledge belongs to domain experts.  
It’s their job to specialize in and comprehend all the intricacies of the business domain.

By no means should we, nor can we, become domain experts.  
That said, it’s crucial for us to understand domain experts and to use the same business terminology they use.

Effective knowledge sharing between domain experts and software engineers requires effective communication.

### Communication

It’s safe to say that almost all software projects require the collaboration of stakeholders in different roles: domain experts, product owners, engineers, UI and UX designers, project managers, testers, analysts, and others.

As in any collaborative effort, the outcome depends on how well all those parties can work together.  
For example:

Do all stakeholders agree on what problem is being solved?  
What about the solution they are building?  
Do they hold any conflicting assumptions about its functional and non-functional requirements?

Agreement and alignment on all project-related matters are essential to a project’s success.

Research into why software projects fail has shown that effective communication is essential for knowledge sharing and project success.  
Yet, despite its importance, effective communication is rarely observed in software projects.

### Translation

Often, business people and engineers have no direct interaction with one another.  
Instead, domain knowledge is pushed down from domain experts to engineers.

During the traditional software development lifecycle,  
The domain knowledge is “translated” into an engineer-friendly form known as an analysis model.

Which is a description of the system’s requirements,  
Rather than an understanding of the business domain behind it.

While the intentions may be good, such mediation is hazardous to knowledge sharing.

In any translation, information is lost.  
And in this case,  
Domain knowledge that is essential for solving business problems,  
Gets lost on its way to the software engineers.

This is not the only such translation on a typical software project.  
The traditional software development lifecycle implies the following translations:

- Domain knowledge into an analysis model
- Analysis model into requirements
- Requirements into system design
- System design into source code

As often happens, documents go out of date quickly.  
The source code is used to communicate business domain knowledge to software engineers who will maintain the project later.

To be effective, the software has to mimic the domain experts’ way of thinking about the problem (their mental models).

Without an understanding of the business problem and the reasoning behind the requirements,  
Our solutions will be limited to “translating” business requirements into source code.

What if the requirements miss a crucial edge case?  
Or fail to describe a business concept and limiting our ability to implement a model that will support future requirements?

Such a software development process resembles the children’s game Telephone:  
The message, or domain knowledge, often becomes distorted.

The information leads to software engineers implementing the wrong solution,  
Or the right solution but to the wrong problems.

In either case, the outcome is the same: a failed software project.

Domain-driven design proposes a better way to get the knowledge from domain experts to software engineers:  
By using a ubiquitous language.

## What is Ubiquitous Language Solution?

Using a ubiquitous language is the cornerstone practice of domain-driven design.  
The idea is simple and straightforward:

If parties need to communicate efficiently,  
Instead of relying on translations,  
They have to speak the same language.

Instead of continuously translating domain knowledge,  
Domain-driven design calls for cultivating a single language  
For describing the business domain.

## What is an Example of a Ubiquitous Language?

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
In that case, they won’t be able to completely understand the business logic or why it operates the way it does,  
Which will limit their ability to model and implement an effective solution.

## How To Use Ubiquitous Language?

### Continuous Usage

All project-related stakeholders including software engineers, product owners, domain experts & UI/UX designers should consistently use the ubiquitous language when describing the business domain.

The language should be continuously reinforced throughout the project:  
Requirements, tests, documentation, and even the source code itself should use this language.

Only through the continuous use of the ubiquitous language and its terms can a shared understanding among all of the project’s stakeholders be cultivated.

### Continuous Interaction With Domain Experts

Formulation of a ubiquitous language requires interaction with its natural holders, the domain experts.  
Only interactions with actual domain experts can uncover inaccuracies, wrong assumptions, or an overall flawed understanding of the business domain.

### Language of The Business

It’s crucial to emphasize that the ubiquitous language is the language of the business.  
As such, it should consist of business domain–related terms only. No technical jargon!

Teaching business domain experts about singletons and abstract factories is not your goal.  
The ubiquitous language aims to frame the domain experts’ understanding and mental models of the business domain in terms that are easy to understand.

Domain experts must be comfortable using the ubiquitous language when reasoning about the business domain.  
This language will represent both the business domain and the domain experts’ mental models.

### Modeling the Ubiquitous Language Effectively

When cultivating a ubiquitous language, we are effectively building a model of the business domain.

The model is supposed to capture the domain experts’ mental models and their thought processes about,  
How the business works to implement its function.

The model has to reflect the involved business entities and their behavior, cause and effect relationships, and invariants.

The ubiquitous language we use is not supposed to cover every possible detail of the domain.  
That would be equivalent to making every stakeholder a domain expert.  
Instead, the model is supposed to include just enough aspects of the business domain to make it possible to implement the required system.  
That is, to address the specific problem the software is intended to solve.

### Effective Interaction With Domain Experts

Effective communication between engineering teams and domain experts is vital.  
The importance of this communication grows with the complexity of the business domain.

The more complex the business domain is, the harder it is to model and implement its business logic in code.  
Even a slight misunderstanding of a complicated business domain, or its underlying principles, will inadvertently lead to an implementation prone to severe bugs.

The only reliable way to verify a business domain’s understanding is to converse with domain experts and do it in the language they understand: the language of the business.

### Consistency

To ensure effective communication,  
The ubiquitous language must be precise and consistent.  
The ubiquitous language has to eliminate ambiguities and implicit assumptions.  
All of a language’s terms should have one and only one meaning and no synonymous terms.

Let’s look at a few examples of unclear terminology and how it can be improved:

#### Ambiguous Terms

Let’s say that in some business domain, the term policy has multiple meanings:  
It can mean a regulatory rule or an insurance contract.

The exact meaning can be worked out in human-to-human interaction, depending on the context.  
Software, however, doesn’t cope well with ambiguity,  
And it can be cumbersome and challenging to model the “policy” entity in code.

Ubiquitous language demands a single meaning for each term,  
So “policy” should be modeled explicitly using the two terms regulatory rule and insurance contract.

#### Synonymous Terms

Two terms cannot be used interchangeably in a ubiquitous language.

For example, many systems use the term user.  
However, a careful examination of the domain experts’ lingo may reveal that user and other terms are used interchangeably:  
For example, user, visitor, administrator, account, etc.

Synonymous terms can seem harmless at first.  
However, in most cases, they denote different concepts.

In this example, both visitor and account technically refer to the system’s users;  
however, in most systems, unregistered and registered users represent different roles and have different behaviors.  
For example, the “visitors” data is used mainly for analysis purposes,  
Whereas “accounts” actually uses the system and its functionality.

It is preferable to use each term explicitly in its specific context.  
Understanding the differences between the terms in use,  
Allows for building simpler and clearer models and implementations of the business domain’s entities.

### Continuous Effort

Cultivating a ubiquitous language is a continuous process.  
As the project evolves, more domain knowledge will be discovered.  
It’s important for such insights to be reflected in the ubiquitous language.

It should be constantly validated and evolved.  
Everyday use of the language will, over time, reveal deeper insights into the business domain.  
When such breakthroughs happen,  
The ubiquitous language must evolve to keep pace with the newly acquired domain knowledge.

## Tools of Ubiquitous Language

Tools such as wiki-based glossaries and Gherkin tests can greatly alleviate the process of documenting and maintaining a ubiquitous language.

However, keep in mind the main prerequisite for an effective ubiquitous language is usage.  
The language has to be used consistently in all project-related communications.

Use the tools to support the management of the ubiquitous language,  
But don’t expect the documentation to replace the actual usage.

> Individuals and interactions over processes and tools.  
> — Agile Manifesto

### Wikis

A wiki can be used as a glossary to capture and document the ubiquitous language.

Such a glossary alleviates the onboarding process of new team members,  
As it serves as a go-to place for information about the business domain’s terminology.

It’s important to make glossary maintenance a shared effort.  
When a ubiquitous language is changed, all team members should be encouraged to go ahead and update the glossary.  
That’s contrary to a centralized approach, in which only team leaders or architects are in charge of maintaining the glossary.

### Gherkin Tests

Despite the obvious advantages of maintaining a glossary of project-related terminology, it has an inherent limitation.

Glossaries work best for “nouns”: names of entities, processes, roles, and so on.  
Although nouns are important, capturing the behavior is crucial.

The behavior is not a mere list of verbs associated with nouns,  
But the actual business logic, with its rules, assumptions, and invariants.  
Such concepts are much harder to document in a glossary.

Hence, glossaries are best used in tandem with other tools that are better suited to capture the behavior.  
For example, use cases or Gherkin tests.

Automated tests written in the Gherkin language are not only great tools for capturing the ubiquitous language,  
But also act as an additional tool for bridging the gap between domain experts and software engineers.

Domain experts can read the tests and verify the system’s expected behavior.

For example, see the following test written in the Gherkin language:

```gherkin
Scenario: Notify the agent about a new support case
Given Vincent Jules submits a new support case saying:
"""
I need help configuring AWS Infinidash
"""
When the ticket is assigned to Mr. Wolf
Then the agent receives a notification about the new ticket
```

Managing a Gherkin-based test suite can be challenging at times,  
Especially at the early stages of a project.  
However, it is definitely worth it for complex business domains.

### Static Code Analysis

There are even static code analysis tools that can verify the usage of a ubiquitous language’s terms.

A notable example for such a tool is NDepend.

## Challenges of Ubiquitous Language

In theory, cultivating a ubiquitous language sounds like a simple, straightforward process.  
In practice, it isn’t.

### Missing Knowledge

The only reliable way to gather domain knowledge is to converse with domain experts.

Quite often, the most important knowledge is tacit.  
It’s not documented or codified but resides only in the minds of domain experts.

The only way to access it is to ask questions.

As you gain experience in this practice, you will notice that frequently,  
This process involves not merely discovering knowledge that is already there,  
But rather co-creating the model in tandem with domain experts.

There may be ambiguities and even white spots in domain experts’ own understanding of the business domain.  
For example, defining only the “happy path” scenarios,  
But not considering edge cases that challenge the accepted assumptions.

### Knowledge Confliction

Furthermore, you may encounter business domain concepts that lack explicit definitions.  
Asking questions about the nature of the business domain often makes such implicit conflicts and white spots explicit.  
This is especially common for core subdomains.

In such a case, the learning process is mutual.  
You are helping the domain experts better understand their field.

### Introducing Ubiquitous Language Into an Already Existing Project

When introducing domain-driven design practices to a brownfield project,  
You will notice that there is already a formed language for describing the business domain,  
And that the stakeholders use it.

However, since DDD principles do not drive that language,  
It won’t necessarily reflect the business domain effectively.  
For example, it may use technical terms, such as database table names.

Changing a language that is already being used in an organization is not easy.  
The essential tool in such a situation is patience.  
You need to make sure the correct language is used where it’s easy to control it:  
In the documentation and source code.

### Ubiquitous Language in a not English-Speaking Country

Finally, the question about the ubiquitous language that I am asked often at conferences is what language should we use  
if the company is not in an English-speaking country.

My advice is to at least use English nouns for naming the business domain’s entities.  
This will alleviate using the same terminology in code.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
