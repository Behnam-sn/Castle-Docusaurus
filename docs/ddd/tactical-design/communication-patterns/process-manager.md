---
sidebar_position: 4
---

# Process Manager

The saga pattern manages simple, linear flow.  
Strictly speaking, a saga matches events to the corresponding commands.

In the examples we used to demonstrate saga implementations,  
We actually implemented simple matching of events to commands:

- `CampaignActivated` event to `PublishingService.SubmitAdvertisement` command
- `PublishingConfirmed` event to `Campaign.TrackConfirmation` command
- `PublishingRejected` event to `Campaign.TrackRejection` command

The process manager pattern,  
Is intended to implement a business-logic-based process.

It is defined as a central processing unit,  
That maintains the state of the sequence and determines the next processing steps.

As a simple rule of thumb,  
If a saga contains if-else statements to choose the correct course of action,  
It is probably a process manager.

Another difference between a process manager and a saga is,  
That a saga is instantiated implicitly when a particular event is observed,
As in `CampaignActivated` in the preceding examples.

A process manager, on the other hand, cannot be bound to a single source event.  
Instead, it’s a coherent business process consisting of multiple steps.

Hence, a process manager has to be instantiated explicitly.  
Consider the following example:

- Booking a business trip starts with the routing algorithm choosing the most cost effective flight route,  
  And asking the employee to approve it.
- In case the employee prefers a different route,  
  Their direct manager needs to approve it.
- After the flight is booked,  
  One of the pre-approved hotels has to be booked for the appropriate dates.
- If no hotels are available,  
  The flight tickets have to be canceled.

In this example, there is no central entity to trigger the trip booking process.  
The trip booking is the process and it has to be implemented as a process manager.

From an implementation perspective,  
Process managers are often implemented as aggregates,  
Either state based or event sourced.  
For example:

```cs
public class BookingProcessManager
{
    private readonly IList<IDomainEvent> _events;
    private BookingId _id;
    private Destination _destination;
    private TripDefinition _parameters;
    private EmployeeId _traveler;
    private Route _route;
    private IList<Route> _rejectedRoutes;
    private IRoutingService _routing;

    public void Initialize(Destination destination, TripDefinition parameters, EmployeeId traveler)
    {
        _destination = destination;
        _parameters = parameters;
        _traveler = traveler;
        _route = _routing.Calculate(destination, parameters);

        var routeGenerated = new RouteGeneratedEvent(
            BookingId: _id,
            Route: _route);

        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestEmployeeApproval(_traveler, _route)
        );

        _events.Append(routeGenerated);
        _events.Append(commandIssuedEvent);
    }

    public void Process(RouteConfirmed confirmed)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new BookFlights(_route, _parameters)
        );

        _events.Append(confirmed);
        _events.Append(commandIssuedEvent);
    }

    public void Process(RouteRejected rejected)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestRerouting(_traveler, _route)
        );

        _events.Append(rejected);
        _events.Append(commandIssuedEvent);
    }

    public void Process(ReroutingConfirmed confirmed)
    {
        _rejectedRoutes.Append(route);
        _route = _routing.CalculateAltRoute(destination,
                                            parameters, rejectedRoutes);
        var routeGenerated = new RouteGeneratedEvent(
            BookingId: _id,
            Route: _route);

        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestEmployeeApproval(_traveler, _route)
        );

        _events.Append(confirmed);
        _events.Append(routeGenerated);
        _events.Append(commandIssuedEvent);
    }

    public void Process(FlightBooked booked)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new BookHotel(_destination, _parameters)
        );

        _events.Append(booked);
        _events.Append(commandIssuedEvent);
    }
}
```

In this example, the process manager has its explicit ID and persistent state,
describing the trip that has to be booked.

As in the earlier example of a saga pattern,  
The process manager subscribes to events that control the workflow,
(RouteConfirmed, RouteRejected, ReroutingConfirmed, etc.),

and it instantiates events of type `CommandIssuedEvent` that will be processed by an outbox relay to execute the actual commands.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
