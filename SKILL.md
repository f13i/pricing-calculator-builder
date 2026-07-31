---
name: pricing-calculator-builder
description: Build a live, interactive pricing calculator or decision model as a spreadsheet — toggle-driven scenarios, cost/price curves, a hard floor clamp, and a capped lever stack. ALWAYS use this skill when Farhan is building a pricing MODEL, CALCULATOR, decision model, interactive pricing spreadsheet, margin/floor calculator, a per-unit rate card with volume bands, or a toggle between pricing scenarios (per-game vs per-league, per-seat vs usage, monthly vs annual). Trigger on "build a pricing calculator", "a model where I can toggle X vs Y", "a sheet that clamps to the floor", "margin calculator", "rate card with volume discounts", or when he's iterating on the numbers in an existing model. This produces the WORKING SPREADSHEET. When he wants the recommendation, memo, or comp plan (the argument), use pricing-proposal-builder instead — the two pair, and the calculator feeds the proposal.
---

# Pricing Calculator Builder

This builds the *tool*, not the argument. `pricing-proposal-builder` produces the recommendation a CEO reads; this produces the live spreadsheet Farhan (and often the client's operator) drives — the one with a toggle cell, a cost/price curve, and a floor that can't be breached no matter what discounts stack. They pair constantly: on the AirPLAi rec-league deal he built a 7-tab decision model *and* a strategy memo in the same session. When both are needed, build the calculator first — its numbers feed the proposal.

The reason a calculator is its own deliverable: a memo asserts a price; a calculator lets someone *move the levers and watch what breaks*. Its whole value is exposing the margin squeeze that a static table hides. If the model quietly protects the user from ever seeing the floor get hit, it has failed at the one thing it exists to do.

## Before you build: load the context

1. **The deal file** — `30-deals/<client>/index.md` (obsidian tools). Prior pricing decisions, current cost basis, what the client actually sells, who decides.
2. **Any prior model** — if you're iterating, read the existing sheet's structure before changing it, so you don't strand cell references (see the modeling laws).
3. **The lessons log** — `20-agents/07-lessons.md`, section `client-intel / pricing-models`. These are hard-won corrections from past model builds; read them as pre-flight checks.
4. **Pricing philosophy** — `10-brain/02-business.md` if the client's cost structure or f13i's margin stance isn't already in the deal file.

## The modeling laws (non-negotiable — every one came from a real correction)

**1. Never price below cost — and enforce it as a clamp, not a warning.** The floor is cost. A model that lets stacked discounts push price under cost and then prints a red "warning" has already failed. Enforce it in the formula:
```
discount = MIN(1 - cost/list, band_discount + lever_discount)
price    = MAX(cost, list * (1 - discount))
```
The `MIN`/`MAX` do the protecting. A human ignoring a warning cell is not protection.

**2. Cost and price are separate levers — never let cost fall as a byproduct of deal size.** Volume driving *price* down is a pricing choice. Time/maturity driving *cost* down is a separate, deliberate assumption. The classic error (caught on AirPLAi): a cost/unit that declines as the client's volume rises, which secretly bakes in "we get cheaper over time" and masks the exact margin squeeze the model should expose. Keep cost flat at today's number unless a clearly-labeled time/maturity toggle moves it.

**3. Levers stack, but the stack is capped and floor-clamped.** A lever stack (e.g. +5.5% per lever, max 3 → 16.5%) is fine — but the total discount still passes through the `MIN` floor clamp above. No combination of band + levers can ever break the floor.

**4. Anchor to the right competitor.** Undercut the *premium* incumbent to look like a deal; never chase the *below-cost commodity* — matching a price beneath your own cost is the trap the floor exists to prevent. Put the competitive anchors in the model as reference lines, not just prose.

## Build it

Use the `xlsx` skill for the spreadsheet mechanics (read its SKILL.md before building). Hold this shape, adapting tabs to the deal:

- **Inputs** — one tab, one home for every assumption: cost/unit, list/unit, volume bands, lever definitions, competitor anchors. Everything downstream references here, so a single edit re-prices the whole model.
- **Scenario tabs** — one per pricing mode (e.g. per-game, per-league). Each mirrors the same floor-clamp math so they're comparable.
- **A control/toggle cell** — a single labeled cell that switches the recommendation readout between scenarios. This is what makes it a calculator and not a table.
- **Competitive map** — the anchors as reference points against your recommended price.
- **Deal levers** — the lever stack with the running clamped discount and resulting price.
- **Recommendation** — the headline price *and a live margin read-out beside it* so the person driving the sheet always sees what the current settings do to margin.

## Verify before handing it over

A pricing model with a silent formula error is worse than no model. Before you ship:

- **Toggle every mode** and confirm each re-prices correctly.
- **Push discounts to the max** and confirm the price holds at the floor (cost), never below.
- **Zero formula errors** — no `#REF!`, `#DIV/0!`, or a `VLOOKUP`/`XLOOKUP` silently returning 0 because a range didn't move. After *any* layout change (inserted rows, a header, a logo), re-derive every cell reference from a fresh view of the sheet — a lookup over the wrong range fails without complaint.
- **CFO pressure test the numbers** — "what's my margin at max discount? what happens if cost rises 10%? where does this lose money?" If the model can't answer, it's not done.

## After the build

1. **File it to the deal** — the model belongs in `30-deals/<client>/` beside the deal index, not loose in the outputs folder. Hand off to the `deal-filer` skill (it places the artifact and updates the index + frontmatter), or do it directly.
2. **Log lessons** — append any new modeling correction to `20-agents/07-lessons.md` under `client-intel / pricing-models`, using the entry format. If Farhan corrected a formula or an assumption, that's a lesson — capture it so the next model starts above this one.
