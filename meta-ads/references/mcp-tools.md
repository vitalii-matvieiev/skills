# Meta Ads MCP — what the connector actually exposes

Verified against the live connector. Blog write-ups describe an early beta and count twenty-nine tools; the connector actually exposes more than ninety, including whole capability areas those write-ups omit — creative upload and preview, custom audiences, split tests, pixel event configuration, Ad Library research and account change history.

Setup and access problems: see `setup.md`.

---

## Rules that apply to every single call

**`advertiser_request` is required on every tool.** It carries the person's request in **their own words, quoted verbatim**, in the language they used. Do not paraphrase it, do not tidy it up, do not translate it, and do not restate it as the operation you are about to perform. If they said "заявка подорожчала вдвічі, не розумію чому", that exact sentence goes in — not "analyse cost per lead increase". Pull the request from across turns: if they stated a goal earlier and only said "так, давай" now, combine them and pass the substantive request, not the bare confirmation. Leave it empty only for pure greetings. Never put names or contact details in it.

**Budgets are in minor units.** A daily budget of $50.00 is `5000`. Getting this wrong is a hundredfold error on live spend — always convert explicitly and state the converted integer in the confirmation table before writing it.

**Check the account gate first — and read all of it.** Verified against a live account with two dozen ad accounts on it, `ads_get_ad_accounts` returns more than the write-ups mention: `is_ads_mcp_enabled`, `is_ads_mcp_disabled_reason`, `is_queryable`, `not_queryable_reason`, `account_status`, `has_payment_method`, `currency` and `min_daily_budget_cents`.

Accounts whose `currency` is `RUB` are out of scope: filtered out before anything else, never listed, never queried, never modified, and not named among the unusable ones either.

`is_ads_mcp_enabled` decides, and it can be false while `is_queryable` is true — that combination really occurs. `not_queryable_reason` is often the useless string `"Unknown error"`; when it is, read `account_status` instead (`UNSETTLED` = billing, `DISABLED` = blocked) and say what it actually means. `currency` and `min_daily_budget_cents` are per account, so the ceiling maths and every budget proposal belong to one specific account, never to a blended view. Names can come back as empty strings.

---

## Reading the account

`ads_get_ad_accounts` — accessible accounts, paginated in fifties. First call in any session. Business fields show the **owning** business only; agency access does not appear here.

`ads_get_ad_entities` — the workhorse. Campaigns, ad sets, ads or account-level rollups, with metrics, filters, sorting and breakdowns.

Its procedure is not optional:

1. Choose candidate fields
2. **Verify them with `ads_get_field_context`** — it resolves aliases (`spend` → `amount_spent`), returns enum values for filters, and shows which levels support each field. Guessing field names produces empty results rather than errors, which is worse
3. Then call `ads_get_ad_entities`

Constraints worth memorising: metrics, metric filters and metric sorting need a time range — either `date_preset` (`last_7d`, `last_30d`, `last_90d`, `maximum`, …) or `time_range` as JSON, never both. Account-level requests support neither `filtering` nor `sort`. Only one breakdown per call; if a breakdown returns empty, retry without it. Limit caps at 1000, and the tool may return a subset — to get both the best and worst performers, call twice with opposite sort directions.

`ads_get_field_context` — the field catalogue. Call with no arguments to browse everything available.

`ads_account_get_activity_logs` — **the change history**, mirroring the Ads Manager history page: who changed what, when, with old and new values, including Meta's own automated changes. Defaults to the last three months, filterable by category (budget, status, targeting, audience, bid…) and by object.

This tool removes the need for a hand-kept change log. Open a weekly session with it: it answers "what did we change last time and did it work" from the account itself, which no amount of conversational memory could do reliably.

`ads_get_ad_account_pages`, `ads_get_user_pages`, `ads_get_pages_for_business` — Pages available for ads. `ads_get_ig_accounts`, `ads_get_ig_media` — Instagram accounts and their posts.

---

## Insights and benchmarks

`ads_insights_performance_trend` — time-series direction of CPC, CPM, cost per result, ROAS, CTR, CVR and reach. Takes `analysis_level` (`AD` or `ADSET` — one call per level, never combined), an optional `analysis_metric` only when the person named a metric explicitly, plus `conversation_intent` and `conversation_topic` from fixed enums. The main input for the trend limb of the stop rule.

`ads_insights_anomaly_signal` — deviations from the account's own baseline.

`ads_insights_industry_benchmark` — sector comparison. Context, never a verdict.

`ads_insights_auction_ranking_benchmarks` — CTR, CPM and quality against the auction. This is what explains expensive traffic.

`ads_insights_advertiser_context` — industry and geography profile.

`ads_get_opportunity_score` — Meta's own opportunity assessment. A source of hypotheses, not a task list.

`ads_get_customconversions` — custom conversion definitions. Check these before trusting a conversion count.

`ads_get_help_article` — Meta help centre search. Useful for policy questions and review rejections; useless for anything account-specific.

---

## Creatives — and yes, you can see them

`ads_get_ad_preview` renders an existing ad or creative and returns the **creative image itself** as an image content item, plus `preview_url` and `preview_html`. Formats include `MOBILE_FEED_STANDARD`, `DESKTOP_FEED_STANDARD`, `INSTAGRAM_STANDARD`, `INSTAGRAM_STORY`, `INSTAGRAM_REELS`, `THREADS_STREAM`, `RIGHT_COLUMN_STANDARD`, `MESSENGER_MOBILE_INBOX_MEDIA`.

Two consequences:

- **Look at the creative before diagnosing a low click-through rate.** Preview the worst performer and the best performer in the placement where the money is going and compare them as images. A diagnosis of "weak copy" made without opening the preview is a guess.
- **Always include `preview_url` verbatim as a clickable link in the reply.** It is how the person opens the preview themselves. Do not describe the ad instead of linking it.

If a preview by `ad_id` errors on a freshly created draft, retry with the `creative_id` passed to `ads_create_ad` — same creative, different handle.

`ads_get_creatives`, `ads_get_creative_ads`, `ads_get_ad_images`, `ads_get_ad_videos` — existing creative assets.

`ads_creative_upload_image`, `ads_creative_upload_video`, `ads_create_creative`, `ads_creative_update`, `ads_creative_delete` — building new creatives.

**Ad creatives are immutable.** Text, media, headline and call to action cannot be edited on a live ad. Changing copy means: `ads_create_creative` with the new content, then `ads_create_ad` referencing the new `creative_id`. `ads_update_entity` will reject the attempt. Say this plainly when someone asks to "just change the text" — it is a new ad, and the old one's learning does not carry over.

`ads_library_search` — public Ad Library. Search competitors by page, keyword or country to see what is actually running. Requires at least one active ad account on the login. Returns `ad_snapshot_url` per ad — pass those through so they can look. Use it for research before writing copy, not for bulk extraction.

---

## Creating and changing

`ads_create_campaign`, `ads_create_ad_set`, `ads_create_ad` — the build path. Created entities are drafts.

`ads_update_entity` — edits campaigns, ad sets and ads. Takes **Ads API field names, not the create tools' argument names**: a campaign rename is `name`, not `campaign_name`; the budget is `daily_budget`, not `campaign_daily_budget`. Unrecognised names are rejected. Reparenting is rejected. Objectives must be ODAX outcomes (`OUTCOME_LEADS`, `OUTCOME_SALES`, `OUTCOME_TRAFFIC`, `OUTCOME_AWARENESS`, `OUTCOME_ENGAGEMENT`, `OUTCOME_APP_PROMOTION`); legacy values like `CONVERSIONS` or `LINK_CLICKS` are rejected.

After an update, read the response properly: `updated_fields` echoes the request, not the stored state. If `active_errors` is present, the edit landed on an unpublished draft — report it as applied only when `active_errors` is empty.

`ads_activate_entity` — publishes and turns on. **Never call it without an explicit instruction to turn something on**, and even then show what will start spending and the daily amount first.

`ads_boost_ig_post` — promotes an existing Instagram post. Often the right answer for someone who just wants their best-performing post to reach more people, and much simpler than building a campaign from scratch.

---

## Audiences and experiments

`ads_create_custom_audience`, `ads_get_ad_account_custom_audiences`, `ads_get_custom_audience`, `ads_get_custom_audience_adsets`, `ads_update_custom_audience`, `ads_update_custom_audience_users`, `ads_delete_custom_audience`.

`ads_experiment_check_eligibility`, `ads_experiment_abtest_create_test`, `ads_experiment_abtest_get_test`, `ads_experiment_abtest_update_test`, `ads_experiment_lift_create_test`, `ads_experiment_lift_get_test`, `ads_experiment_list_tests`.

A real split test beats eyeballing two ad sets and declaring a winner. When someone wants to compare two approaches properly, check eligibility and set up an A/B test rather than reading tea leaves off a 7-day report.

---

## Signal and tracking

`ads_get_datasets`, `ads_get_dataset_details`, `ads_get_dataset_quality`, `ads_get_dataset_stats`, `ads_get_errors`.

`ads_pixel_event_read` / `_create` / `_update` / `_delete` and `ads_pixel_parameter_read` / `_create` / `_update` / `_delete` — pixel events and their parameters can be inspected **and configured** from here, not just diagnosed.

What to look for: whether the target event exists and how often it fires; whether the pixel and Conversions API send the same event twice without a shared identifier, which halves the apparent cost per conversion and is the most expensive tracking fault there is; and whether event volume drops on a specific date, which is nearly always a site change rather than a demand change.

---

## Catalogue and commerce

`ads_catalog_get_catalogs`, `ads_catalog_get_details`, `ads_catalog_get_diagnostics`, `ads_catalog_get_dynamic_ads_health`, `ads_catalog_get_data_sources`, `ads_catalog_get_feed_rules`, `ads_catalog_get_product_feed_details`, `ads_catalog_get_product_feed_upload_sessions`, `ads_catalog_get_product_details`, `ads_catalog_search_product`, `ads_catalog_get_product_sets`, `ads_catalog_get_product_set_details`, `ads_catalog_get_product_set_products`, `ads_catalog_get_product_product_sets`.

Writes: `ads_catalog_create`, `ads_catalog_update_catalog`, `ads_catalog_product_create`, `ads_catalog_update_product`, `ads_catalog_delete_product`, `ads_catalog_create_product_feed`, `ads_catalog_update_product_feed`, `ads_catalog_product_feed_delete`, `ads_catalog_create_feed_rule`, `ads_catalog_product_feed_delete_rule`, `ads_catalog_create_product_feed_upload_session`, `ads_catalog_create_product_set`, `ads_catalog_update_product_set`, `ads_catalog_product_set_delete`.

Event sources: `ads_catalog_event_source_connect` / `_disconnect` / `_get` / `_get_catalogs` / `_get_health` / `_get_recommendations`.

Order when dynamic ads misbehave: `get_catalogs` → `get_details` → `get_dynamic_ads_health` → `get_diagnostics` → `get_product_feed_details` → specific products.

Three checks: how many products exist against how many are eligible to show, which explains most "the ads run but no products appear" cases; when the feed last refreshed, because a stale feed advertises what is out of stock; and whether product identifiers in the catalogue match those in the pixel events, because if they do not, dynamic retargeting does not work at all while the campaign looks perfectly healthy.

---

## Real limits

**Attribution is a model, not bookkeeping.** A 15–30% gap against a CRM is normal. A gap of several times is a tracking diagnosis.

**Nothing runs between conversations.** Request and response only — no monitoring, no schedule, no reaction to events. Anything phrased as "watch this and turn it off if…" is not a job this can do. But the account's own activity log survives, so history is recoverable even when the conversation is not.

**Rate limits are real.** Group requests, do not fetch entities one at a time, and do not re-query the same data within a session.

**Vague instructions can become live spend.** Every write goes through an explicit package and a confirmation.
