# The autonomy boundary checklist

Five questions to answer before you let a system decide something on its own.

## Why I made this

A few years ago I designed a verifier for grant applications, the kind that run
to 200 pages and take a person five hours to check. My first design had the
system scoring the applications itself. I was quite pleased with it.

Then we built a prototype, and the prototype showed me that the thing I had
designed should not exist. Not because the model was bad at reading. Because
nobody could tell me who was responsible when it was wrong, and once you ask
that question out loud about a grant decision, the answer has to be a person.

We shipped a different version. It cut verification from five hours to two, and
a human still made the call. That is the whole idea behind this checklist.

Here is the pattern I keep running into: **automation rarely fails at the demo.
It fails a few weeks later, quietly, when the team stops trusting it.** And when
I dig into why, it is almost never the model. It is that nobody wrote down what
the system was allowed to decide by itself, so everyone hedged, everyone
double-checked, and the tool became one more thing to review.

So now I write it down first. Five questions, one automated step at a time.

I call it TRACE. It is a rule of thumb, not a standard. Nobody outside my own
work uses it, which is exactly why you should feel free to rip it apart.

---

## T. Track: can you actually see it work?

**Ask:** Where does this step write its log? Who can read that log without
asking someone for access? If it goes wrong at 3am, how long until a person
knows?

If your honest answer to the last one is "when a customer complains", stop and
fix that before anything else here. Everything below assumes you can see what
happened.

A log nobody can reach is not a log. I have been on teams where the answer was
"it's in the logs" and getting to them meant asking the one backend engineer who
had the dashboard bookmarked. That is not observability, that is a favour.

## R. Rank: what does it claim, and how sure is it?

**Ask:** Does the output carry a confidence, or just an answer? And can you write
one line saying **what would have to be true for this answer to be wrong?**

That second one is the useful half. If you cannot write the line, you do not
have a ranking. You have a guess with a number stapled to it.

I make myself write it before shipping, and it has killed more of my own ideas
than any review meeting.

## A. Assign: who owns the result?

**Ask:** Who is responsible when this is wrong? Name a person. Not a team, not a
rota, not "product".

Then set a severity level that always goes to a human, **even when the model is
very confident.** This is the part people skip, and it is the part that matters
most. Being sure is not the same as being responsible. A model at 0.95
confidence on something that could cost someone their funding still needs a
name attached to the decision.

The default I use: high severity always escalates, regardless of confidence.
Confidence sets the routing for the boring cases. Severity overrides it.

One more: decide what that person actually sees. Just the answer? Or the answer
plus the case against it? Those produce very different decisions, and the second
one is almost always worth the extra screen.

## C. Challenge: can a person disagree cheaply?

**Ask:** How many clicks to override this? Is the override saved with a reason,
or does it vanish? Does the reviewer see the argument against the answer
*before* they decide, or only after they have already committed?

Here is the trap, and I have walked into it: **if disagreeing is slow, people
stop disagreeing.** Then your metrics show high agreement and you congratulate
yourself on a well-calibrated model. What you have actually built is a system
that wore everybody down.

Make overriding easy and make the reason mandatory. The reasons are the most
valuable data the whole system will ever produce.

## E. Evaluate: what closes the loop?

**Ask:** Who reads the overrides, and how often? What is the rule for changing
the threshold?

Write that rule down **now**, while nothing is on fire. Threshold changes made
during an incident are just panic with a number.

And one question I like because it is uncomfortable: if nothing has changed in
three months, is that because the system is working, or because nobody is
looking? Both look identical on a dashboard.

---

## The one question to answer before you tune anything

**What does a miss cost, and what does a false alarm cost?**

- **Miss is expensive, false alarm costs a minute** → favour recall. Accept the
  noise. Tell the team you are doing this on purpose, or they will file it as a
  bug.
- **Both cost about the same** → you probably do not need this automation.
  Genuinely. Go do something else.
- **False alarm is expensive** → raise the bar and accept that you will catch
  less. Say so out loud, so nobody is surprised later.

Answer this first. Otherwise you are tuning by feel and calling it data.

---

## How to actually use this

Copy it into your team docs. Fill it in per automated step. It takes about
fifteen minutes and the arguments it starts are the point.

Then keep the filled-in version next to the code, not in someone's head. The
test is whether it still makes sense when the person who built the step is on
holiday. That is not a hypothetical. That is week three.

Use it, change it, no need to credit me. If a question here is wrong or you
would add a sixth, I would genuinely like to hear it.
