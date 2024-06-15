# Domain-Driven Design in the Real World

## Strategic Analysis

Following the order of our exploration of domain-driven design patterns and practices,  
The best starting point for introducing DDD in an organization,  
Is to invest time in understanding the organization’s business strategy,  
And the current state of its systems’ architecture.

### Understand the Business Domain

First, identify the company’s business domain:

- What is the organization’s business domain(s)?
- Who are its customers?
- What service, or value, does the organization provide to customers?
- What companies or products is the organization competing with?

Answering these questions will give you a bird’s-eye view of the company’s high-level goals.

Next, “zoom in” to the domain,  
And look for the business building blocks the organization employs to achieve its high-level goals: the subdomains.

A good initial heuristic is the company’s org chart:  
its departments and other organizational units.

Examine how these units cooperate to allow the company to compete in its business domain.

Furthermore, look for the signs of specific types of subdomains.

#### Core subdomains

To identify the company’s core subdomains, look for what differentiates it from its
competitors:

- Does the company have a “secret sauce” that its competitors lack? For example,
  intellectual property, such as patents and algorithms designed in-house?

- Keep in mind that the competitive advantage, and thus the core subdomains, are
  not necessarily technical. Does the company possess a nontechnical competitive advantage? For example, the ability to hire top-level personnel, produce a unique
  artistic design, and so on?

Another powerful yet unfortunate heuristic for core subdomains is identifying the
worst-designed software components—those big balls of mud that all engineers hate
but the business is unwilling to rewrite from scratch because of the accompanying
business risk. The key here is that the legacy system cannot be replaced with a ready-
made system—it would be a generic subdomain—and any modification to it entails
business risks.

#### Generic subdomains

To identify generic subdomains, look for off-the-shelf solutions, subscription serv‐
ices, or integration of open source software. As you learned in Chapter 1, the same
ready-made solutions should be available to the competing companies, and those
companies leveraging the same solution should have no business impact on your
company.

#### Supporting subdomains

For supporting subdomains, look for the remaining software components that cannot
be replaced with ready-made solutions yet do not directly provide a competitive
advantage. If the code is in rough shape, it triggers less emotional response from soft‐
ware engineers since it changes infrequently. Thus, the effects of the suboptimal soft‐
ware design are not as severe as for the core subdomains.

You don’t have to identify all of the core subdomains. It won’t be practical or even
possible to do so, even for a medium-sized company. Instead, identify the overall
structure, but pay closer attention to the subdomains that are most relevant to the
software systems you are working on.
