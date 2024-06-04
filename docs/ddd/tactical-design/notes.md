# Notes

## Conclusion

This chapter explained the event sourcing pattern and its application for modeling the dimension of time in the domain model’s aggregates.

In an event-sourced domain model,  
All changes to an aggregate’s state are expressed as a series of domain events.

That’s in contrast to the more traditional approaches in which a state change just updates a record in the databases.  
The resultant domain events can be used to project the aggregate’s current state.

Moreover, the event-based model gives us the flexibility to project the events into multiple representation models, each optimized for a specific task.

This pattern fits cases in which it’s crucial to have deep insight into the system’s data,  
Whether for analysis and optimization or because an audit log is required by law.

This chapter completes our exploration of the different ways to model and implement
business logic. In the next chapter, we will shift our attention to patterns belonging to
a higher scope: architectural patterns.

state-based and event-sourced aggregates

## Why “Event-Sourced Domain Model”?
