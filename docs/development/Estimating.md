# Estimating

The Library of Congress in Washington, DC, currently has about 75 terabytes
of digital information online. Quick! How long will it take to send all that
information over a 1Gbps network? How much storage will you need for a
million names and addresses? How long does it take to compress 100Mb of
text? How many months will it take to deliver your project?

At one level, these are all meaningless questions—they are all missing infor-
mation. And yet they can all be answered, as long as you are comfortable
estimating. And, in the process of producing an estimate, you’ll come to
understand more about the world your programs inhabit.

By learning to estimate, and by developing this skill to the point where you
have an intuitive feel for the magnitudes of things, you will be able to show
an apparent magical ability to determine their feasibility. When someone says
“we’ll send the backup over a network connection to S3,” you’ll be able to
know intuitively whether this is practical. When you’re coding, you’ll be able
to know which subsystems need optimizing and which ones can be left alone.

## How Accurate Is Accurate Enough?

To some extent, all answers are estimates. It’s just that some are more
accurate than others. So the first question you have to ask yourself when
someone asks you for an estimate is the context in which your answer will
be taken. Do they need high accuracy, or are they looking for a ballpark figure?

One of the interesting things about estimating is that the units you use make
a difference in the interpretation of the result. If you say that something will
take about 130 working days, then people will be expecting it to come in
pretty close. However, if you say “Oh, about six months,” then they know to
look for it any time between five and seven months from now. Both numbers
represent the same duration, but “130 days” probably implies a higher degree
of accuracy than you feel. We recommend that you scale time estimates as
follows:

Duration
Quote estimate in
1–15 daysDays
3–6 weeksWeeks
8–20 weeks Months
20+ weeks
Think hard before giving an estimate

So, if after doing all the necessary work, you decide that a project will take
125 working days (25 weeks), you might want to deliver an estimate of “about
six months.”

The same concepts apply to estimates of any quantity: choose the units of
your answer to reflect the accuracy you intend to convey.

## Where Do Estimates Come From?

All estimates are based on models of the problem. But before we get too deeply
into the techniques of building models, we have to mention a basic estimating
trick that always gives good answers: ask someone who’s already done it.
Before you get too committed to model building, cast around for someone
who’s been in a similar situation in the past. See how their problem got solved.
It’s unlikely you’ll ever find an exact match, but you’d be surprised how many
times you can successfully draw on others’ experiences.

### Understand What’s Being Asked

The first part of any estimation exercise is building an understanding of what’s
being asked. As well as the accuracy issues discussed above, you need to
have a grasp of the scope of the domain. Often this is implicit in the question,
but you need to make it a habit to think about the scope before starting to
guess. Often, the scope you choose will form part of the answer you give:
“Assuming there are no traffic accidents and there’s gas in the car, I should
be there in 20 minutes.”

### Build a Model of the System

This is the fun part of estimating. From your understanding of the question
being asked, build a rough-and-ready bare-bones mental model. If you’re
estimating response times, your model may involve a server and some kind
of arriving traffic. For a project, the model may be the steps that your organi-
zation uses during development, along with a very rough picture of how the
system might be implemented.

Model building can be both creative and useful in the long term. Often, the
process of building the model leads to discoveries of underlying patterns and
processes that weren’t apparent on the surface. You may even want to reex-
amine the original question: “You asked for an estimate to do X. However, it
looks like Y, a variant of X, could be done in about half the time, and you lose
only one feature.”

Building the model introduces inaccuracies into the estimating process. This
is inevitable, and also beneficial. You are trading off model simplicity for
accuracy. Doubling the effort on the model may give you only a slight increase
in accuracy. Your experience will tell you when to stop refining.

### Break the Model into Components

Once you have a model, you can decompose it into components. You’ll need
to discover the mathematical rules that describe how these components
interact. Sometimes a component contributes a single value that is added
into the result. Some components may supply multiplying factors, while
others may be more complicated (such as those that simulate the arrival of
traffic at a node).

You’ll find that each component will typically have parameters that affect how
it contributes to the overall model. At this stage, simply identify each
parameter.

### Give Each Parameter a Value

Once you have the parameters broken out, you can go through and assign
each one a value. You expect to introduce some errors in this step. The trick
is to work out which parameters have the most impact on the result, and
concentrate on getting them about right. Typically, parameters whose values
are added into a result are less significant than those that are multiplied or
divided. Doubling a line speed may double the amount of data received in an
hour, while adding a 5ms transit delay will have no noticeable effect.

You should have a justifiable way of calculating these critical parameters.
For the queuing example, you might want to measure the actual transaction
arrival rate of the existing system, or find a similar system to measure. Simi-
larly, you could measure the current time taken to serve a request, or come
up with an estimate using the techniques described in this section. In fact,
you’ll often find yourself basing an estimate on other subestimates. This is
where your largest errors will creep in.

### Calculate the Answers

Only in the simplest of cases will an estimate have a single answer. You might
be happy to say “I can walk five cross-town blocks in 15 minutes.” However,
as the systems get more complex, you’ll want to hedge your answers. Run
multiple calculations, varying the values of the critical parameters, until you
work out which ones really drive the model. A spreadsheet can be a big help.
Then couch your answer in terms of these parameters. “The response time
is roughly three quarters of a second if the system has SSDs and 32GB of
memory, and one second with 16GB memory.” (Notice how “three quarters
of a second” conveys a different feeling of accuracy than 750ms.)

During the calculation phase, you get answers that seem strange. Don’t be
too quick to dismiss them. If your arithmetic is correct, your understanding
of the problem or your model is probably wrong. This is valuable information.

### Keep Track of Your Estimating Prowess

We think it’s a great idea to record your estimates so you can see how close
you were. If an overall estimate involved calculating subestimates, keep track
of these as well. Often you’ll find your estimates are pretty good—in fact, after
a while, you’ll come to expect this.

When an estimate turns out wrong, don’t just shrug and walk away—find out
why. Maybe you chose some parameters that didn’t match the reality of the
problem. Maybe your model was wrong. Whatever the reason, take some time
to uncover what happened. If you do, your next estimate will be better.

## Estimating Project Schedules

Normally you’ll be asked to estimate how long something will take. If that
“something” is complex, the estimate can be very difficult to produce. In this
section, we’ll look at two techniques for reducing that uncertainty.

### Painting the Missile

“How long will it take to paint the house?”

“Well, if everything goes right, and this paint has the coverage they claim, it
might be as few as 10 hours. But that’s unlikely: I’d guess a more realistic
figure is closer to 18 hours. And, of course, if the weather turns bad, that could
push it out to 30 or more.”

That’s how people estimate in the real world. Not with a single number (unless
you force them to give you one) but with a range of scenarios.

When the U.S. Navy needed to plan the Polaris submarine project, they
adopted this style of estimating with a methodology they called the Program
Evaluation Review Technique, or PERT.

Every PERT task has an optimistic, a most likely, and a pessimistic estimate.
The tasks are arranged into a dependency network, and then you use some
simple statistics to identify likely best and worst times for the overall project.

Using a range of values like this is a great way to avoid one of the most com-
mon causes of estimation error: padding a number because you’re unsure.
Instead, the statistics behind PERT spreads the uncertainty out for you, giving
you better estimations of the whole project.

However, we’re not big fans of this. People tend to produce wall-sized charts
of all the tasks in a project, and implicitly believe that, just because they used
a formula, they have an accurate estimate. The chances are they don’t, because
they have never done this before.

### Eating the Elephant

We find that often the only way to determine the timetable for a project is by
gaining experience on that same project. This needn’t be a paradox if you
practice incremental development, repeating the following steps with very
thin slices of functionality:

• Check requirements
• Analyze risk (and prioritize riskiest items earlier)
• Design, implement, integrate
• Validate with the users

Initially, you may have only a vague idea of how many iterations will be
required, or how long they may be. Some methods require you to nail this
down as part of the initial plan; however, for all but the most trivial of projects
this is a mistake. Unless you are doing an application similar to a previous
one, with the same team and the same technology, you’d just be guessing.

So you complete the coding and testing of the initial functionality and mark
this as the end of the first iteration. Based on that experience, you can refine
your initial guess on the number of iterations and what can be included in
each. The refinement gets better and better each time, and confidence in the
schedule grows along with it. This kind of estimating is often done during the
team’s review at the end of each iterative cycle.

That’s also how the old joke says to eat an elephant: one bite at a time.

This may not be popular with management, who typically want a single, hard-
and-fast number before the project even starts. You’ll have to help them
understand that the team, their productivity, and the environment will
determine the schedule. By formalizing this, and refining the schedule as
part of each iteration, you’ll be giving them the most accurate scheduling
estimates you can.

## What to Say When Asked for an Estimate

You say “I’ll get back to you.”

You almost always get better results if you slow the process down and spend
some time going through the steps we describe in this section. Estimates
given at the coffee machine will (like the coffee) come back to haunt you.
