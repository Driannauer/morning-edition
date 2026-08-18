---
name: morning-news-brief
description: "Create a high-signal Simplified Chinese morning news briefing from live sources. Optimized for OpenClaw with managed Brave web_search and web_fetch, and for agents running GPT-5.6 Sol with xhigh reasoning. Use for morning news, daily digest, today's important news, last-24-hours news, or AI/technology/finance/world-news briefings. Deduplicate at the event level, verify material claims, rank by importance, and target a five-minute read unless the user overrides scope or length."
---

# Morning News Brief

Produce an editor-curated briefing, not a feed dump. Optimize for signal, recency, source quality, and decision usefulness.

## Runtime contract

Read `references/openclaw-runtime.md` before the first run in a new OpenClaw setup or whenever search behavior looks wrong.

- Use OpenClaw managed `web_search` as the discovery tool. The host configuration should pin its provider to Brave.
- Use `web_fetch` only after shortlisting candidate events, to inspect strong primary or independent sources.
- Do not silently substitute model memory, native model search, or another search provider when Brave is required.
- Treat GPT-5.6 Sol and `xhigh` as host runtime configuration, not something this skill changes.
- Use deep reasoning internally for event identity, source conflicts, and ranking. Return conclusions and evidence, not hidden chain-of-thought.

## Workflow

1. Resolve scope.
   - Default language: Simplified Chinese.
   - Default window: the most recent 24 hours ending at execution time.
   - Default sections: AI, technology, finance/markets, and world affairs.
   - Default length: 6-10 event-level stories, normally readable in about five minutes.
   - Preserve explicit user overrides for topics, geography, sources, length, tone, or time window.
   - If the request is simply a morning brief or today's brief, use defaults without follow-up questions.

2. Establish time context.
   - Use the runtime's current local date/time.
   - Interpret relative dates in the user's local timezone when available.
   - Distinguish publication time from event time. Prefer events that occurred or materially changed inside the requested window.

3. Run the Brave discovery pass.
   - Read `references/brave-search-playbook.md` and follow its normal search budget.
   - Search each requested section separately. Do not rely on one generic news query.
   - For a normal 24-hour brief, target roughly 40-70 raw result snippets across 6-8 searches before deduplication when coverage permits.
   - Do not `web_fetch` every result during discovery.

4. Normalize by event, not article.
   - Represent each candidate as: principal actor + material action/development + approximate event time.
   - Merge rewrites, syndication, reactions, and commentary about the same underlying event.
   - Keep follow-up coverage separate only when it contains a genuinely material new development.
   - Retain the strongest source URLs and discard duplicate coverage.

5. Shortlist before deep verification.
   - From snippets, narrow to roughly 12-18 candidate events.
   - Eliminate obvious low-signal stories, stale items, rumors, marketing-only launches, and duplicate market wraps.
   - Use `references/source-pool.md` to judge source strength.

6. Verify material claims.
   - Apply `references/brave-search-playbook.md` for targeted follow-up searches and fetch limits.
   - For the top three stories, prefer a primary source plus an independent high-quality report when both are available.
   - For extraordinary, disputed, geopolitical, security, or market-moving claims, seek independent corroboration even outside the top three.
   - If only an official statement exists, report it as an announcement or claim rather than independently established fact.
   - If a paywalled page is visible only through a snippet, do not infer details beyond that snippet; seek another accessible source.

7. Score and select.
   - Read `references/editorial-policy.md` and score candidates with its 0-10 rubric.
   - Prefer 6+ scores. Include a 5 only for essential context or category coverage.
   - Do not force equal quotas. Let major news dominate, but do not pad quiet sections.
   - Select 6-10 distinct events for the normal edition; use fewer only when there are not 6 credible, worthwhile events in the requested window.

8. Write the briefing.
   - Read `references/output-format.md`.
   - Put the most consequential items first, not the newest links first.
   - For each item, state what happened, preserve the most useful numbers/timing, and add only the background needed to understand the update.
   - Keep facts separate from interpretation and causal speculation.
   - End every story with one direct original-source link using `原文：[来源名称](URL)`. Prefer a primary source; if none is suitable, use the strongest accessible original report. Do not link to a search-results page or aggregator when the original URL is available.
   - Never fabricate a source, quote, number, date, or citation.

9. Quality-check before sending.
   - Confirm every headline represents a distinct event.
   - Confirm all material factual claims are supported by an appropriate source.
   - Confirm relative dates and event timing are internally consistent.
   - Confirm at least several independent source domains are represented when available.
   - Remove hype, filler, duplicated context, and unexplained jargon.
   - Confirm there are 6-10 distinct selected stories unless the day is unusually quiet; confirm every story title is bold, every story body is 80-120 Chinese characters, and every story ends with one direct original-source link.

## Editorial decisions

- Prefer impact over virality.
- Prefer primary evidence and original reporting over aggregation.
- Prefer genuinely new developments over commentary on old news.
- Use Hacker News, GitHub Trending, Reddit, X, and Product Hunt mainly as radar; verify important facts elsewhere.
- For AI research, distinguish peer-reviewed work, preprints, vendor claims, benchmark claims, and independent evaluations.
- For market moves, separate observed price/action from explanations. Do not present one commentator's causal story as settled fact.
- For contested political or geopolitical claims, attribute claims explicitly and distinguish confirmed facts from unresolved reports.

## User customization

Use `references/default-profile.md` when the user has not specified their own topic mix or length. Explicit current-request preferences always override defaults.

## Failure handling

- If `web_search` is unavailable, say a current briefing cannot be reliably produced. Do not fake freshness.
- If Brave is not configured as the managed provider in a setup that requires Brave, do not silently fall back to another provider; surface the configuration problem.
- If one section has no meaningful news, omit it or state that there is no update worth taking space; do not pad.
- If a major claim remains single-sourced, exclude it or label the sourcing limitation clearly.
- If sources disagree on a material fact, present the disagreement briefly rather than manufacturing certainty.
- If `web_fetch` fails, fall back to a targeted Brave search and another accessible source; do not invent missing page details.

## References

- Read `references/openclaw-runtime.md` for OpenClaw, model, and Brave configuration requirements.
- Read `references/brave-search-playbook.md` for query rounds, tool budgets, and verification strategy.
- Read `references/source-pool.md` for source tiers and domain guidance.
- Read `references/editorial-policy.md` for deduplication, reliability, scoring, and editorial exclusions.
- Read `references/output-format.md` when composing the final briefing.
- Read `references/default-profile.md` when the user has not specified topic mix or length.
