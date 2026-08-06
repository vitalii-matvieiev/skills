# The economics behind every verdict

Load this when calculating the ceiling, when the person does not know their numbers, or when a verdict needs to be justified.

## Why the ceiling comes first

A campaign with a return on ad spend of 1.8 can be losing money. A campaign with an "expensive" cost per lead can be the most profitable thing in the account. Neither statement can be evaluated from the ad dashboard alone, because the dashboard does not know the margin, the sales conversion rate or the repeat purchase behaviour.

So the sequence is fixed: economics first, data second, verdict third. Skipping the first step produces analysis that sounds authoritative and means nothing.

## Services and lead generation

Four numbers, asked in plain language:

| Symbol | Question to ask | Common mistake |
|---|---|---|
| `M` | "How much is left from one deal after everything it costs you to deliver it?" | People answer with revenue, not profit. Ask again if the number looks like a price |
| `C` | "Out of 100 enquiries, how many end up paying?" | Guessed from feeling rather than from records. If they guess, mark the result as an estimate |
| `k` | "What share of that profit are you willing to spend to get one customer?" | Unstated. Default to 0.3; go to 0.5 only when deliberately buying growth |
| repeat | "Does a customer come back, and how many times on average?" | Ignored, which understates the ceiling badly for recurring businesses |

```
ceiling cost per lead = M × C × k × average purchases per customer
```

Worked example, spoken out loud rather than left as algebra: profit per deal 800, one in eight enquiries pays, willing to spend a third of the profit, no repeat purchases → 800 × 0.125 × 0.3 = 30. Anything above 30 per enquiry is either a loss or an experiment being paid for on purpose.

**Count leads in the CRM, not in the ad account.** The dashboard counts form submissions; the business counts money. The gap between the two is itself a diagnostic number worth naming.

## Products and e-commerce

```
ceiling cost per purchase = average order value × margin share × k
minimum return on ad spend = 1 / (margin share × k)
```

Ask whether returns and refunds are already deducted from the margin. They usually are not, and on physical products this can move the ceiling by a fifth.

## Launches and course-style products

Registration cost cannot be judged on its own. Route it through the conversion into payment:

```
ceiling cost per registration = price × margin share × registration-to-payment rate × k
```

Add a time constraint the other models do not have: spend that keeps acquiring an audience after the sales window closes is a cost with no verdict attached. Check the calendar before judging the numbers.

## When the numbers are not available

Do not fabricate them and do not reach for benchmarks as a substitute. State the consequence directly: advertising cannot be managed without this figure, only watched.

Then offer the fallback and label it clearly — comparative analysis. Rank campaigns against each other and against `ads_insights_industry_benchmark`, and say explicitly that this ranks relative performance without answering whether any of it is profitable.

Getting the person to find their margin and their sales conversion rate is usually the single most valuable outcome of a first session.

## Reading the second and third levels

Once the ceiling exists, the dashboard metrics become useful as explanations rather than verdicts.

| Symptom | Most likely reading |
|---|---|
| Cheap clicks, expensive conversions | The offer or the landing page, not the ads |
| Expensive clicks, good conversion rate | Auction pressure or a narrow audience — check `ads_insights_auction_ranking_benchmarks` |
| Click-through rate falling, frequency rising, cost per thousand impressions rising | Creative or audience fatigue. Replace ads before pausing the ad set |
| Conversions in the dashboard, none in the CRM | Tracking, almost certainly duplicated or misattributed events |
| Sudden change on a specific date | Something changed on the site or in the account that day. Find the date first, theorise second |

One problem gets one cause. A list of five "possible reasons" is a refusal to analyse — if the data genuinely does not support a single cause, say which data is missing instead.

## Tone of a verdict

- Number first, conclusion second
- Prioritise: what to do today, what this week, what not to do at all
- No "it is worth noting", "it is important to consider", "overall not bad"
- If the advertising is losing money, say it with the figure attached
