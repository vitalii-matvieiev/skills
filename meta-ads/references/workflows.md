# The three modes, step by step

Load the section that matches what the person asked for.

---

# Mode 1 — Review

Read-only. Nothing in the account is changed.

## 1. Economics before data

Ask in blocks of three, explaining why the numbers are needed: without them nobody can say whether an enquiry is cheap or expensive.

**Block one:** what is sold and to whom, in one sentence · what a customer pays on average · what is left from that after the cost of delivering it.

**Block two:** out of 100 enquiries, how many pay · whether customers come back and how often · what share of the profit may go into advertising, defaulting to a third.

Calculate the ceiling and show the arithmetic. See `economics.md`.

Stop and re-ask if answers contradict each other — for example profit larger than the average order value. Do not calculate on obviously wrong inputs.

## 2. Can the numbers be trusted

`ads_get_dataset_quality`, `ads_get_dataset_stats`, `ads_get_errors`.

Watch for three things: whether the target event exists at all and how often it fires; whether the pixel and the Conversions API are sending the same event twice without a shared identifier, which halves the apparent cost per conversion and is the most expensive tracking fault there is; and whether there is a gap in the event volume on a specific date, which is almost always a change on the site rather than a change in demand.

If quality is poor, say so first, in plain language, and mark everything below as provisional.

## 3. Pull the data

Window: 30 days against the previous 30, unless another period was requested.

`ads_get_ad_accounts` (ask which account if there are several — never guess) → `ads_get_ad_entities` for structure and budgets → `ads_insights_performance_trend` for both windows → `ads_insights_anomaly_signal` → `ads_insights_industry_benchmark` and `ads_insights_auction_ranking_benchmarks` for external context → `ads_get_opportunity_score` as a source of hypotheses, not instructions.

Group requests. Rate limits are real.

## 4. Four passes

**Structure.** How many campaigns and ad sets run at once. Whether the budget is spread so thin that nothing accumulates enough events to learn. Whether two ad sets compete for the same people inside the same account — self-competition raises the price of both. Whether the campaign objective matches what the business actually sells.

**Money.** Which campaigns consumed 80% of the spend and what they returned. The headline finding is usually not "a bad campaign" but that most of the budget went to something nobody had checked in months.

**Performance.** Every campaign and ad set gets a status from the verdict scale, with its numbers attached.

**Fatigue.** Frequency, click-through rate against its own peak, cost per thousand impressions. Separate creative fatigue from audience exhaustion — different diagnoses, different actions.

**Look at the ads.** Preview the best and the worst performer with `ads_get_ad_preview` in the placement taking the money, and compare them as images. Pass every `preview_url` through as a clickable link. A creative verdict written without opening the preview is a guess dressed up as analysis.

**Check the history.** `ads_account_get_activity_logs` shows what was changed in the period under review and by whom. A cost spike three days after someone doubled a budget is not a mystery — but only if you look.

## 5. Deliver

In the conversation: the ceiling and how it was calculated, in one line · exactly three findings with numbers · a table of campaign / spent / conversions / cost per conversion / ceiling / status · a prioritised plan split into today, this week, and not at all.

Then a standalone HTML report with the full breakdown, the calculations, the per-ad-set tables and the reasoning behind each verdict — written so someone who does not work with ads daily can follow it.

---

# Mode 2 — Launch

Ends with a structure created and **paused**. Nothing starts spending without a separate explicit decision by the person.

Check write access before the interview, not after. If only read access was granted, say so immediately and explain how to change it.

## 1. Interview, three questions at a time

**What and for whom:** what is sold, in one sentence, without a company description · who the customer is — not "everyone", but the specific situation in which someone looks for this · what the person should do after seeing the ad.

**Money:** what a customer pays and what is left from it · out of 100 enquiries how many pay · the test budget and over how many days.

Calculate the ceiling and **check it against the budget**. If the test budget is smaller than three to five ceiling costs per conversion, say directly that this will not buy a readable result: either more budget, or fewer hypotheses.

**Readiness:** where the traffic goes and whether that page is ready · whether conversion tracking is set up · who answers enquiries and how fast.

## 2. Checklist before creating anything

- Tracking configured and events actually arriving — `ads_get_dataset_details`, `ads_get_dataset_stats`
- The target event is frequent enough to learn from. If it happens rarely, optimise for an event higher in the funnel and track the deep one as secondary
- Facebook Page reachable — `ads_get_pages_for_business`
- No existing campaign already targeting the same audience with the same objective — `ads_get_ad_entities`
- Ad copy ready
- Images or video ready. Upload through `ads_creative_upload_image` / `ads_creative_upload_video`, then preview the assembled ad with `ads_get_ad_preview` and look at it before anything goes live
- Before writing copy, `ads_library_search` shows what competitors are actually running in that market — worth five minutes
- Special ad categories — credit, housing, employment, social issues. Ask explicitly; getting this wrong blocks the campaign in review

If a critical item fails, do not create. Name what is blocking and what to do about it.

## 3. Structure

Minimal by design. A complex structure at launch means a diluted budget and no readable conclusion.

One campaign, one objective. One or two ad sets, each testing exactly **one** hypothesis — either the audience or the offer, never both at once, because a combined test cannot be interpreted. Enough budget per ad set to reach roughly 50 target events per week; if that is not possible, use fewer ad sets. Two or three ads per ad set.

Show the structure as a table **before** creating it — campaign / ad set / hypothesis / audience / daily budget / target event / ads — explain each column in plain words, and wait for confirmation.

## 4. Create

Only after confirmation: `ads_create_campaign` → `ads_create_ad_set` per hypothesis → `ads_create_creative` → `ads_create_ad`.

Budgets go in as integers in minor units — €50.00 is `5000`. State the converted figure in the confirmation table. Campaign objectives must be ODAX outcomes (`OUTCOME_LEADS`, `OUTCOME_SALES`, `OUTCOME_TRAFFIC`, `OUTCOME_AWARENESS`, `OUTCOME_ENGAGEMENT`, `OUTCOME_APP_PROMOTION`); the older names are rejected.

Everything stays a draft. Then preview each ad with `ads_get_ad_preview` and hand over the `preview_url` links — seeing the ad as it will actually appear is the last checkpoint before spending money on it.

If a call fails, stop, show the error in plain language, and do not blindly create the rest — a half-built structure is worse than none.

If the ambition is to compare two approaches properly rather than eyeball a report later, check `ads_experiment_check_eligibility` and set up a real split test instead.

## 5. Deliver

What was created, in plain language · three or four things to check before turning it on · **the exit rules, written down before launch**: at what numbers the hypothesis is declared dead, at what numbers the budget goes up · when to come back — not sooner than 3 days or 50 target events.

Exit rules are written before launch because afterwards there is always a reason to give it one more day.

---

# Mode 3 — Weekly

Ends with an executed package of changes. Nothing is changed without an explicit yes to a specific list.

Ask for the target cost per conversion if it is not already known in the conversation. Without it, optimisation is just moving budgets around blindly — say that.

## 1. Read

Window: 7 days against the previous 7.

Start with `ads_account_get_activity_logs` for the period since the last session: what was changed, by whom, from what to what — including Meta's own automated changes. This is the account's own record, so it works even though the conversation remembers nothing. It answers the only question that matters at the start of a weekly cycle: did last week's changes do anything.

Then `ads_get_ad_accounts` → `ads_get_ad_entities` for active entities and current budgets → `ads_insights_performance_trend` → `ads_insights_anomaly_signal` → `ads_get_dataset_quality`.

If tracking quality has dropped since last time, that is the event of the week, not the fluctuation in cost per conversion. Say it first and do not propose changes on distorted data.

## 2. Judge

Assign one status per active ad set using the verdict scale.

For **Scale**: also confirm the budget was not raised in the last 3 days. If reach is exhausted and frequency is high, raising the budget just buys the same people in a more expensive auction — propose duplicating the ad set with a broader audience instead, keeping the original as a control.

For **Fix**: exactly one change with one hypothesis and a 3–5 day window. Not three at once, or next week nobody will know what worked.

For **Stop**: name which of the three conditions fired and say what happens to the freed budget.

When the cause is creative fatigue — high frequency, click-through rate down from its peak, rising cost per thousand impressions — replace the ads, not the ad set. A working audience does not get switched off because the pictures got tired.

## 3. Package and confirm

One table: what / action / current / new / why. Maximum five changes; the rest is "next round", with the reason stated. One line underneath on what is deliberately left alone. One confirmation for the whole package.

If the person edits the package, show the updated table and ask again.

## 4. Execute and report

Order: pauses, then edits, then budget increases.

Report what was executed with the actual new values, what failed and why in plain language, the account's daily spend before and after, and when to check the changed entities — not sooner than 3 days.

## 5. Record the hypotheses

The account logs *what* changed. It does not log *why*. Write five or six lines the person keeps: date, what changed, on which hypothesis, when to review.

Only the reasoning needs keeping. The changes themselves are recoverable next week from `ads_account_get_activity_logs`, so there is no need to ask anyone to maintain a manual ledger of budget numbers.
