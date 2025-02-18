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
