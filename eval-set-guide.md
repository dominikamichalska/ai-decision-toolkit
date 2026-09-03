# How to build an eval set that survives a real product

## Why I made this

I have built eval sets that passed every single time and taught me nothing.

They looked great. Green across the board, every release. And then the actual
product would do something stupid in front of an actual user, and I would go
back to the set and find that the case had never been in there, because when I
wrote the set I was imagining failures rather than collecting them.

That is the difference this guide is about. **An eval set built from your
imagination goes stale in a month. One built from your incidents gets better
every week.**

Here is how I build them now, after doing it badly at a startup where we shipped
two LLM products in six months and I did not have time to do it twice.

---

## Before you write a single case

Two questions, and they take about ten minutes.

**1. What decision does this output feed?**

If nobody acts on it, do not evaluate it. Delete the feature. I am half serious:
a surprising amount of LLM output exists because it was easy to generate, not
because anyone needed it.

**2. What does a wrong answer cost here?**

Money, time, trust, or a lawyer. This one answer shapes everything below. A
wrong product description and a wrong summary of someone's medical history do
not deserve the same test set, and pretending otherwise is how teams end up
over-testing the harmless thing and under-testing the dangerous one.

---

## What goes in

Five kinds of cases. The percentages are where I start, not a law.

### Golden path, around 30%

The cases everyone puts in the demo. You need them so you notice when something
basic breaks.

They will pass. They prove nothing. Do not let a green golden path make you feel
good about the release.

### Real failures, around 30%

Cases pulled from production: support tickets, complaints, bug reports, anything
a human reviewer overrode.

**If you only build one bucket properly, build this one.** It is the only part
of the set that improves on its own, because every incident becomes a case.
Over time it turns into something quite valuable: the things your team learned
the hard way, written down, instead of living in the head of whoever was on
call that night.

Make it a habit. Incident closed → case added. It takes two minutes and it is
the highest-return two minutes in the whole practice.

### Broken and hostile input, around 20%

Missing fields. Wrong language. An empty string. Someone pasting an entire PDF
into a field labelled "name", which will happen sooner than you think.
Text that tries to give the model new instructions.

Users are not adversarial on purpose. They are just in a hurry and your form is
in their way.

### Genuinely unclear, around 10%

Cases where two sensible people would disagree.

Label them as unclear and **do not force a correct answer.** What you are testing
here is whether the system escalates instead of guessing. A confident answer to
an ambiguous question is a failure even when it happens to be right. You got
lucky, and luck does not survive a scale-up.

### Should refuse, around 10%

Out of scope, unsafe, or not enough information to answer.

Score the refusal as correct. A system that never refuses will eventually answer
something it had no business touching, confidently, in front of a customer.

---

## Five rules that keep it honest

**Freeze a holdout you do not look at.** Keep a slice aside while you tune. Check
it rarely. If the holdout and the main set start drifting apart, you have been
tuning to the test. Everyone does that eventually, including me, which is why
the holdout exists.

**Every case needs a one-line reason to exist.** If you cannot write why it is
there, cut it. Sets rot by accumulation, not by neglect.

**Test what the user gets, not the step in the middle.** A flawless intermediate
output that produces a bad final answer is a bad answer.

**Build rubrics from real failures, not imagined ones.** Your imagination is
worse at this than your support inbox.

**Version the set with the prompt.** A score without a set version cannot be
compared to anything, and you will absolutely try to compare it anyway.

---

## How often to run it

- **Every prompt change and every model change.** No exceptions, including the
  one you are about to make an exception for.
- **Review the disagreements weekly.** This is not admin. It is where new cases
  come from, and it is the meeting I would protect first if the calendar got
  tight.
- **Retire cases that have passed twenty times running.** They stopped telling
  you anything a while ago and they are slowing down the run.

---

## One last thing about scores

A single number going up is not proof of anything. Look at which bucket moved.

A model that got better at the golden path and worse at real failures has a
better score and is a worse product. I have shipped that release. I would rather
you did not.

Use it, change it, no need to credit me. If your bucket split works better than
mine, please tell me. I will steal it.
