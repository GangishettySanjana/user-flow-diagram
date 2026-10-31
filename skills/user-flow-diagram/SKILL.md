---
name: user-flow-diagram
description: Build a detailed, standalone user-flow flowchart (oval/rectangle/diamond/parallelogram, right-angle connectors, solid vs dashed lines) for a product or feature. Use whenever the user asks for a "user flow", "user flow diagram", "flowchart of how someone uses X", wants to map every trigger/step/decision a user hits in a product, or asks to turn a described flow into a visual diagram. Also use when they ask to see "what's possible" in a product as a map, or to distinguish what different roles/actors can do in a flow. Prefer this over a generic Artifact or a loose sketch whenever flowchart conventions, maximal detail, or a plain downloadable HTML file is wanted.
---

# User Flow Diagram

A user flow diagram maps the real, specific path a user takes through a product to complete **one task** — not an abstract system/data diagram, and not a user journey map (see Founding principles below). Build it as a real flowchart with standard symbols, delivered as a plain standalone HTML file the user can open directly.

## Founding principles

This skill's conventions aren't invented from scratch — they're grounded in three standard references on user flows. When a judgment call comes up that isn't covered elsewhere in this file, these are the tiebreakers:

- **[Figma: What is a user flow?](https://www.figma.com/resource-library/user-flow/)** — start with user goals, focus on one goal per flow, keep symbols/shapes/labels consistent throughout, map only meaningful moments (forms completed, buttons tapped — not every click), show decision points as forks in the path, share early and iterate.
- **[NN/g: User Journeys vs. User Flows](https://www.nngroup.com/articles/user-journeys-vs-user-flows/)** — a user flow is the granular, single-product, single-task view: "key user actions and system responses." This is distinct from a user journey, which is the broad, multi-channel, emotion-inclusive view. A user flow explicitly does **not** contextualize the process with emotions or thoughts, and doesn't span multiple products/channels or long timeframes — that's journey-map territory, out of scope for this skill.
- **[IxDF: User Flows](https://ixdf.org/literature/topics/user-flows)** — standard shapes are ovals (start/end), rectangles (steps), diamonds (decisions), parallelograms (user input), each paired with a brief text label; mark entry and exit points explicitly; keep options limited ("more options, more problems" — Scott Belsky); a flow that's too simple is as real a failure as one that's too complex.

In short: one task, one product, the real steps and the system's real responses to them, no emotions or thoughts, consistent symbols, explicit entry and exit points.

## Why this exists

A flowchart earns its keep when a cold reader can see the actual mechanism — every trigger, every branch, who can do what — without having to assemble it from a feature list or a paragraph of prose. Treat the product's own docs (README, roadmap, specs) as the source of truth for what belongs in it; don't invent a generic "happy path" that could describe any app.

## Shape conventions (non-negotiable — these are standard, not stylistic)

- **Oval / pill (terminator)** — start or end of the flow.
- **Rectangle** — a screen the user views, or an action/task they perform.
- **Diamond** — a decision point with branches (usually two: yes/no).
- **Parallelogram** — input/output: data entering or leaving the system, especially anything shared with other people (a vote, a submitted form, a shared link).
- **Circle** — on-page connector, only if a direct line would get genuinely messy. Most flows don't need one; don't add it just to look complete.

Always draw a small legend reproducing these exact shapes with the same fill/stroke used in the diagram, so the diagram is self-explanatory without this file.

## Every diamond must say who is deciding, not just what's being decided

A diamond is a decision point, but "decision point" collapses two different things that look identical on the page: a **user decision** (a person is actively choosing between options — "Create new, or join existing?") and a **system check** (the app is evaluating a condition automatically, nobody is choosing anything — "Does it pass validation?", "All approved?"). Same shape, same color, but the reader needs to know which one they're looking at, because a system check reads as passive ("this got evaluated") while a user decision reads as active ("someone picked"). Don't rely on context to carry this — most diamonds in a real flow turn out to be system checks (a condition the app computed), with only a handful being genuine user decisions, and a reader can't tell the two apart from the diamond's shape alone.

Make the distinction visible in the diamond's own title, not as a separate label: phrase a user decision as a question the *person* is answering ("Create new, or join existing?"), and phrase a system check as the condition itself, ideally naming what's being checked rather than leaving it generic ("Does it pass validation?" rather than just "Check?"). When a diamond is ambiguous either way (e.g. a tally that a person ultimately confirms), say so in a sub-caption rather than leaving it unstated — don't force every diamond into one category if the real behavior is mixed.

## Line conventions

- **Solid line** — the primary, forward-moving path (including a decision's "yes" branch when it continues forward).
- **Dashed line** — an alternate path, a conditional detour, or a backward loop (retrying a failed check, looping back to adjust something). Color these distinctly (an accent color) so backward motion reads at a glance.
- **Route every connector as orthogonal segments (horizontal/vertical), with softly rounded corners at each bend** — plan the path the same way as a real flowchart tool (Visio/Lucidchart/draw.io): horizontal and vertical runs, no diagonals, with each bend gently curved rather than a sharp 90° angle. Implement by keeping the same waypoint list you'd already use for right-angle routing, then rounding each interior vertex: trim back along each incident segment by an adaptive radius (`min(desired_radius, seg_len/2 - 2)`, skip rounding — leave the corner sharp — if that comes out under ~3px) and join with a quadratic Bézier (`Q`) through the original vertex as control point. This only softens the bend; it doesn't change the underlying route, so all the crossing/overlap verification below still applies to the same waypoints.

## Every decision's branches must be spelled out — this is the single most important rule

A diamond with two unlabeled or vaguely-labeled exits is the #1 thing that makes a flowchart unreadable, even when the lines themselves are clean. Clean, non-overlapping lines are not sufficient on their own — a reviewer can trace every line perfectly and still have no idea what the diagram is actually saying if the branches don't state their own outcome in plain language.

For every single diamond:
- Both exit arrows get a label starting with **"Yes —"** or **"No —"**, every time, with no exceptions and no inconsistent phrasing (don't let one branch say "Yes — it fits" and a sibling decision's branch say just "dates set, confirmed" with no Yes/No prefix at all — that inconsistency is exactly what reads as unclear).
- The label states the **plain-language result or destination**, not just the raw condition. "Yes — cuts applied, re-check" tells the reader what happens and implies where it's going; "Yes, apply" does not. "No — adjust manually" is clear; "adjust" floating near a line is not.
- If a decision's real-world meaning isn't obvious from the diamond's title alone, rename the diamond itself too (e.g. "Applies it?" → "Approves the change?") rather than relying on the branch labels alone to carry the meaning.
- It's fine — encouraged, even — for this to make the diagram bigger. Spacing a dense cluster of decisions further apart so every label has room to sit directly on its own line, unambiguous, beats cramming it smaller. There is no size limit on a flowchart that earns real clarity.

## "Always available" / persistent features need their own flows too, not just a card

Don't stop at pulling persistent features (chat, settings, sharing, notifications, tasks, an activity log) out of the main spine into a side panel with one caption line each. If asked for "every flowchart" or the product has real behavior behind each of those, give each one its own small flow in the same shape/line/Yes-No conventions — most have at least one genuine decision point (already claimed by someone else? inviting vs exporting? tap the notification or not?) worth diagramming, not just a one-line summary card. Don't invent a decision where none exists, though — a feature that's genuinely linear (no real branch) stays a straight line rather than forcing a diamond onto it.

## Lines must never pass through an unrelated shape, not just avoid text

The label-masking technique (below) only protects text from being crossed by a line. It does nothing to stop a loop-back or branch line from visually passing *through* a node box or diamond that isn't its source or destination — which looks exactly as broken as a line cutting through text, and is easy to introduce by accident when hand-routing a long loop around a dense cluster. Before delivering, run a second geometric check (not just the label-overlap one): for every arrow path segment, test it against the bounding box of every node shape (every `rect`/`polygon`/`ellipse` that represents an actual node, not a label mask or background panel) using a true line–rectangle intersection (not just a bounding-box overlap check, which gives false positives on diagonal lines) — and flag any segment that enters a shape's box without that shape being the segment's own start or end point. Fix every hit by rerouting the line through a clear lane (a y or x band with nothing else in it) rather than shortening or hand-waving it.

Run a third check too: path-vs-path crossings between every pair of arrows (not just within the dashed/loop group — a rerouted loop can just as easily cut across a different solid primary-path arrow or another loop entirely). An unlabeled crossing between two unrelated arrows is exactly the kind of "too many lines, where does this one even go" confusion that reads as broken even when nothing touches text or a shape. When a reroute fixes one crossing, always re-run all three checks (text, shape, line-line) together — moving a line to dodge one problem routinely creates a new crossing somewhere else in the same cluster, so treat one clean pass as provisional until a full re-check comes back empty.

When hand-computing a polygon's own vertices for routing an arrow (e.g. "exit from the diamond's left vertex"), double check the vertex coordinate against the actual `points` list rather than assuming — it's easy to accidentally use the shape's center instead, which draws the arrow starting from inside the shape, straight through its own label text.

## When a loop keeps needing re-fixing, simplify the logic instead of re-routing again

If the same cluster of nodes gets flagged as confusing across multiple review rounds even after the lines stop literally crossing anything, that's a signal the *underlying decision structure* is the problem, not the routing. A three-node loop (does it pass? → here's what to fix → did you approve the fix?) is harder to trace than a two-node one (does it pass? → here's what to fix, go fix it, then it re-checks automatically), especially once it's drawn with multiple turns to dodge other shapes. Before re-routing a confusing loop for the third time, ask whether a node in it can be cut — specifically, whether an "approve/apply" decision actually changes what happens next, or whether the real product behavior is just "the suggestion updates the same editable thing you already touch, and the check re-runs." If so, remove the decision and replace the loop with one plain arrow back to the editing step.

**Keep parallel decisions visually consistent.** When two parts of a flow do structurally the same thing (e.g. two independent approval or confirmation steps), give them the same shape: if one has a "chosen?" gate diamond before the next step, the other needs one too, even if the product's real behavior makes it less strictly necessary — the reader is pattern-matching across the diagram, and an inconsistency between two similar-looking moments reads as a missing decision, not a deliberate simplification.

**A loop-back's target matters, not just its label.** When a decision's "No" branch skips over an intermediate step to land further back in the flow, that reads as ambiguous even with a correct label, because the reader can't tell whether the skipped step was optional. Default to landing a loop-back on the nearest preceding step, not the earliest one, unless there's a specific reason to jump further.

**Don't let a completion arrow look like a decision branch.** An arrow that just returns to the main flow after a side action finishes (not a decision's Yes/No) can get misread as an unlabeled branch if it visually hugs a nearby diamond or uses the same accent color/dash style without being near any diamond's vertex. Word it as a plain statement of what just happened ("ready to continue"), not a fragment that could be mistaken for a branch condition, and keep it visually separated from any nearby decision diamond.

## Mark every Yes/No with a symbol, not just the word

Spelling out "Yes —" / "No —" in text is necessary, but a literal glyph reads even faster: prefix every branch label with a checkmark/cross (`✓ Yes` / `✗ No`). This reads at a glance even faster than the words alone, and — just as important — forces every label short (under ~50px wide), which sidesteps most of the width-driven overlap problems below. Push any extra context (who's responsible, what condition applies) onto the node's own title or sub-caption instead of the arrow label; the arrow only needs to carry Yes/No plus the glyph. Color the two consistently but distinctly (e.g. ink for Yes, a softer neutral for No) — don't reuse whatever color is doing double duty elsewhere in the diagram (see Visual system below), since one color meaning two things is exactly the kind of ambiguity this glyph convention exists to kill.

## Verify every label sits on TOP of every node shape too, not just that it avoids lines

The label-overlaps-a-line check (above) is not the only way a label goes unreadable. If labels are drawn earlier in the SVG than the node shapes (rects/polygons/ellipses), any label that happens to fall within a shape's bounding box gets silently painted over by that shape, since later elements in SVG draw on top. This produces a label that's still present in the markup but invisible on screen — reads as text "cutting off" or a Yes/No "disappearing" when it's actually just occluded. Two independent fixes, do both:
1. **Draw the labels `<g>` last**, after every node, so it always renders on top.
2. **Also verify geometrically** with a label-vs-shape check (same rect-overlap test as the line-vs-shape check, but comparing each label's text bbox against every node's bbox) and reposition any hit — don't rely on draw order alone, since a label sitting on top of a shape still looks messy even when it's technically legible.

When writing this check (or the line-vs-shape one), double check the property names match between the two bbox objects being compared (`width`/`height` vs a shorthand like `w`/`h`) — a mismatch silently produces `NaN` comparisons that register as "overlap" for every single pair, which looks like dozens of real bugs and wastes a lot of time chasing phantoms. Sanity-check a new verification script against one clearly-non-overlapping pair and one clearly-overlapping pair before trusting its output on the real diagram.

## Every label needs an arrow, and every arrow needs to actually exist

A label floating near a diamond ("Yes, late") is not the same as a drawn arrow to the node it supposedly points to — it's easy to add the label and forget the `<path>`, especially late in a long editing session. This renders as "there's no line, how does a person know this is a yes" and is a different bug from routing or crossing problems: no amount of rerouting fixes it, since there was never a line to begin with. Before shipping, cross-check that every label in the labels group has a corresponding path whose start or end point sits near it — or more simply, trace every single node in the diagram and confirm it has both an incoming and an outgoing connector (except the true start/end nodes).

## When multiple arrows land on the same node, separate their entry points

A node that receives more than one incoming arrow (e.g. a loop-back "No" arriving at a step that also has a normal forward arrow from elsewhere) needs each arrow to land somewhere visually distinct — a different edge, or at least a clearly separated point on the same edge. Two arrows converging on nearly the same spot reads as one tangled, ambiguous line even when both are individually correct and labeled, because the reader can't tell at a glance which arrow is which or trace either one back to its source. A loop-back landing right next to a separate forward arrow's entry point on the same edge of the same box will read as one confused junction, even with correct labels on both. The fix is to route one of them into a different edge entirely (the side instead of the top, say) so each incoming arrow has its own clear lane into the shape. When adding or rerouting any arrow, check what else already lands on that node and make sure the new entry point doesn't cluster with an existing one.

## New diamonds need a shape-vs-shape check too, not just line checks

Adding a new decision diamond near an existing one (e.g. to mirror an existing pattern elsewhere in the diagram, like giving a second branch a confirmation gate because an earlier one has one) can make the two diamonds' bounding boxes — or worse, their actual tapered shapes — overlap or nearly touch, especially when space is already tight. Run a fourth check: every node shape's bbox against every other node shape's bbox, flagging any pair that overlaps (not just lines against shapes). Diamonds taper to points, so a bbox-only check will over-report near the tips — but treat anything flagged within ~10-15px as worth a manual look rather than dismissing it, since two tapering points that close together usually do read as touching once rendered. Expect that fixing one crossing or overlap in a crowded cluster often creates a new one a few pixels away (two loops now sharing a lane, a rerouted line grazing a shape it didn't touch before) — budget for 3-4 iterations of fix-then-recheck-all-five-checks before a crowded area actually comes back clean, and re-run the full check suite (text-line, shape-line, line-line, label-shape, shape-shape) after every single reroute rather than assuming one fix is isolated.

## Detail level: maximal content, simple execution

Default to including **every real trigger** the product actually has — every screen, every action, every decision, every role-gated step — pulled from the product's own documentation, not trimmed down to a "representative" happy path. When someone asks for this to be "simpler" or "clearer," that means simpler *visual execution* (generous spacing, consistent shapes, one accent color, short clear labels), not fewer real steps. Cutting real content to make a diagram look cleaner is the wrong trade — fix it with layout and whitespace instead.

Two practical techniques that keep a maximally-detailed flow readable:

1. **A persistent-features side panel.** Not everything a product does is a sequential trigger. Chat, settings, sharing, notifications, an activity log — these are open the whole time once some precondition exists (e.g. "once the trip/project/document exists"), not a step in the linear path. Pull them out into a clearly labeled zone ("ALWAYS AVAILABLE, ONCE X EXISTS") with one connector into it, instead of interleaving them into the main spine where they don't belong.
2. **Conditional side-branches that rejoin.** A step that only applies sometimes (e.g. "only if X condition is true") belongs as a diamond that branches off the spine, does its thing in a short side column, and rejoins the spine at the next shared step — not forced into every path.

## Actor / role distinction

When a flow has more than one kind of actor (an admin/organizer/owner vs. any member/user), show who can do each step rather than leaving it implicit:

- Mark only the **genuinely exclusive** actions — the ones only that role can do — with a distinct accent color (e.g. a colored border) and a small badge/caption naming the role ("ADMIN ONLY," "OWNER ONLY" — whatever term the product uses).
- Leave everything else in the default/neutral styling, and say so once in the legend ("everything else: any member can do it").
- Don't build full parallel swimlanes unless the flow is genuinely split down the middle between actors (most flows aren't) — the badge approach stays legible for a mostly-shared flow and is much less work to lay out correctly.

## Visual system

- Reuse the product's own design tokens if the project has them (color palette, fonts) — check for an existing design system/canvas first rather than picking fresh colors.
- **Two valid color systems — pick per-request rather than assuming:** (a) *single-accent* — neutral ink/grey strokes on every shape, with one accent color reserved for everything that needs attention (decisions, backward loops, role badges); (b) *semantic-fill* — each shape *type* gets its own light fill + matching border color (e.g. one color for anything a user/group does — both action rectangles and input/output parallelograms share this, since shape already distinguishes the two; a second color for every decision diamond; a neutral/dark fill for start/end), with role-exclusive steps marked by swapping just the *border* to a separate accent color while keeping the same base fill — this preserves "one signal color for something exclusive" even though the base palette is no longer monochrome. Whichever system you use, dashed/loop lines and "No" labels should NOT reuse whatever color is already carrying the role-badge or decision meaning — pick a neutral (ink-soft/grey) for those so no color does double duty.
- Typography: a display face for node titles, a plain body face for sub-labels, generous font-size (titles ~13–15px, sub-labels ~10.5–11.5px at the drawn scale) — this is a diagram people read closely, not a thumbnail.
- Build it as hand-authored inline `<svg>` (rect/ellipse/polygon/path/text — no diagramming library). Lay out coordinates on paper/in your head first: main spine down the center, side branches and loop columns left/right, a side panel for persistent features. Compute shape bounding boxes before placing arrows, and double check two things that are easy to get wrong by hand: (a) side-column shapes don't overlap the main spine's shapes (give at least ~100px clearance), (b) an incoming arrow lands on an edge that's clear of the box's own text, not through the middle of it.

## Delivery

Write a real standalone `.html` file (inline CSS, inline SVG, a Google Fonts link if needed — no build step, no framework). Save it to a sensible location (the user's home directory is fine unless they say otherwise) and deliver it so it opens inline. **Do not publish this as a hosted Artifact** unless the user explicitly asks for a shareable link — a plain file they can open locally is the default expectation for this kind of diagram.

Before sending, open the file in a local browser preview and look at it (scroll the full length). But don't trust a screenshot-zoom tool to judge whether small text overlaps a line — at diagram scale (a 1300–1700px-wide SVG shown in a ~800px pane), a "zoom" that crops a screenshot rather than re-rendering will make fine text look cut off or garbled even when it's actually fine, and you can chase a phantom bug for several edits. The reliable check is to query the live DOM instead: run a small script that calls `getBBox()` on every label `<text>` and compares it against its own background mask (or against nearby arrow path coordinates) to confirm numerically that nothing overlaps — this is exact, instant, and immune to screenshot scaling.

**Give every arrow label its own background mask**, always, not just when something looks wrong. A label text drawn directly over a line will often have the line or an arrowhead visibly cross through it once real coordinates are in play, even when your by-hand layout plan looked clear on paper. The fix that actually holds up: place a small solid rect (matching the page/card background) immediately before each label's `<text>` element, sized a bit larger than the text's expected bounding box (for a monospace label face, ~7px per character at an 11px font size is a safe estimate, plus ~8–10px of padding). This guarantees the line is visually hidden behind the label regardless of small positioning errors — cheaper and more robust than trying to hand-place every label to dodge every line perfectly.

## Worked structure (example skeleton)

```
Start (oval)
  → Sign in / onboard (rectangle)
  → Create / join (rectangle, role-badge if creation is exclusive)
  → [persistent-features connector branches off here into the side panel]
  → Core loop: add/do the thing (rectangle, loop target)
  → Does it pass/fit/validate? (diamond)
      No  → fix-it action (rectangle) → re-check (diamond, role-badge if only one role applies it) → loop back
      Yes → continue
  → [conditional branch if applicable] → rejoin
  → Confirmation / sign-off (parallelogram)
  → All confirmed? (diamond) → loop back if no
  → Finalize (rectangle, role-badge if exclusive)
  → Execute / use it (rectangle)
  → Exception loop if one exists (diamond → side fix → loop back)
  → End (oval)
```

This is a shape, not a template to fill in blindly — the real skeleton always comes from what the product actually does.

## Sources

- Figma, [*What is a user flow?*](https://www.figma.com/resource-library/user-flow/)
- Nielsen Norman Group, [*User Journeys vs. User Flows*](https://www.nngroup.com/articles/user-journeys-vs-user-flows/)
- Interaction Design Foundation, [*User Flows*](https://ixdf.org/literature/topics/user-flows)
