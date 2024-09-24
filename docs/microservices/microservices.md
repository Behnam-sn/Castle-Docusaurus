# Microservices

## Overview

Microservices are an approach to distributed systems,  
That promote the use of finely grained services,  
That can be changed, deployed, and released independently.

For organizations that are moving toward more loosely coupled systems,  
With autonomous teams delivering user-facing functionality,  
Microservices work incredibly well.

Beyond this,  
Microservices provide us with a huge number of options for building out systems,  
Giving us a lot of flexibility to ensure our system can change to meet the needs of the users.

Microservices aren’t without significant downsides, though.

As a distributed system,  
They bring a host of complexity,  
Much of which may be new even to experienced developers.

## What Are Microservices?

Microservices are independently releasable services that are modeled around a business domain.

A service encapsulates functionality and makes it accessible to other services via networks.

You construct a more complex system from these building blocks.  
One microservice might represent inventory, another order management, and yet another shipping,  
But together they might constitute an entire e-commerce system.

Microservices are an architecture choice that is focused on giving you many options for solving the problems you might face.

They are a type of service-oriented architecture,  
Albeit one that is opinionated about how service boundaries should be drawn,  
And one in which independent deployability is key.

They are technology agnostic,  
Which is one of the advantages they offer.

From the outside,  
A single microservice is treated as a black box.

It hosts business functionality on one or more network endpoints (for example, a queue or a REST API),  
Over whatever protocols are most appropriate.

Consumers,  
Whether they’re other microservices or other sorts of programs,  
Access this functionality via these networked endpoints.

Internal implementation details,  
Such as the technology the service is written in,  
Or the way data is stored,  
Are entirely hidden from the outside world.

This means microservice architectures avoid the use of shared databases in most circumstances;  
Instead, each microservice encapsulates its own database where required.

Microservices embrace the concept of information hiding.

Information hiding means hiding as much information as possible inside a component,  
And exposing as little as possible via external interfaces.

This allows for clear separation between what can change easily and what is more difficult to change.

Implementation that is hidden from external parties can be changed freely,  
As long as the networked interfaces the microservice exposes don’t change in a backward-incompatible fashion.

Changes inside a microservice boundary shouldn’t affect an upstream consumer,  
Enabling independent releasability of functionality.

This is essential in allowing our microservices to be worked on in isolation and released on demand.

Having clear and stable service boundaries,  
That don’t change when the internal implementation changes,  
Results in systems that have looser coupling and stronger cohesion.

### Hexagonal Architecture Pattern

While we’re talking about hiding internal implementation detail,  
It would be remiss of me not to mention the Hexagonal Architecture pattern,  
First detailed by Alistair Cockburn.

This pattern describes the importance of keeping the internal implementation separate from its external interfaces,  
With the idea that you might want to interact with the same functionality over different types of interfaces.

I draw my microservices as hexagons partly to differentiate them from “normal” services,  
But also as an homage to this piece of prior art.
