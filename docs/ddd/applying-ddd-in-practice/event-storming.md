# EventStorming

In this chapter, we will take a break from discussing software design patterns and
techniques. Instead, we will focus on a low-tech modeling process called EventStorm‐
ing. This process brings together the core aspects of domain-driven design that we
covered in the preceding chapters.

You will learn the EventStorming process, how to facilitate an EventStorming work‐
shop, and how to leverage EventStorming to effectively share domain knowledge and
build a ubiquitous language.

## What Is EventStorming?

EventStorming is a low-tech activity for a group of people to brainstorm and rapidly model a business process.
In a sense, EventStorming is a tactical tool for sharing busi‐
ness domain knowledge.

An EventStorming session has a scope: the business process that the group is interes‐
ted in exploring. The participants are exploring the process as a series of domain
events, represented by sticky notes, over a timeline. Step by step, the model is
enhanced with additional concepts—actors, commands, external systems, and
others—until all of its elements tell the story of how the business process works.

Who Should Participate in EventStorming?

> Just keep in mind that the goal of the workshop is to learn as much as possible in the shortest
> time possible. We invite key people to the workshop, and we don’t want to waste their valua‐
> ble time.
> —Alberto Brandolini, creator of the EventStorming workshop

Ideally, a diverse group of people should participate in the workshop. Indeed, anyone
related to the business domain in question can participate: engineers, domain experts,
product owners, testers, UI/UX designers, support personnel, and so on. As more
people with different backgrounds are involved, more knowledge will be discovered.

Take care not to make the group too big, however. Every participant should be able to
contribute to the process, but this can be challenging for groups of more than 10
participants.

## What Do You Need for EventStorming?

EventStorming is considered a low-tech workshop because it is done using a pen and
paper—a lot of paper, actually. Let’s see what you need in order to facilitate an Event‐
Storming session:

- Modeling space
  First, you need a large modeling space. A whole wall covered with butcher paper
  makes the best modeling space, A large whiteboard can
  fit the purpose as well, but it has to be as big as possible—you will need all the
  modeling space you can get.

- Sticky notes
  Next, you need lots of sticky notes of different colors. The notes will be used to
  represent different concepts of the business domain, and every participant should
  be able to add them freely, so make sure you have enough colors and enough for
  everyone. The colors that are traditionally used for EventStorming are described
  in the next section. It’s best to stick to these conventions, if possible, to be consis‐
  tent with all of the currently available EventStorming books and trainings.

- Markers
  You’ll also need markers that you can use to write on the sticky notes. Again, sup‐
  plies shouldn’t be a bottleneck for knowledge sharing—there should be enough
  markers for all participants.

- Snacks
  A typical EventStorming session lasts about two to four hours, so bring some
  healthy snacks for energy replenishment.

- Room
  Finally, you need a spacious room. Ensure there isn’t a huge table in the middle
  that will prevent participants from moving freely and observing the modeling
  space. Also, chairs are a big no-no for EventStorming sessions. You want people
  to participate and share knowledge, not sit in a corner and zone out. Therefore, if
  possible, take the chairs out of the room.

## The EventStorming Process

An EventStorming workshop is usually conducted in 10 steps. During each step, the
model is enriched with additional information and concepts.

### Step 1: Unstructured Exploration

EventStorming starts with a brainstorm of the domain events related to the business
domain being explored. A domain event is something interesting that has happened
in the business. It’s important to formulate domain events in the past tense
they are describing things that have already happened.

During this step, all participants are grabbing a bunch of orange sticky notes, writing
down whatever domain events come to mind, and sticking them to the modeling
surface.

At this early stage, there is no need to worry about ordering events, or even about
redundancy. This step is all about brainstorming the possible things that can happen
in the business domain.

The group should continue generating domain events until the rate of adding new
ones slows significantly.

### Step 2: Timelines

Next, the participants go over the generated domain events and organize them in the
order in which they occur in the business domain.

The events should start with the “happy path scenario”: the flow that describes a suc‐
cessful business scenario.

Once the “happy path” is done, alternative scenarios can be added—for example,
paths where errors are encountered or different business decisions are taken. The
flow branching can be expressed as two flows coming from the preceding event or
with arrows drawn on the modeling surface.

This step is also the time to fix incorrect events, remove duplicates, and of course,
add missing events if necessary.

### Step 3: Pain Points

Once you have the events organized in a timeline, use this broad view to identify
points in the process that require attention. These can be bottlenecks, manual steps
that require automation, missing documentation, or missing domain knowledge.

It’s important to make these inefficiencies explicit so that it will be easy to return to
them as the EventStorming session progresses, or to address them afterward. The
pain points are marked with rotated (diamond) pink sticky notes.

Of course, this step is not the only opportunity to track pain points. As a facilitator,
be aware of the participants’ comments throughout the process. When an issue or a
concern is raised, document it as a pain point.

### Step 4: Pivotal Events

Once you have a timeline of events augmented with pain points, look for significant
business events indicating a change in context or phase. These are called pivotal
events and are marked with a vertical bar dividing the events before and after the piv‐
otal event.

For example, “shopping cart initialized,” “order initialized,” “order shipped,” “order
delivered,” and “order returned” represent significant changes in the process of mak‐
ing an order.

Pivotal events are an indicator of potential bounded context boundaries.

### Step 5: Commands

Whereas a domain event describes something that has already happened, a command
describes what triggered the event or flow of events. Commands describe the system’s
operations and, contrary to domain events, are formulated in the imperative. For
example:

- Publish campaign
- Roll back transaction
- Submit order

Commands are written on light blue sticky notes and placed on the modeling space
before the events they can produce. If a particular command is executed by an actor
in a specific role, the actor information is added to the command on a small yellow
sticky note.

The actor represents a user persona within
the business domain, such as customer, administrator, or editor.

Naturally, not all commands will have an associated actor. Therefore, add the actor
information only where it’s obvious. In the next step we will augment the model with
additional entities that can trigger commands.

### Step 6: Policies

Almost always, some commands are added to the model but have no specific actor
associated with them. During this step, you look for automation policies that might
execute those commands.

An automation policy is a scenario in which an event triggers the execution of a com‐
mand. In other words, a command is automatically executed when a specific domain
event occurs.

On the modeling surface, policies are represented as purple sticky notes connecting
events to commands.

If the command in question should be triggered only if some decision criteria is met,
you can specify the decision criteria explicitly on the policy sticky note. For example,
if you need to trigger the escalate command after the “complaint received” event,
but only if the complaint was received from a VIP customer, you can explicitly state
the “only for VIP customers” condition on the policy sticky.

If the events and commands are far apart, you can draw an arrow on the modeling
surface to connect them.

### Step 7: Read Models

A read model is the view of data within the domain that the actor uses to make a
decision to execute a command. This can be one of the system’s screens, a report, a
notification, and so on.

The read models are represented by green sticky notes
with a short description of the source of information needed to sup‐
port the actor’s decision.

Since a command is executed after the actor has viewed the
read model, on the modeling surface the read models are positioned before the
commands.

### Step 8: External Systems

This step is about augmenting the model with external systems. An external system is
defined as any system that is not a part of the domain being explored. It can execute
commands (input) or can be notified about events (output).

The external systems are represented by pink sticky notes.

the CRM
(external system) triggers execution of the “Ship Order” command. When the ship‐
ment is approved (event), it is communicated to the CRM (external system) through
a policy.

By the end of this step, all commands should either be executed by actors, triggered
by policies, or called by external systems.

### Step 9: Aggregates

Once all the events and commands are represented, the participants can start think‐
ing about organizing related concepts in aggregates. An aggregate receives commands
and produces events.

Aggregates are represented as large yellow sticky notes, with commands on the left
and events on the right.

### Step 10: Bounded Contexts

The last step of an EventStorming session is to look for aggregates that are related to
each other, either because they represent closely related functionality or because
they’re coupled through policies. The groups of aggregates form natural candidates
for bounded contexts’ boundaries.

## Variants

Alberto Brandolini, the creator of the EventStorming workshop, defines the Event‐
Storming process as guidance, not hard rules. You are free to experiment with the pro‐
cess to find the “recipe” that works best for you.

In my experience, when introducing EventStorming in an organization I prefer to
start by exploring the big picture of the business domain by following steps 1 (chaotic
exploration) through 4 (pivotal events). The resultant model covers a wide range of
the company’s business domain, builds a strong foundation for ubiquitous languages,
and outlines possible boundaries for bounded contexts.

After gaining the big picture and identifying the different business processes, we con‐
tinue to facilitate a dedicated EventStorming session for each relevant business pro‐
cess—this time, following all the steps to model the complete process.

At the end of a full EventStorming session, you will have a model describing the busi‐
ness domain’s events, commands, aggregates, and even possible bounded contexts.
However, all of these are just nice bonuses. The real value of an EventStorming ses‐
sion is the process itself—the sharing of knowledge among different stakeholders,
alignment of their mental models of the business, discovery of conflicting models,
and, last but not least, formulation of the ubiquitous language.

The resultant model can be adopted as a basis for implementing an event-sourced
domain model. The decision of whether to go that route or not depends on your
business domain. If you decide to implement the event-sourced domain model, you
have the bounded context boundaries, the aggregates, and of course, the blueprint of
the required domain events.