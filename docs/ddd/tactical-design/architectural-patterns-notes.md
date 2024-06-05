# Architectural Patterns Notes

The tactical patterns discussed up to this point in the book defined the different ways to model and implement business logic.

In this chapter, we will explore tactical design decisions in a broader context:  
The different ways to orchestrate the interactions and dependencies between a system’s components.

## Business Logic Versus Architectural Patterns

Business logic is the most important part of software system;  
However, it is not the only part of a software system.

To implement functional and nonfunctional requirements,  
The codebase has to fulfill more responsibilities.

It has to interact with users to gather input and provide output,  
And it has to use different storage mechanisms to persist state,  
And integrate with external systems and information providers.

The variety of concerns that a codebase has to take care of,  
Makes it easy for its business logic,  
To become diffused among the different components.

That is, for some of the logic to be implemented in the user interface or database,  
Or be duplicated in different components.

Lacking strict organization in implementation concerns makes the codebase hard to change.

When the business logic has to change,  
It may not be evident what parts of the codebase have to be affected by the change.

The change may have unexpected effects on seemingly unrelated parts of the system.

Conversely, it may be easy to miss code that has to be modified.

All of these issues dramatically increase the cost of maintaining the codebase.

Architectural patterns introduce organizational principles for the different aspects of a codebase,  
And present clear boundaries between them:  
How the business logic is wired to the system’s input, output, and other infrastructural components.

This affects how these components interact with each other:  
What knowledge they share and how the components reference each other.

Choosing the appropriate way to organize the codebase,  
Or the correct architectural pattern,  
Is crucial to support implementation of the business logic in the short term,  
And alleviate maintenance in the long term.

Let’s explore 3 predominant application architecture patterns and their use cases:

- Layered Architecture
- Ports & Adapters
- CQRS

## Layered Architecture

Layered architecture is one of the most common architectural patterns.

It organizes the codebase into horizontal layers,  
With each layer addressing one of the following technical concerns:

- Interaction with the consumers
- Implementing business logic
- Persisting the data

In its classic form,  
The layered architecture consists of three layers:

- The presentation layer (PL)
- The business logic layer (BLL)
- the data access layer (DAL)

### Presentation Layer

The presentation layer,  
Implements the program’s user interface for interactions with its consumers.

In the pattern’s original form,  
This layer indicate a graphical interface,  
Such as a web interface or a desktop application.

However in modern systems,  
The presentation layer has a broader scope:

That is, all means for triggering the program’s behavior,  
Both synchronous and asynchronous.

For example:

- Graphical user interface (GUI)
- Command-line interface (CLI)
- API for programmatic integration with other systems
- Subscription to events in a message broker
- Message topics for publishing outgoing events

All of these are the means for the system to receive requests from the external environment and communicate the output.

### Business Logic Layer

As the name suggests,  
This layer is responsible for implementing,  
And encapsulating the program’s business logic.

This is the place where business decisions are implemented.  
As Eric Evans says, this layer is the heart of software.

### Data Access Layer

The data access layer provides access to persistence mechanisms.

In the pattern’s original form, this referred to the system’s database.

However, as in the case of the presentation layer,  
The layer’s responsibility is broader for modern systems.

First, ever since the NoSQL revolution broke out,  
it is common for a system to work with multiple databases.  
For example:

- A document store can act as the operational database
- A search index for dynamic queries
- And an in-memory database for performance-optimized operations

Second, traditional databases are not the only medium for storing information.  
For example:

- cloud-based object storage can be used to store the system’s files
- Or a message bus can be used to orchestrate communication between the program’s different functions.

Finally, this layer also includes integration with the various external information providers,  
Needed to implement the program’s functionality:

APIs provided by external systems,  
Or cloud vendors’ managed services,  
Such as language translation, stock market data, and audio transcription.

## Communication Between Layers

The layers are integrated in a top-down communication model:  
Each layer can hold a dependency only on the layer directly beneath it.

This enforces decoupling of implementation concerns and reduces the knowledge shared between the layers.

The presentation layer references only the business logic layer.  
It has no knowledge of the design decisions made in the data access layer.

## Variation

It’s common to see the layered architecture pattern extended with an additional layer:  
The service layer.

### Service layer

> Defines an application’s boundary with a layer of services that establishes a set of available operations and coordinates the application’s response in each operation.
> — Patterns of Enterprise Application Architecture

The service layer acts as an intermediary between the program’s presentation and business logic layers.  
Consider the following code:

```cs
namespace MvcApplication.Controllers
{
    public class UserController: Controller
    {
        [AcceptVerbs(HttpVerbs.Post)]
        public ActionResult Create(ContactDetails contactDetails)
        {
            OperationResult result = null;

            try
            {
                _db.StartTransaction();

                var user = new User();
                user.SetContactDetails(contactDetails)
                user.Save();

                _db.Commit();
                result = OperationResult.Success;
            } catch (Exception ex) {
                _db.Rollback();
                result = OperationResult.Exception(ex);
            }

            return View(result);
        }
    }
}
```

The MVC controller in this example belongs to the presentation layer.  
It exposes an endpoint that creates a new user.  
The endpoint uses the `User` active record object to create a new instance and save it.  
Moreover, it orchestrates a database transaction to ensure that a proper response is generated in case of an error.

To further decouple the presentation layer from the underlying business logic,  
Such orchestration logic can be moved into a service layer.

:::note
It’s important to note that in the context of the architectural pattern,  
The service layer is a logical boundary.  
It is not a physical service.
:::

The service layer acts as a facade for the business logic layer:  
it exposes an interface that corresponds with the public interface’s methods,  
Encapsulating the required orchestration of the underlying layers.

For example:

```cs
interface CampaignManagementService
{
      OperationResult CreateCampaign(CampaignDetails details);
      OperationResult Publish(CampaignId id, PublishingSchedule schedule);
      OperationResult Deactivate(CampaignId id);
      OperationResult AddDisplayLocation(CampaignId id, DisplayLocation newLocation);
}
```

All of the preceding methods correspond to the system’s public interface.  
However, they lack presentation-related implementation details.

The presentation layer’s responsibility becomes limited to providing the required input,  
To the service layer and communicating its responses back to the caller.

Let’s refactor the preceding example and extract the orchestration logic into a service layer:

```cs
namespace MvcApplication.Controllers
{
    public class UserController: Controller
    {[AcceptVerbs(HttpVerbs.Post)]
        public ActionResult Create(ContactDetails contactDetails)
        {
            var result = _userService.Create(contactDetails);
            return View(result);
        }
    }
}
```

```cs
namespace ServiceLayer
{
    public class UserService
    {
        public OperationResult Create(ContactDetails contactDetails)
        {
            OperationResult result = null;

            try
            {
                _db.StartTransaction();

                var user = new User();
                user.SetContactDetails(contactDetails)
                user.Save();

                _db.Commit();
                result = OperationResult.Success;
            } catch (Exception ex) {
                _db.Rollback();
                result = OperationResult.Exception(ex);
            }

            return result;
        }
    }
}
```

Having an explicit service level has a number of advantages:

- We can reuse the same service layer to serve multiple public interfaces;  
  For example, a graphical user interface and an API.  
  No duplication of the orchestration logic is required.
- It improves modularity by gathering all related methods in one place.
- It further decouples the presentation and business logic layers.
- It makes it easier to test the business functionality.

That said, a service layer is not always necessary.

For example,  
When the business logic is implemented as a transaction script,  
It essentially is a service layer,  
As it already exposes a set of methods that form the system’s public interface.  
In such a case,  
The service layer’s API would just repeat the transaction scripts’ public interfaces,  
Without abstracting or encapsulating any complexity.  
Hence, either a service layer or a business logic layer will suffice.

On the other hand,  
The service layer is required if the business logic pattern requires external orchestration,  
As in the case of the active record pattern.  
In this case, the service layer implements the transaction script pattern,  
While the active records it operates on are located in the business logic layer.

#### Terminology

Elsewhere, you may encounter other terms used for the layered architecture:

- Presentation layer = user interface layer
- Service layer = application layer
- Business logic layer = domain layer = model layer
- Data access layer = infrastructure layer

To eliminate confusion, I present the pattern using the original terminology.  
That said, I prefer “user interface layer” and “infrastructure layer” as these terms better reflect the responsibilities of modern systems and an application layer to avoid confusion with the physical boundaries of services.

## When to Use Layered Architecture?

The dependency between the business logic and the data access layers,  
Makes this architectural pattern a good fit for a system with its business logic implemented using the transaction script or active record pattern.

However, the pattern makes it challenging to implement a domain model.

In a domain model, the business entities (aggregates and value objects),  
Should have no dependency and no knowledge of the underlying infrastructure.

The layered architecture’s top-down dependency requires jumping through some hoops to fulfill this requirement.
It is still possible to implement a domain model in a layered architecture,  
But the pattern we will discuss next fits much better.

## Ports & Adapters

The ports & adapters architecture addresses the shortcomings of the layered architecture,  
And is a better fit for implementation of more complex business logic.

Interestingly, both patterns are quite similar.

Let’s “refactor” the layered architecture into ports & adapters.

### Terminology

Essentially, both the presentation layer and data access layer represent integration with external components:  
databases, external services, and user interface frameworks.

These technical implementation details do not reflect the system’s business logic;

so, let’s unify all such infrastructural concerns into a single “infrastructure layer”.

### Dependency Inversion Principle

The dependency inversion principle (DIP),  
States that high-level modules,  
Which implement the business logic,  
Should not depend on low-level modules.

However, that’s precisely what happens in the traditional layered architecture.  
The business logic layer depends on the infrastructure layer.  
To conform with the DIP, let’s reverse the relationship.

Instead of being sandwiched between the technological concerns,  
Now the business logic layer takes the central role.
It doesn’t depend on any of the system’s infrastructural components.

Finally, let’s add an application layer as a facade for the system’s public interface.  
As the service layer in the layered architecture,

It describes all the operations exposed by the system,  
And orchestrates the system’s business logic for executing them.

The result is the ports & adapters architectural pattern.

The business logic doesn’t depend on any of the underlying layers,  
As required for implementing the domain model and event-sourced domain model patterns.

Why is this pattern called ports & adapters?
To answer this question,  
Let’s see how the infrastructural components are integrated with the business logic.

## Integration of Infrastructural Components

The core goal of the ports & adapters architecture is to,  
Decouple the system’s business logic from its infrastructural components.

Instead of referencing and calling the infrastructural components directly,  
The business logic layer defines “ports”,  
That have to be implemented by the infrastructure layer.

The infrastructure layer implements “adapters”:  
Concrete implementations of the ports interfaces for working with different technologies.

The abstract ports are resolved into concrete adapters in the infrastructure layer,  
Either through dependency injection or by bootstrapping.

For example,  
Here is a possible port definition and a concrete adapter for a message bus:

```cs
namespace App.BusinessLogicLayer
{
    public interface IMessaging
    {
        void Publish(Message payload);
        void Subscribe(Message type, Action callback);
    }
}
```

```cs
namespace App.Infrastructure.Adapters
{
    public class SQSBus: IMessaging
    {
    }
}
```

## Variants

The ports & adapters architecture is also known as hexagonal architecture, onion architecture, and clean architecture.

All of these patterns are based on the same design principles,  
Have the same components,  
And have the same relationships between them.

But as in the case of the layered architecture,  
The terminology may differ:

- Application layer = service layer = use case layer
- Business logic layer = domain layer = core layer

Despite that, these patterns can be mistakenly treated as conceptually different.  
That’s just another example of the importance of a ubiquitous language.

## When to Use Ports & Adapters?

The decoupling of the business logic from all technological concerns,  
Makes the ports & adapters architecture a perfect fit for business logic implemented with the domain model pattern.
