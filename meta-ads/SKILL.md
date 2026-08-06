---
name: meta-ads
description: "Analyse, launch and optimise Meta (Facebook and Instagram) ad campaigns through a connected Meta Ads MCP server. Use when someone asks why their Facebook or Instagram ads are not working, where their ad budget is going, whether their cost per lead is too high, how to launch a new campaign, which campaigns to scale or pause, what changed in the account last week, or asks for an ad account audit or a weekly optimisation pass. Also use when someone asks how to connect their Meta ad account to Claude or cannot get the ads tools to work. Not for Google Ads, TikTok or LinkedIn, and not for website or landing page audits. Українською також — розбери мою рекламу, чому не працює реклама, куди зливається бюджет, скільки коштує заявка, запусти кампанію, що масштабувати, що вимкнути, тижнева оптимізація реклами, як підключити рекламний кабінет."
---

# Meta ads — audit, launch, weekly optimisation

Work on live Facebook and Instagram ad campaigns through the Meta Ads connector: read the account, judge it against the business economics, and change it only with explicit permission.

Respond in the user's language.

Assume the person does not work with ads daily. Explain every term the first time it appears. Never use jargon as if it were shared knowledge.

## Every call, without exception

**`advertiser_request` carries their words, not yours.** Every tool in this connector takes this parameter. Quote the person verbatim, in the language they used. Do not paraphrase, do not translate, do not tidy it into industry vocabulary, and do not restate it as the operation being performed. If they said "заявка подорожчала вдвічі", that sentence goes in — not "analyse cost per lead increase". When they stated a goal earlier and only said "yes, go ahead" now, pass the substantive request, not the confirmation.

**Budgets are in minor units.** A €50.00 daily budget is `5000`. Convert explicitly and show the converted integer in the confirmation table before writing it. This is a hundredfold error on live money if it goes wrong.

## Before anything else: the account gate

Call `ads_get_ad_accounts` and read every field it returns, not just the name:

- `is_ads_mcp_enabled` — the deciding flag. False means the account is unusable, **even when `is_queryable` says true**. The two genuinely disagree on some accounts; this one wins. Show `is_ads_mcp_disabled_reason` verbatim — usually a staged rollout, with nothing the person can do.
- `is_queryable` / `not_queryable_reason` — if false, do not call `ads_get_ad_entities`. But `not_queryable_reason` is frequently just `"Unknown error"`, which tells nobody anything. Fall back to `account_status`: `UNSETTLED` means unpaid or incomplete billing, `DISABLED` means the account is blocked. Say that, rather than repeating "unknown error".
- `currency` — set per account. Calculate the ceiling in the currency of the account being worked on. Never convert silently, never mix currencies in one table.
- `min_daily_budget_cents` — the minimum daily budget, in minor units. It is both proof that budgets are in cents and a hard floor: a proposal below it will be rejected.
- `ad_account_name` and `business_name` can be **empty strings**. Identify the account by `ad_account_id` and ask what it is rather than displaying a blank.

**Accounts denominated in `RUB` are out of scope.** Drop them before any other filtering: never list them, never offer them, never pull their data, never change anything in them, and do not mention them among the unusable ones either. If someone names such an account directly, say briefly that this skill does not work with rouble-denominated accounts and stop there.

**When there are many accounts** — and there often are — filter to the usable ones (`is_ads_mcp_enabled` and `is_queryable` both true), list them briefly with name, currency and status, and let the person choose. Never pick for them. Mention the unusable ones in one line with the reason; knowing which accounts are out of reach and why is useful in itself.

If the tools are missing entirely, or a call fails on access, load `references/setup.md` and walk them through connecting. Do not simulate data, do not produce an illustrative example, and do not describe what the numbers "would probably look like".

## Core rule: money beats dashboard metrics

The ad account reports a cost per lead. A business lives on profit. Confusing the two is the most expensive mistake in advertising.

Order of trust:

1. **Profit per customer against the cost of acquiring them** — the only final answer
2. **Cost per conversion against the ceiling** — the working number for daily decisions
3. **Click-through rate, cost per thousand impressions, frequency, return on ad spend** — explain *why* level 2 broke; never a verdict on their own

Until the ceiling cost per conversion has been calculated, there is no verdict on whether the advertising works. There are only observations. Say this out loud rather than producing a confident-sounding analysis without it.

## The ceiling: what a conversion may cost

Ask for these numbers. Never invent them and never substitute "industry averages".

**Services and lead generation**

- `M` — profit left from one closed deal after the cost of delivering it
- `C` — share of leads that end up paying (0.15 means 15 out of 100)
- `k` — share of that profit the business is willing to spend on advertising; a working default is 0.3

```
ceiling cost per lead = M × C × k
```

Multiply by the average number of purchases per customer if people come back.

**Products and e-commerce**

```
ceiling cost per purchase = average order value × margin share × k
minimum return on ad spend = 1 / (margin share × k)
```

Show the arithmetic step by step with the actual numbers, then translate it: "above this figure per lead, the advertising starts eating the profit."

If the person does not know their numbers, say directly that advertising cannot be *managed* without this figure, only *watched*. Offer a rough estimate from whatever is available and label it as rough.

Full detail: `references/economics.md`.

## Verdict scale

Every campaign and ad set gets exactly one status, always with a number next to it.

| Status | Condition | Action |
|---|---|---|
| **Scale** | Cost per conversion below the ceiling, at least 10 conversions in the window, metrics not deteriorating | Raise budget by 20–30%, no more than once every 3 days |
| **Hold** | Cost per conversion within ±20% of target | Change nothing. Say this as a decision, not as an omission |
| **Fix** | Cost per conversion 20–100% above target, conversions still coming | One change, one hypothesis, checked over 3–5 days |
| **Stop** | The stop rule below triggered | Pause, and record which condition fired |

"Weak campaign" is not a verdict. "Cost per lead 62 against a ceiling of 29, 340 spent, five leads" is a verdict.

## Stop rule: three conditions, not one

Check all three and name the one that fired.

**Money.** More than two ceiling costs per conversion spent with zero conversions → pause.

**Time.** An ad set that has not reached 50 optimisation events in 7 days has a structural problem — audience too narrow, budget per ad set too small, or the optimisation event too deep in the funnel. Rebuild it; do not raise its budget.

**Trend.** Cost per conversion rising across three consecutive readings, frequency on cold audiences above 2.5, click-through rate down by more than a third from its peak → the creative or the audience is burnt out. **Open the ad preview and look at it** before concluding. Replace the ads first; pause the ad set only if that does not help.

## Scaling rule

- Step of **+20–30%** of the current daily budget
- No more than **once every 3 days** per ad set — verify the last change through `ads_account_get_activity_logs` rather than asking the person to remember
- Only for the "Scale" status
- A sharp budget jump resets the algorithm's learning. A series of small steps always beats one large one
- If cost per conversion rises by more than a quarter after an increase and stays there for three days, roll the budget back

## Sample size

**Fewer than 10 conversions in the window is noise.** Nothing can be decided on it, and this has to be said out loud instead of presenting a verdict as if it carried weight.

Default windows: 30 days for a full review (compared with the previous 30), 7 days for the weekly cycle (compared with the previous 7).

## Look at the creative before diagnosing it

`ads_get_ad_preview` returns the rendered ad as an image, for the placement that matters — mobile feed, Instagram feed, Stories, Reels. Use it.

A low click-through rate is equally explained by weak copy, a weak visual and a burnt-out audience. Preview the worst performer and the best performer side by side and compare them as images before naming a cause. A creative diagnosis made without opening the preview is a guess.

Always pass `preview_url` through to the person as a clickable link, verbatim. Describing the ad instead of linking it takes away the one thing they can check themselves.

**Creatives are immutable.** Changing text or media on a live ad is not possible: it means a new creative through `ads_create_creative` and a new ad through `ads_create_ad`. Say so plainly when someone asks to "just change the wording" — it is a new ad, and the old one's learning does not carry over.

## Querying data correctly

`ads_get_ad_entities` needs a specific procedure: choose candidate fields → **verify them with `ads_get_field_context`** → then query. Guessing field names returns empty results rather than errors, which is worse than failing.

Metrics, metric filters and metric sorting all require a time range (`date_preset` or `time_range`, never both). Account-level requests support neither filtering nor sorting. One breakdown per call. To get both best and worst performers, call twice with opposite sort directions.

## Safety protocol for any change

Nothing in the account is changed without an explicit yes to a specific list.

1. Collect every planned change into one package
2. Show it as a table: **what / action / current / new / why** — with budgets shown both as money and as the integer that will be written
3. Cap the package at five changes. Mark the rest as "next round" and explain why: when many things change at once, it becomes impossible to tell what worked
4. Add one line underneath: "what we are not touching, and why"
5. Wait for **one** confirmation covering the whole package. Do not ask item by item
6. Execute in order — pauses first, edits second, budget increases last
7. Check `active_errors` in each response before reporting a change as applied; `updated_fields` only echoes the request

**Anything created stays a draft.** Never call `ads_activate_entity` unless the person explicitly asks to turn something on, and even then show what will start spending and how much per day first.

## Three modes

Identify what the person needs, then load the matching section of `references/workflows.md`:

- **Review** — "why isn't my advertising working", "where is the budget going", "audit my account". Read-only.
- **Launch** — "start a campaign", "I want to advertise". Ends with a structure created as a draft.
- **Weekly** — "what should I scale", "what should I turn off", "check the week". Ends with an executed package of changes.

If the request is ambiguous, ask which one before pulling data.

Open a weekly session with `ads_account_get_activity_logs`: it shows what changed since last time, by whom, with old and new values, straight from the account. That answers "did last week's change work" from evidence rather than from memory.

Before any analysis, check signal quality with `ads_get_dataset_quality` and `ads_get_dataset_stats`. If event quality is poor or events are being counted twice, say so first: every number below it is distorted, and analysis on top of broken tracking produces confidence where there should be none.

The full tool map, including creative uploads, custom audiences, split tests and Ad Library research, is in `references/mcp-tools.md`.

## Honest limits — state these when they matter

- Ad account figures come from Meta's attribution model, not from bookkeeping. A gap of up to a third against a CRM is normal; a gap of several times is a tracking diagnosis, not a reason to switch the ads off.
- Nothing runs between conversations. There is no monitoring and no schedule — but the account's own activity log survives, so history is recoverable even when the conversation is not.
- Requests are rate limited. Group them instead of fetching entities one by one.
- Ad Library search needs at least one active ad account on the login.

## Never

- Produce a verdict before the ceiling cost per conversion is calculated
- Change anything before an explicit confirmation of a specific list
- Turn on something that was created as a draft
- Raise a budget by more than 30%, or more often than once every 3 days
- Diagnose a creative without opening its preview
- Write a budget without converting to minor units and showing the converted figure
- Reassure for the sake of politeness. If the advertising is losing money, say it with a number
