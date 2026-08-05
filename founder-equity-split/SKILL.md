---
name: founder-equity-split
description: "Split startup equity fairly between co-founders using Mike Moyer's Slicing Pie dynamic equity model. Use when someone asks how to divide shares between founders, whether a 50/50 split is fair, how to account for one founder working full-time while another only invests money, what to do when a co-founder leaves, or mentions Slicing Pie, dynamic equity, or a cap table for an early startup. Українською також — розподіл часток між співзасновниками, хто скільки отримає в стартапі, справедливий поділ бізнесу, партнер вийшов із проєкту."
---

# Slicing Pie — dynamic equity split

Calculate a fair, contribution-based equity split for an early-stage startup, and produce a contribution log the team can keep updating.

Respond in the user's language.

## Core rule

A person's share of the company must equal their share of the **at-risk contributions** — anything given without being paid for at the time.

Every contribution converts into **slices**:

| Contribution type | Multiplier | Why |
|---|---|---|
| Unpaid time, services, unreimbursed use of equipment or IP | **2×** fair market value | Can be re-earned by working elsewhere |
| Cash spent by the company, unreimbursed expenses | **4×** amount | Once spent, it is gone forever |

`slices = value × multiplier`
`share % = person's slices ÷ total slices`

Percentages recalculate every time a contribution is added. Nobody's share is fixed until the freeze event.

## Workflow

### 1. Establish the baseline for each participant

Ask for, and do not guess:

- Name and role.
- **Fair market salary** for that role — what they would be paid for this work at a real employer, annualized. Convert to an hourly rate: `annual salary ÷ 2000`.
- Whether they take any cash salary. Only the **unpaid portion** counts. Someone on a $60k market rate taking $20k cash contributes $40k of at-risk time per year.

If the user cannot name a market rate, help them anchor it against real job postings for that role in their city. Do not let anyone assign themselves a rate they could not actually command — inflated rates are the most common way this model gets broken.

### 2. Collect contributions

For each participant, gather:

- **Time**: hours worked × unpaid hourly rate × 2
- **Cash**: money they put in that the company spent × 4
- **Expenses**: unreimbursed out-of-pocket (travel, subscriptions, hardware) × 4
- **Equipment / supplies**: fair rental or market value × 2
- **IP / existing assets** brought in: fair market value × 2

Ideas alone earn nothing. The idea is worth slices only through the work and money spent making it real. Say this explicitly if a participant expects a share for the idea — it is the single most common point of conflict.

### 3. Calculate and present

Produce a table: participant, slices by category, total slices, current %. Then state plainly what changed versus whatever split they had assumed, and why.

Sanity-check the result against intuition. If the number looks shocking (one founder at 90%), that is usually the model working correctly — but verify the inputs first, especially rates and hours, before delivering it.

### 4. Set the freeze event

The model runs until the pie is "baked", then percentages lock permanently. Trigger events:

- The company can pay market salaries from its own revenue.
- A priced funding round closes.
- The company is sold, or the team agrees to stop.

Make the team name their trigger in advance and write it down. An unnamed freeze event is what turns this model into a dispute.

### 5. Cover the exit rules

Every team must agree on these **before** anyone leaves:

| Departure | Result |
|---|---|
| **Good leaver** — fired without cause, illness, agreed exit | Keeps all accumulated slices |
| **Bad leaver** — resigns without good reason, fired for cause | Loses time-based slices; keeps cash-based slices |

The asymmetry is deliberate: money spent cannot be recovered, unpaid time can be re-earned elsewhere.

### 6. Hand over the log

Offer `assets/contribution-log.csv` — a spreadsheet the team keeps updating weekly. The model only works if logging is a habit; a calculation done once and abandoned is worthless.

## What to warn the user about

Raise these unprompted when relevant:

- **This is not a legal document.** It is internal accounting for contributions. Formalizing it means a co-founder agreement plus issuing shares at the freeze event — a lawyer's job. Read `references/legal.md` before advising on structure.
- **Formalize while the company is still worth little.** Issuing shares for past contributions after the company has real value can be taxed as income in many jurisdictions.
- **Hours measure quantity, not quality.** A slow developer logs more hours than a fast one. Counter this with honest differentiated rates by seniority, agreed by the whole team upfront.
- **Everyone must log honestly.** The model has no defense against inflated hours other than the team's willingness to remove a person who does it.

## References

- `references/methodology.md` — full methodology: mechanics, pros and cons, worked examples, comparison with fixed splits and vesting.
- `references/legal.md` — how to formalize legally, jurisdiction differences, tax timing, investor handling.
- `assets/contribution-log.csv` — contribution log template.
