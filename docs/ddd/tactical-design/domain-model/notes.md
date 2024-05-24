# Notes

## What is Domain Model Pattern?

The domain model pattern is intended to cope with cases of complex business logic.
Here, instead of CRUD interfaces, we deal with complicated state transitions, business rules, and invariants: rules that have to be protected at all times.

Let’s assume we are implementing a help desk system.  
Consider the following excerpt from the requirements that describes the logic controlling the lifecycles of support tickets:

- Customers open support tickets describing issues they are facing.
- Both the customer and the support agent append messages.
- And all the correspondence is tracked by the support ticket.
- Each ticket has a priority: low, medium, high, or urgent.
- An agent should offer a solution within a set time limit (SLA) that is based on the ticket’s priority.
- If the agent doesn’t reply within the SLA, the customer can escalate the ticket to the agent’s manager.
- Escalation reduces the agent’s response time limit by 33%.
- If the agent didn’t open an escalated ticket within 50% of the response time limit,  
  It is automatically reassigned to a different agent.
- Tickets are automatically closed if the customer doesn’t reply to the agent’s questions within seven days.
- Escalated tickets cannot be closed automatically or by the agent, only by the customer or the agent’s manager.
- A customer can reopen a closed ticket only if it was closed in the past seven days.

These requirements form an entangled net of dependencies among the different rules,  
All affecting the support ticket’s lifecycle management logic.

This is not a CRUD data entry screen.  
Attempting to implement this logic using active record objects will make it easy to duplicate the logic and corrupt the system’s state by mis-implementing some of the business rules.
