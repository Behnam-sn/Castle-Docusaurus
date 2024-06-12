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
