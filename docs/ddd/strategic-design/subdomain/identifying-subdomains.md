---
sidebar_position: 5
---

# Identifying Subdomains

## Why We Need to Identify Business Subdomains?

Identifying subdomains and their types can help considerably in making different design decisions when building software solutions.

The subdomains and their types are defined by the company’s business strategy:  
Its business domains and how it differentiates itself to compete with other companies in the same field.

## How to Identify Subdomains?

In the vast majority of software projects,  
In one way or another the subdomains are “already there”.  
However That doesn’t mean, it is always easy and straightforward to identify their boundaries.

If you ask a CEO for a list of their company’s subdomains,  
You will probably receive a blank stare.  
They are not aware of this concept.  
Therefore, you’ll have to do the domain analysis yourself to identify and categorize the subdomains at play.

_A good starting point is the company’s departments and other organizational units._

For example, an online retail shop might include:  
Warehouse, customer service, picking, shipping, quality control, and channel management departments, among others.

These, however, are relatively coarse-grained areas of activity.

Take, for example, the customer service department.  
It’s reasonable to assume that it would be a supporting, or even a generic subdomain, as this function is often outsourced to third-party vendors.

But is this information enough for us to make sound software design decisions?

### Distilling Subdomains

Coarse-grained subdomains are a good starting point, but the devil is in the details.  
We have to make sure we are not missing important information hidden in the intricacies of the business function.

Let’s go back to the example of the customer service department.  
If we investigate its inner workings,  
We will see that a typical customer service department is composed of finer-grained components,  
Such as a help desk system, shift management and scheduling, telephone system, and so on.

When viewed as individual subdomains,  
These activities can be of different types:  
While help desk and telephone systems are generic subdomains,  
Shift management is a supporting one,  
While a company may develop its ingenious algorithm for routing incidents to agents having success with similar cases in the past.  
The routing algorithm requires analyzing incoming cases and identifying similarities in past experience—both of which are nontrivial tasks.  
Since the routing algorithm allows the company to provide a better customer experience than its competitors, the routing algorithm is a core subdomain.

On the other hand, we cannot drill down indefinitely, looking for insights at lower and lower levels of granularity.  
When should you stop?

### Subdomains As Coherent Use Cases

From a technical perspective, subdomains resemble sets of interrelated, coherent use cases.

Such sets of use cases usually involve the same actor, the business entities, and they all manipulate a closely related set of data.

We can use the definition of _“subdomains as a set of coherent use cases”_ as a guiding principle for when to stop looking for finer-grained subdomains.  
These are the most precise boundaries of the subdomains.

### When to Stop

Should you always strive to identify such laser-focused subdomain boundaries?  
It is definitely necessary for core subdomains.  
Core subdomains are the most important, volatile, and complex.  
It’s essential that we distill them as much as possible since that will allow us to extract all generic and supporting functionalities and invest the effort on a much more focused functionality.

The distillation can be somewhat relaxed for supporting and generic subdomains.  
If drilling down further doesn’t unveil any new insights that can help you make software design decisions, it can be a good place to stop.  
This can happen, for example, when all of the finer-grained subdomains are of the same type as the original subdomain.

Another important question to consider when identifying the subdomains is whether we need all of them?

### Focus On the Essentials

Subdomains are a tool that alleviates the process of making software design decisions.  
All organizations likely have quite a few business functionalities that drive their competitive advantage but have nothing to do with software.

The jewelry maker we discussed earlier is a example.  
When looking for subdomains, it’s important to identify business functions that are not related to software, acknowledge them as such, and focus on aspects of the business that are relevant to the software system you are working on.

As we discussed earlier, a core subdomain is not necessarily related to software.

Another useful guiding principle for identifying software related core subdomains is to evaluate the complexity of the business logic that you will have to model and implement in code.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
