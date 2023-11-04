# DDD

Domain-Driven Design

## What is DDD?

Domain-driven design provides a set of practices for a collaborative approach to building software from the perspective of the business.

It was originally invented by Eric Evans in 2003 with
the publication of Domain-Driven Design: Tackling Complexity in the Heart of Software.

## What Problem is DDD Trying to Solve?

Failure to grasp the business domain results in suboptimal implementation of the business software.  
Unfortunately, that’s quite common. According to studies, approximately 70% of software projects are not delivered:

- on time
- on budget
- or according to the client’s requirements

In other words, the vast majority of software projects fail.  
This issue is so deep and widespread that we even have a term for it: software crisis.

The term software crisis was introduced all the way back in 1968.  
One would assume that things would have improved in the intervening 50 years.  
During those years,  
numerous approaches, methodologies, and disciplines were introduced to make software engineering more effective:

- Agile Manifesto
- extreme programming
- test-driven development
- high-level languages
- DevOps
- and others

Unfortunately, things didn’t change much. Projects are still failing quite often and the software crisis is still here.

Many studies have been conducted to investigate the reasons for the common project failures.  
Although researchers have not been able to pinpoint a single cause, most of their findings share a common theme: **communication**.

Communication issues thwarting projects can manifest themselves in different ways; for example:

- unclear requirements
- uncertain project goals
- or ineffective coordination of effort between teams

Yet again, over the years, we have tried to improve inter and intra team communication by introducing new communication opportunities, processes, and mediums. Unfortunately, the success rates of our projects still didn’t change much.

Domain-driven design (DDD) proposes to attack the root cause for failed software projects from a different angle.  
Effective communication is the central theme of the domain-driven design tools and practices.

DDD will make you a more effective software engineer by alleviating the process of making sense of business domains and guiding the design decisions according to the business strategy.  
The tighter the connection between the software design and its business strategy is, the easier it will be to maintain and evolve the system to meet the future needs of the business, ultimately leading to more successful software projects.

## DDD Parts

The domain-driven design (DDD) methodology can be divided into two main parts:

- ### Strategic Design

  The strategic aspect of DDD deals with answering the questions of “what?” and “why?”  
  what software we are building and why we are building it.

- ### Tactical Design

  The tactical part is all about the “how?”  
  how each component is implemented.

Both the strategic and tactical patterns and practices of DDD align software design with its business domain.  
That’s where the name comes from: (business) domain-driven (software) design.

## Analyzing Business Domains

### What Is a Business Domain?

A business domain defines a company’s main area of activity. Generally speaking,  
it’s the service the company provides to its clients. For example:

- FedEx provides courier delivery
- Starbucks is best known for its coffee
- Walmart is one of the most widely recognized retail establishments

A company can operate in multiple business domains. For example:

- Amazon provides both retail and cloud computing services
- Uber is a ride share company that also provides food delivery and bicycle-sharing services

:::tip Note

It’s important to note that companies may change their business domains often. A
canonical example of this is Nokia, which over the years has operated in fields as
diverse as wood processing, rubber manufacturing, telecommunications, and mobile
communications.

:::

### What Is a Subdomain?

A subdomain is a fine-grained area of business activity.  
All of a company’s subdomains form its business domain: the service it provides to its customers.

Implementing a single subdomain is not enough for a company to succeed.  
A company has to operate in multiple subdomains, and the subdomains have to interact with each other to achieve the company’s goals and targets in its business domain.

For example, Star‐
bucks may be most recognized for its coffee, but building a successful coffeehouse
chain requires more than just knowing how to make great coffee. You also have to
buy or rent real estate at effective locations, hire personnel, and manage finances,
among other activities. None of these subdomains on its own will make a profitable
company. All of them together are necessary for a company to be able to compete in
its business domain(s).
