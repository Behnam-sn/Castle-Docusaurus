---
sidebar_position: 3
---

# EventStorming

EventStorming is a collaboration-based workshop for modeling business processes.  
Apart from the resultant models, its primary benefit is knowledge sharing.

By the end of the session,  
All the participants will synchronize their mental models of the business process,  
And take the first steps toward using a ubiquitous language.

EventStorming is like riding a bicycle.  
It’s much easier to learn by doing it than to read about it in a book.  
Nevertheless, the workshop is fun and easy to facilitate.

You don’t need to be an EventStorming black belt to get started.  
Just facilitate the session, follow the steps, and learn during the process.

## What is EventStorming?

EventStorming is a low-tech activity for a group of people to brainstorm and rapidly model a business process.

In a sense, EventStorming is a tactical tool for sharing business domain knowledge.

An EventStorming session has a scope:  
The business process that the group is interested in exploring.

The participants are exploring the process as a series of domain events, represented by sticky notes, over a timeline.

Step by step, the model is enhanced with additional concepts such as:

- Actors
- Commands
- Eternal Systems
- And Others

Until all of its elements tell the story of how the business process works.

## Why Use EventStorming?

The workshop can be facilitated for many reasons:

- ### Build a ubiquitous language

  As the group cooperates in building the model of the business process,  
  They instinctively synchronize the terminology and start using the same language.

- ### Model the business process

  An EventStorming session is an effective way to build a model of the business process.  
  Since it is based on DDD-oriented building blocks,  
  It is also an effective way to discover the boundaries of aggregates and bounded contexts.

- ### Explore new business requirements

  You can use EventStorming to ensure that all the participants are on the same page regarding the new functionality,  
  And reveal edge cases not covered by the business requirements.

- ### Recover domain knowledge

  Over time, domain knowledge can get lost.  
  This is especially acute in legacy systems that require modernization.

  EventStorming is an effective way to merge the knowledge held by each participant into a single coherent picture.

- ### Explore ways to improve an existing business process

  Having an end-to-end view of a business process,  
  Provides the perspective needed to notice inefficiencies,  
  And opportunities to improve the process.

- ### Onboard new team members

  Facilitating an EventStorming session together with new team members is a great way to expand their domain knowledge.

:::warning
In addition to when to use EventStorming,  
It’s important to mention **when not to use it**.

EventStorming will be less successful when the business process you’re exploring is simple or obvious,  
Such as following a series of sequential steps without any interesting business logic or complexity.
:::

## Who Should Participate in EventStorming?

> Just keep in mind that the goal of the workshop is to learn as much as possible in the shortest time possible.  
> We invite key people to the workshop,  
> And we don’t want to waste their valuable time.  
> — Alberto Brandolini, creator of the EventStorming workshop

Ideally, a diverse group of people should participate in the workshop.

Anyone related to the business domain in question can participate:

- Engineers
- Domain Experts
- Product Owners
- Testers
- UI/UX Designers
- Support Personnel
- And so on

As more people with different backgrounds are involved, more knowledge will be discovered.

Take care not to make the group too big, however.  
Every participant should be able to contribute to the process,  
But this can be challenging for groups of more than 10 participants.

## What Do You Need for EventStorming?

EventStorming is considered a low-tech workshop because it is done using a pen and paper.  
(A lot of paper, actually)

Let’s see what you need in order to facilitate an EventStorming session:

- ### Modeling Space

  First, you need a large modeling space.

  A whole wall covered with butcher paper makes the best modeling space,  
  A large whiteboard can fit the purpose as well,  
  But it has to be as big as possible.

  You will need all the modeling space you can get.

- ### Sticky Notes

  Next, you need lots of sticky notes of different colors.

  The notes will be used to represent different concepts of the business domain;  
  And every participant should be able to add them freely.

  So make sure you have enough colors and enough for everyone.

  The colors that are traditionally used for EventStorming are described in the next section.

- ### Markers

  You’ll also need markers that you can use to write on the sticky notes.

  Supplies shouldn’t be a bottleneck for knowledge sharing.  
  There should be enough markers for all participants.

- ### Snacks

  A typical EventStorming session lasts about two to four hours,  
  So bring some healthy snacks for energy replenishment.

- ### Room

  Finally, you need a spacious room.

  Ensure there isn’t a huge table in the middle,  
  That will prevent participants from moving freely and observing the modeling space.

  Also, chairs are a big no-no for EventStorming sessions.  
  You want people to participate and share knowledge, not sit in a corner and zone out.  
  Therefore, if possible, take the chairs out of the room.

## The EventStorming Process

An EventStorming workshop is usually conducted in 10 steps.  
During each step, the model is enriched with additional information and concepts.

### Step 1: Unstructured Exploration

EventStorming starts with a brainstorm of the domain events related to the business domain being explored.

A domain event is something interesting that has happened in the business.

It’s important to formulate domain events in the past tense,  
Because they are describing things that have already happened.

During this step,  
All participants are grabbing a bunch of orange sticky notes,  
Writing down whatever domain events come to mind,  
And sticking them to the modeling surface.

At this early stage,  
There is no need to worry about ordering events,  
Or even about redundancy.

This step is all about brainstorming the possible things that can happen in the business domain.

The group should continue generating domain events until the rate of adding new ones slows significantly.

### Step 2: Timelines

Next, the participants go over the generated domain events,  
And organize them in the order in which they occur in the business domain.

The events should start with the **happy path scenario**:  
The flow that describes a successful business scenario.

Once the **happy path** is done,  
Alternative scenarios can be added.

For example,  
Paths where errors are encountered,  
Or different business decisions are taken.

The flow branching can be expressed as two flows coming from the preceding event,  
Or with arrows drawn on the modeling surface.

This step is also the time to fix incorrect events, remove duplicates, and of course, add missing events if necessary.

### Step 3: Pain Points

Once you have the events organized in a timeline,  
Use this broad view to identify points in the process that require attention.

These can be bottlenecks, manual steps that require automation, missing documentation, or missing domain knowledge.

It’s important to make these inefficiencies explicit,  
So that it will be easy to return to them as the EventStorming session progresses, or to address them afterward.

The pain points are marked with rotated (diamond) pink sticky notes.

:::note
Of course, this step is not the only opportunity to track pain points.  
As a facilitator, be aware of the participants’ comments throughout the process.  
When an issue or a concern is raised, document it as a pain point.
:::

### Step 4: Pivotal Events

Once you have a timeline of events augmented with pain points,  
look for significant business events indicating a change in context or phase.

These are called pivotal events,  
And are marked with a vertical bar dividing the events before and after the pivotal event.

For example:

- Shopping Cart Initialized
- Order Initialized
- Order Shipped
- Order Delivered
- Order Returned

Represent significant changes in the process of making an order.

Pivotal events are an indicator of potential bounded context boundaries.

### Step 5: Commands

Whereas a domain event describes something that has already happened,  
A command describes what triggered the event or flow of events.

Commands describe the system’s operations,  
And contrary to domain events, are formulated in the imperative.

For example:

- Publish Campaign
- Roll Back Transaction
- Submit Order

Commands are written on light blue sticky notes,  
And placed on the modeling space before the events they can produce.

If a particular command is executed by an actor in a specific role,  
The actor information is added to the command on a small yellow sticky note.

The actor represents a user persona within the business domain, such as customer, administrator, or editor.

Naturally, not all commands will have an associated actor.  
Therefore, add the actor information only where it’s obvious.

### Step 6: Policies

Almost always some commands are added to the model that have no specific actor associated with them.

During this step, you look for automation policies that might execute those commands.

An automation policy is a scenario in which an event triggers the execution of a command.  
In other words, a command is automatically executed when a specific domain event occurs.

On the modeling surface,  
Policies are represented as purple sticky notes connecting events to commands.

If the command in question should be triggered only if some decision criteria is met,  
You can specify the decision criteria explicitly on the policy sticky note.

For example,  
If you need to trigger the escalate command after the `ComplaintReceived` event,  
But only if the complaint was received from a VIP customer,  
You can explicitly state the _“only for VIP customers”_ condition on the policy sticky.

:::note
If the events and commands are far apart,  
You can draw an arrow on the modeling surface to connect them.
:::

### Step 7: Read Models

A read model is the view of data within the domain,  
That the actor uses to make a decision to execute a command.

This can be one of the system’s screens, a report, a notification, and so on.

The read models are represented by green sticky notes,  
With a short description of the source of information needed to support the actor’s decision.

:::note
Since a command is executed after the actor has viewed the read model,  
On the modeling surface the read models are positioned before the commands.
:::

### Step 8: External Systems

This step is about augmenting the model with external systems.

An external system is defined as any system that is not a part of the domain being explored.  
It can execute commands (input) or can be notified about events (output).

The external systems are represented by pink sticky notes.

By the end of this step,  
All commands should either be,  
Executed by actors,  
Triggered by policies,  
Or called by external systems.

### Step 9: Aggregates

Once all the events and commands are represented,  
The participants can start thinking about organizing related concepts in aggregates.

An aggregate receives commands and produces events.

Aggregates are represented as large yellow sticky notes,  
With commands on the left and events on the right.

### Step 10: Bounded Contexts

The last step of an EventStorming session is to look for aggregates that are related to each other.  
Either because they represent closely related functionality or because they’re coupled through policies.

The groups of aggregates form natural candidates for bounded contexts boundaries.

## Variants

Alberto Brandolini, the creator of the EventStorming workshop,  
Defines the EventStorming process as guidance, not hard rules.

You are free to experiment with the process to find the _“recipe”_ that works best for you.

In my experience,  
When introducing EventStorming in an organization,  
I prefer to start by exploring the big picture of the business domain,  
By following steps 1 (chaotic exploration) through 4 (pivotal events).

The resultant model,  
Covers a wide range of the company’s business domain,  
Builds a strong foundation for ubiquitous languages,  
And outlines possible boundaries for bounded contexts.

After gaining the big picture and identifying the different business processes,  
We continue to facilitate a dedicated EventStorming session for each relevant business process,  
This time, following all the steps to model the complete process.

At the end of a full EventStorming session,  
You will have a model describing the business domain’s events, commands, aggregates, and even possible bounded contexts.

However, all of these are just nice bonuses.  
The real value of an EventStorming session is the process itself.  
Which includes:  
The sharing of knowledge among different stakeholders,  
Alignment of their mental models of the business,  
Discovery of conflicting models,  
And last but not least, formulation of the ubiquitous language.

:::note
The resultant model can be adopted as a basis for implementing an event-sourced domain model.  
The decision of whether to go that route or not depends on your business domain.  
If you decide to implement the event-sourced domain model,  
You have the bounded context boundaries, the aggregates, and of course, the blueprint of the required domain events.
:::

## Facilitation Tips

### Quick Overview

When facilitating an EventStorming session with a group of people who have never done EventStorming before,  
I prefer to start with a quick overview of the process.

I Explain what we are about to do,  
The business process we are about to explore,  
And the modeling elements we will use in the workshop.

As we go through the elements (domain events, commands, actors, and so on),  
I build a legend using the sticky notes we will use,  
And labels to help the participants remember the color code.

The legend should be visible to all participants during the workshop.

### Conventions

It’s best to stick to the color and shape conventions,  
If possible, to be consistent with all of the currently available EventStorming books and trainings.

### Watch the Dynamics

As the workshop progresses,  
It’s important to track the energy of the group.

If the dynamics are slowing down,  
See whether you can reignite the process by asking questions,  
Or whether it’s time to advance to the next stage of the workshop.

Remember that EventStorming is a group activity,  
So ensure that it is handled as such.

Make sure everyone has a chance to participate in the modeling and the discussion.  
If you notice that some participants are shying away from the group,  
Try to involve them in the process by asking questions about the current state of the model.

EventStorming is an intense activity,  
And at some point the group will need a break.

Don’t resume the session until all the participants are back in the room.  
Resume the process by going through the current state of the model to return the group to a collaborative modeling mood.

### Remote EventStorming

EventStorming was invented as a low-tech activity,  
In which people interact and learn together in the same room.

The creator of the workshop, Alberto Brandolini,  
Has often objected to conducting EventStorming remotely,  
Because it’s impossible to achieve the same levels of participation.

However, with the onset of the COVID-19 pandemic in 2020,  
It became impossible to have in-person meetings,  
And do EventStorming as it was meant to be done.

A number of tools attempted to enable collaboration and facilitation of remote EventStorming sessions.  
At the time of this writing, the most notable of them is [miro.com](https://miro.com).

Be more patient when doing online EventStorming,  
And take into account the less effective communication that results.

In addition, my experience shows that remote EventStorming sessions are more effective with a smaller number of participants.  
While as many as 10 people can attend an in-person EventStorming session,  
I prefer to limit online sessions to five participants.

When you need more participants to contribute their knowledge,  
You can facilitate multiple sessions,  
And afterward compare and merge the resultant models.

When the situation allows,  
Return to in-person EventStorming.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
