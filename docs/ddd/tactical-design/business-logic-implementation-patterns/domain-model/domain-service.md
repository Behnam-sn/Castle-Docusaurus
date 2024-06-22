---
sidebar_position: 5
---

# Domain Service

## What is a Domain Service?

A domain service is a stateless object that implements business logic.  
In the vast majority of cases,  
Such logic orchestrates calls,  
To various components of the system,  
To perform some calculation or analysis.

:::note
It is important to point out that domain services have nothing to do with microservices,  
Service-oriented architecture, or almost any other use of the word service in software engineering.

It is just a stateless object used to host business logic.
:::

## What Problem Domain Service is Trying to Solve?

You will encounter business logic,  
That doesn’t belong to any aggregate or value object,  
Or that seems to be relevant to multiple aggregates.

In such cases, domain-driven design proposes to implement the logic as a domain service.

## How to Implement Domain Service?

Let’s go back to the example of the `Ticket` aggregate:

- Recall that the assigned agent has a limited time frame in which to propose a solution to the customer.
- The time frame depends not only on the ticket’s data (its priority and escalation status),
- But also on the agent’s department policy,  
  Regarding the SLAs for each priority and the agent’s work schedule (shifts),  
  We can’t expect the agent to respond during off-hours.

The response time frame calculation logic requires information from multiple sources:

- The ticket
- the assigned agent’s department
- And the work schedule

That makes it an ideal candidate to be implemented as a domain service:

```cs
public class ResponseTimeFrameCalculationService
{
    public ResponseTimeFrame CalculateAgentResponseDeadline(UserId agentId, Priority priority, bool escalated, DateTime startTime)
    {
        var policy = _departmentRepository.GetDepartmentPolicy(agentId);
        var maxProcTime = policy.GetMaxResponseTimeFor(priority);

        if (escalated)
        {
            maxProcTime = maxProcTime * policy.EscalationFactor;
        }

        var shifts = _departmentRepository.GetUpcomingShifts(agentId, startTime, startTime.Add(policy.MaxAgentResponseTime));

        return CalculateTargetTime(maxProcTime, shifts);
    }
}
```

## Domain Service Challenges

Domain services make it easy to coordinate the work of multiple aggregates.

However, it is important to always keep in mind the aggregate pattern’s limitation of modifying only one instance of an aggregate in one database transaction.

Domain services are not a loophole around this limitation.  
The rule of one instance per transaction still holds true.

Instead, domain services lend themselves to implementing calculation logic,  
That requires reading the data of multiple aggregates.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
