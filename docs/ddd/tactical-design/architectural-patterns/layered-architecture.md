---
sidebar_position: 1
---

# Layered Architecture

## What is Layered Architecture?

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

## Presentation Layer

The presentation layer,  
Implements the program’s user interface for interactions with its consumers.

In the pattern’s original form,  
This layer indicate a graphical interface,  
Such as a web interface or a desktop application.

However in modern systems,  
The presentation layer has a broader scope.  
That includes all means for triggering the program’s behavior;  
Both synchronous and asynchronous.

For example:

- Graphical user interface (GUI)
- Command-line interface (CLI)
- API for programmatic integration with other systems
- Subscription to events in a message broker
- Message topics for publishing outgoing events

All of these are the means for the system to receive requests from the external environment and communicate the output.

## Business Logic Layer

As the name suggests,  
This layer is responsible for implementing and encapsulating the program’s business logic.

As Eric Evans says, this layer is the heart of software.

## Data Access Layer

The data access layer provides access to persistence mechanisms.

In the pattern’s original form,  
This referred to the system’s database.

However, the layer’s responsibility is broader for modern systems.

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
Needed to implement the program’s functionality,  
Like APIs provided by external systems or cloud vendors’ managed services.  
Such as:

- Language translation
- Stock market data
- And audio transcription

## Communication Between Layers

The layers are integrated in a top-down communication model.  
Each layer can hold a dependency only on the layer directly beneath it.

This enforces decoupling of implementation concerns and reduces the knowledge shared between the layers.

The presentation layer references only the business logic layer.  
It has no knowledge of the design decisions made in the data access layer.

## Service layer

It’s common to see the layered architecture pattern extended with an additional layer: The service layer.

> Defines an application’s boundary with a layer of services,  
> That establishes a set of available operations,  
> And coordinates the application’s response in each operation.  
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

The service layer acts as a facade for the business logic layer.  
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

The presentation layer’s responsibility becomes limited to,  
Providing the required input to the service layer,  
And communicating its responses back to the caller.

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

## Terminology

Elsewhere, you may encounter other terms used for the layered architecture:

- Presentation layer = user interface layer
- Service layer = application layer
- Business logic layer = domain layer = model layer
- Data access layer = infrastructure layer

To eliminate confusion, I present the pattern using the original terminology.

That said, I prefer **user interface layer** and **infrastructure layer**,  
As these terms better reflect the responsibilities of modern systems.  
And an **application layer** to avoid confusion with the physical boundaries of services.

## When to Use Layered Architecture?

The dependency between the business logic and the data access layers,  
Makes this architectural pattern a good fit for a system with its business logic implemented using the transaction script or active record pattern.

However, the pattern makes it challenging to implement a domain model.

In a domain model, the business entities (aggregates and value objects),  
Should have no dependency and no knowledge of the underlying infrastructure.

The layered architecture’s top-down dependency requires jumping through some hoops to fulfill this requirement.  
It is still possible to implement a domain model in a layered architecture,  
But the Ports & Adapters pattern fits much better.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
