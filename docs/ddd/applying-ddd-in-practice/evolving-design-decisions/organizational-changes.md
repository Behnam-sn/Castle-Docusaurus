---
sidebar_position: 4
---

# Organizational Changes

Another type of change that can affect a system’s design is a change in the organization itself.

look at different patterns of integrating bounded contexts:

- Partnership
- Shared Kernel
- Conformist
- Anticorruption Layer
- Open-Host Service
- Separate Ways

Changes in the organization’s structure can affect teams’ communication and collaboration levels and,  
As a result, the ways the bounded contexts should be integrated.

A trivial example of such change is growing development centers.  
Since a bounded context can be implemented by only one team,  
Adding new development teams can cause the existing wider bounded context boundaries to split into smaller ones so that each team can work on its own bounded context.

Moreover, the organization’s development centers are often located in different geographical locations.  
When the work on the existing bounded contexts is shifted to another location,  
It may negatively impact the teams’ collaboration.

As a result, the bounded contexts’ integration patterns have to evolve accordingly,  
As described in the following scenarios.

## Partnership to Customer–Supplier

The partnership pattern assumes there is strong communication and collaboration among teams.  
As time goes by, that might cease to be the case;

for example,  
When work on one of the bounded contexts is moved to a distant development center.

Such a change will negatively affect the teams’ communication,  
and it may make sense to move away from the partnership pattern toward a customer–supplier relationship.

## Customer–Supplier to Separate Ways

Unfortunately, it’s not uncommon for teams to have severe communication problems.  
The issues might be caused by geographical distance or organizational politics.  
Such teams may experience more and more integration issues over time.

At some point, it may become more cost-effective to duplicate the functionality,  
Instead of continuously chasing one another’s tails.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
