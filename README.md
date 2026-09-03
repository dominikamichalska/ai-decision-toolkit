# AI decision toolkit

Two things I wish someone had handed me before I started putting models into
products where the answer actually mattered.

Both are short. Both came out of getting it wrong first.

## What's in here

### [The autonomy boundary checklist](autonomy-boundary-checklist.md)

Five questions to answer before you let a system decide something on its own.

It exists because of a pattern I kept hitting: automation almost never fails at
the demo. It fails a few weeks later, quietly, when the team stops trusting it,
and the reason is usually that nobody ever wrote down what the system was
allowed to decide by itself.

Run it once per automated step, before you ship. Fifteen minutes, and the
arguments it starts are the point.

### [How to build an eval set that survives a real product](eval-set-guide.md)

What to put in an eval set, what to leave out, how often to run it.

I have built sets that passed every time and told me nothing, because I wrote
them from imagined failures instead of collected ones. This is what I do
differently now.

## How to use them

Copy them into your own docs and change whatever does not fit your team. They
are rules of thumb, not standards. Nobody outside my own work uses them, which
is a good reason to disagree with any part of them.

No credit needed. If something here is wrong, or you would add a question I
missed, open an issue and tell me. That is genuinely more useful to me than a
star.

## Who wrote this

I'm Dominika, an AI Product Manager in Poznań. I spend most of my time on the
boring, load-bearing part of AI products: what the system decides alone, what
comes back to a person, and how you tell whether any of it is working.

I write about that at [Trust-Critical AI](https://www.trustcriticalai.com/), and
the rest of my work is at [domichalska.com](https://domichalska.com/).
