# harvey vault updates, 2026-10-27 (pending: no vault access in the cloud session)

Apply with business-doc-update in a session that has the obsidian tools. Read each target first and match its heading levels and bullet style.

## 1. NEW NOTE: 70-projects/f13i-labs/harvey.md

---
type: project
product: harvey
repo: f13i/harvey
status: v0 built, not live
first_client: reflex-security
updated: 2026-10-27
---

# harvey
harvey is the closer: pricing answers, discount calls, negotiation moves and contract language for reps in Slack, from each company's own playbook. It's internal to the customer's team and never talks to buyers.

How it works
- guard.js is plain code that does every price and discount. Floor clamp, volume bands, give-get levers capped, per-product rep authority. Three outcomes: within_policy, needs_approval (DM to the approver with Approve / Reject), below_floor (nobody can approve it).
- Haiku routes and Sonnet answers, from five layers: f13i method (brain/), company playbook, approved lessons, approver precedent, commons. The model never does price math.
- Learning: `@harvey learn` and `@harvey outcome` draft lessons. Style lessons apply on their own; policy lessons wait for the approver. Approved exceptions become precedent.
- Commons: anonymized cross-company patterns, give-to-get, `share: false` opts out. Code leak scan plus human approval.

State (Oct 27)
- Repo f13i/harvey on main. 10/10 guard tests pass. AI side never run live (no API key yet).
- Registered in f13i-labs-ops (PR #1 merged): products.json, sources.json (usage at ~/f13i/harvey/data/reflex-security/usage.jsonl), labs.json, AGENTS.md.
- Slack: private mode. Answers only Farhan (U0BQS7W7HCJ) by DM, approvals to Farhan. At GA: public channel, Marlow (U0A8GSRADQ8) approves. Checklist in the harvey readme.

Next
1. Review brain/ (drafted in Farhan's voice) and the proposed tier floors.
2. `npm run eval` with ANTHROPIC_API_KEY (15 Reflex questions with traps).
3. Create the Slack app from slack-manifest.yml in the Reflex workspace, fill in .env, `node src/slack.js`.
4. GA once Farhan is happy. Marlow becomes approver.

## 2. APPEND: 30-deals/reflex-security/index.md (log section)

**2026-10-27: harvey built for Reflex**
- Built harvey (f13i labs deal copilot), first client Reflex. The playbook is in f13i/harvey under playbooks/reflex-security/, built from the working-sessions doc, deal tracker, signed order forms, Carahsoft agreement and 15 Granola calls through Oct 26.
- Playbook encodes: $15K land tabletop (reps can't discount; under $15K goes to Farhan; $10K hard floor); give-gets +5% each, max +10%, annual tiers only; Carahsoft not quotable until the price list is posted.
- Proposed (needs Farhan's OK): provisional tiers A $25K list / rep to $20K / floor $15K, B $40K / $30K / $20K, C $65K / $50K / $40K.
- Decided: private to Farhan until GA, then public channel with Marlow as exception approver.
- Open for the Nov 2 / 9 / 16 sessions: unit of the annual (exercise count vs entity vs unlimited), list price on order forms ($150K vs $105K vs $75K), Carahsoft MSRP, Y2 renewal standard, VAR margin.
- Data fix: Granola "$909K" for 909 Cyber is really $10K (per the transcript).

## 3. APPEND: 10-brain/02-business.md (f13i labs products section)

**harvey**: 2026-10-27
- Status: v0 built (f13i/harvey), private pilot for Reflex. Not priced.
- What: deal copilot in Slack (pricing, discount calls, negotiation, contract language) with a floor no one can break, approvals and learning.
- Next move: live eval, then Slack pilot (Farhan only), then GA with Marlow as approver.

## 4. APPEND: 10-brain/04-workflows.md

### harvey: run and teach
**Trigger:** a rep (or Farhan, pre-GA) has a pricing, discount, negotiation or contract question on a live deal.
**Steps:**
1. DM harvey (pre-GA) or @harvey in the sales channel (post-GA).
2. Out-of-policy asks DM the approver with Approve / Reject. The decision becomes precedent.
3. When harvey is wrong: `@harvey learn <correction>`. The approver approves policy lessons.
4. When a deal closes or dies: `@harvey outcome <what happened>`.
5. Weekly: `node bin/harvey.js gaps` to see what the playbook couldn't answer, then update playbooks/<company>/.
6. Deterministic price check, no model: `node bin/harvey.js quote <sku>:<qty> --discount N --gets a,b`.

## 5. Stale flags (tell Farhan, don't edit)
- LegalZoom ($75K) and Rackspace ($75K) in the Reflex pipeline: no status since September.
- Reflex engagement end date (~Dec 15, inferred as 120 days from Aug 17): confirm.
