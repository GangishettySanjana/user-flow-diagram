# User Flow Diagram

A Claude Code skill that builds detailed, standard-convention user flow diagrams as standalone HTML files — not loose sketches, not abstract system diagrams, real flowcharts with the shapes, branching logic, and labeling that make them actually readable by someone who didn't build the product.

## What this is (and isn't)

This is a tool to get a first pass done faster, not a replacement for your actual UX process. What it does is narrow: it tells Claude exactly what "user flow" means in precise UX terms — the specific shapes, the branching logic, the distinction between a user flow and a user journey — so when you ask for one, you get a real flowchart instead of a vague sketch or an abstract system diagram. It doesn't do your user research, doesn't validate the flow against real usage, and the output still deserves a human pass before it ships anywhere. It's built for quick iteration and exploring a flow early, not for skipping the thinking a real flow needs.

I built this for my own use, exploring product flows through Claude before committing to them properly in Figma. Use it the same way, or adapt it to however you work.

## What it does

Ask Claude for a user flow for any product or feature, and this skill:

- Uses standard flowchart shapes — oval (start/end), rectangle (screen/action), diamond (decision), parallelogram (input/output) — the same convention used by Figma, Lucidchart, and most UX tooling.
- Labels every decision branch in plain language (`✓ Yes — cuts applied, re-check`, not a bare "Yes"), so a cold reader can follow the logic without guessing.
- Distinguishes **who** is deciding at each diamond — a person actively choosing, versus the system silently evaluating a condition — which most flowcharts leave ambiguous.
- Runs a real geometric verification pass (lines through shapes, overlapping labels, crossing arrows) instead of eyeballing a screenshot, which is how most hand-drawn flowcharts end up with a line quietly cutting through a box or a label hidden behind a shape.
- Delivers a real file you can open directly — no build step, no framework, no external tool required.

## Founding principles

The conventions in this skill aren't invented from scratch. They're grounded in three standard references on user flows:

- [Figma — What is a user flow?](https://www.figma.com/resource-library/user-flow/)
- [Nielsen Norman Group — User Journeys vs. User Flows](https://www.nngroup.com/articles/user-journeys-vs-user-flows/)
- [Interaction Design Foundation — User Flows](https://ixdf.org/literature/topics/user-flows)

The full skill explains exactly how each principle gets applied — see `skills/user-flow-diagram/SKILL.md`.

## Example

`examples/fitness-studio-booking-flow.html` is a full worked example built from a plain request ("make me a user flow for how someone books a class, including the waitlist and cancellation") — open it directly in a browser to see the skill's output.

## Install

**Quick, no install step:** download `skills/user-flow-diagram/SKILL.md` and drop the folder into your own `~/.claude/skills/`.

**As a plugin, with updates:**

```
/plugin marketplace add sanjanagangishetty/user-flow-diagram
/plugin install user-flow-diagram@sanjana-skills
```
