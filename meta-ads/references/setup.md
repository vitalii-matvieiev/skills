# Connecting the ad account — the guided walkthrough

Load this whenever the Meta ads tools are unavailable, whenever a call fails on access, or whenever the person asks how to set this up.

Walk them through it **one step at a time**, in their language. Do not paste the whole list at once — ask them to confirm each step before moving on, because almost every failure happens at a specific step and you need to know which one.

Two things you cannot do, and should say plainly if asked: you cannot click through their browser for them, and you cannot log into their Meta account. The connection is authorised with their own credentials in their own Claude settings. What you can do is walk them through it and verify the result the moment it is done.

---

## Step 1 — Check what they have before starting

Ask three questions:

1. Are they using Claude in a browser or the desktop app? (Both work. The menu wording differs slightly.)
2. Do they have a **Meta Business** account that owns the ad account — not just a personal Facebook profile?
3. Are they an admin on that business, or were they given access by someone else?

If they are not an admin, the person who is will have to grant the access in step 4. Say this now rather than after a failed attempt.

---

## Step 2 — Add the connector

In Claude: **Settings → Connectors → Add custom connector**, then paste:

```
https://mcp.facebook.com/ads
```

Menu labels move around between releases. If they cannot find it, tell them to look for "Connectors", "Custom connectors", or "Add integration" in Settings — the item that asks for a URL is the right one.

Official reference page from Meta: https://www.facebook.com/business/help/1456422242197840

---

## Step 3 — Sign in

Claude opens a Meta login window. They sign in with the account that has access to the ads and approve the permissions screen.

No API token, no developer app, no app review. If anything asks them to create a developer app, they are in the wrong flow — go back to step 2.

---

## Step 4 — Grant access per ad account

This is the step people miss. Connecting the account is not the same as granting access to the ads inside it. The permission screen lists the ad accounts and asks for a level **on each one separately**:

| Level | What it allows | When to choose it |
|---|---|---|
| **Read only** | Reading campaigns, metrics, tracking quality | Auditing and weekly reviews. Start here |
| **Read and write** | Everything above, plus creating campaigns and changing budgets | Needed to launch or optimise |
| **Read, write and financial** | Everything above, plus billing data | Only if they specifically want billing. Skip by default |

Recommend read-only first if they are nervous. It is enough for a full audit, and the level can be raised later without redoing the connection.

---

## Step 5 — Verify, do not assume

Tell them to say: *"which ad accounts do I have access to?"*

Call `ads_get_ad_accounts` and read three fields on every account before declaring success:

- **`is_ads_mcp_enabled`** — if false, that account cannot be used at all, **even when `is_queryable` says true**; that combination really occurs and this flag wins. The cause is in `is_ads_mcp_disabled_reason`, usually a staged rollout — nothing they configured wrong and nothing to do but wait.
- **`is_queryable`** — if false, `ads_get_ad_entities` will fail. `not_queryable_reason` is often just `"Unknown error"`, which is worth nothing to them; fall back to `account_status`, where `UNSETTLED` means unpaid or incomplete billing and `DISABLED` means the account is blocked. Tell them that.
- **`currency`** — accounts denominated in `RUB` are out of scope and are filtered out before anything else: not listed, not offered, not queried, and not named among the unusable ones. `currency` and `min_daily_budget_cents` are otherwise per account, and the minimum arrives in minor units, so 4500 on a hryvnia account means 45 per day.
- **`business_name`** — confirm it is the business they expected. People routinely connect a personal profile that has access to an old agency account and wonder why the numbers look unfamiliar. The name sometimes comes back as an empty string; identify by account ID and ask.

Say the account name and ID back to them and ask them to confirm it is the right one before pulling any data.

---

## What goes wrong, and what it actually means

**The tools do not appear at all.** The connector was added but never authorised — the login window was closed or blocked. Redo step 3.

**"Not enabled for this account."** `is_ads_mcp_enabled` is false. The rollout has not reached that account. Nothing to fix on their side; other accounts on the same login may still work.

**Reading works, changing fails.** They granted read-only in step 4. They can raise the level in the connector settings without disconnecting.

**Ad Library search errors out.** That tool requires at least one *active* ad account on the login. An account with no live ads cannot use it, even when everything else works.

**Numbers look like someone else's.** Wrong ad account selected, or a business they had forgotten they still had access to. Go back to `ads_get_ad_accounts` and pick deliberately.

**It worked yesterday and not today.** Meta access tokens expire and business permissions get revoked by admins. Reconnecting in step 2 usually resolves it.

---

## After it connects

Do not immediately pull everything. Confirm the account, then ask what they actually want — an audit, a launch, or a weekly review — and follow the matching mode.

If they have no idea where to start, the audit is the right default: it is read-only, it cannot break anything, and it produces the ceiling figure that every other mode depends on.
