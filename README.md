<div align="center">

# pricing-calculator-builder

**A [Claude Code](https://claude.com/claude-code) skill that builds a live pricing calculator you can drive — move the levers and watch what breaks.**

Floor clamp that can't be breached. Capped lever stack. Toggle between pricing scenarios.

`pricing` · `spreadsheet-modeling` · `margin` · `rate-card`

</div>

---

## What it is

This builds the *tool*, not the argument. Where
[pricing-proposal-builder](https://github.com/f13i/pricing-proposal-builder) produces the
recommendation a CEO reads, this produces the live spreadsheet you (and often the client's
operator) actually drive — the one with a toggle cell, a cost/price curve, and a floor
that can't be breached no matter what discounts stack.

The reason a calculator is its own deliverable:

> A memo asserts a price. A calculator lets someone **move the levers and watch what breaks.**

Its whole value is exposing the margin squeeze that a static table hides. If the model
quietly protects the user from ever seeing the floor get hit, it has failed at the one
thing it exists to do.

## The modeling laws it enforces

Every one came from a real correction on a real deal:

- **Never price below cost — enforce it as a clamp, not a warning.** `price = MAX(cost, list * (1 - discount))`. The `MIN`/`MAX` do the protecting; a human ignoring a red warning cell is not protection.
- **Cost and price are separate levers.** Volume driving *price* down is a pricing choice; time driving *cost* down is a separate, deliberate assumption. Never let cost fall as a byproduct of deal size and secretly mask the squeeze.
- **Levers stack, but the stack is capped and floor-clamped.** No combination of band + levers can ever break the floor.
- **Anchor to the right competitor.** Undercut the premium incumbent; never chase the below-cost commodity.

## Use it

In Claude Code, trigger it with requests like *"build a pricing calculator,"* *"a model
where I can toggle per-seat vs usage,"* or *"a margin calculator that clamps to the
floor."* It builds the spreadsheet, then verifies it: toggles every mode, pushes discounts
to the max to confirm the floor holds, and checks for silent formula errors before
handing it over.

## Install

```bash
git clone https://github.com/f13i/pricing-calculator-builder.git \
  ~/.claude/skills/pricing-calculator-builder
```

Then invoke it by describing a pricing model, or by name. It pairs with
[pricing-proposal-builder](https://github.com/f13i/pricing-proposal-builder) — build the
calculator first; its numbers feed the proposal.

---

This is one skill from **[f13i-cli](https://github.com/f13i/f13i-cli)** — the AI
chief-of-staff I use to run [f13i](https://f13i.com), my SaaS pricing consultancy. It's
published as a **reference architecture**: written against my own vault and tooling, with
all client and personal details replaced by placeholders. My pricing background is four
years at Grafana Labs (previously — Sr. Manager, Commercialization & Pricing); the system
here is my own.

**License:** [MIT](LICENSE)
