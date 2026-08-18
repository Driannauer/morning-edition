# Brave Search Playbook

Use OpenClaw managed `web_search` with provider pinned to Brave. Brave returns structured result snippets and supports freshness and language filters. Use `web_fetch` only after shortlisting.

## Normal 24-hour discovery pass

Run 6-8 broad searches, normally with `count: 10` and `freshness: "day"`. Use English queries for global coverage and repeat one or two relevant queries with Chinese-language terms and `language: "zh"` when useful.

Suggested query themes:

1. Frontier AI models, product launches, research, safety, and major AI companies.
2. AI chips, infrastructure, regulation, and policy.
3. Technology platforms, cybersecurity, semiconductors, cloud, and developer ecosystem.
4. Markets, central banks, macro data, major earnings, deals, and regulation.
5. World affairs, geopolitics, conflict, elections, trade, sanctions, and diplomacy.
6. China-focused AI, technology, economy, policy, and markets.
7. Optional breaking-news sweep for major developments that may not fit a category query.
8. Optional user-specific topic query.

Do not fetch pages during this pass. Work from title, URL, domain, date, and snippet to construct event candidates.

## Time handling

- For a normal last-24-hours brief, use `freshness: "day"`, then filter by event time yourself.
- For multi-day windows, use `freshness: "week"` or explicit `date_after` / `date_before` when supported.
- Search freshness is a discovery filter, not proof that the event itself happened inside the requested window.

## Event normalization

For every candidate, keep a compact event record:

```text
actor | action/development | event_time | source_domain | source_url | confidence_note
```

Merge candidates when actor, action, and approximate event time describe the same underlying event.

## Shortlist gate

After the broad pass, reduce to roughly 12-18 events before deeper searches. Drop:

- duplicate rewrites and syndication;
- pure commentary on old news;
- low-impact product marketing;
- rumors without credible corroboration;
- stale stories whose only new element is republication;
- generic market wrap pieces with no distinct development.

## Targeted verification pass

Use focused `web_search` calls with `count: 5` for shortlisted events. Examples:

```text
<entity> <specific event terms>
site:<primary-domain> <entity> <event terms>
<entity> <event terms> Reuters
<entity> <event terms> AP
```

For Brave, prefer `site:` in the query when you need a specific domain. Do not assume a provider-specific domain-filter parameter exists.

Verification targets:

- Top three: primary source + independent high-quality report when available.
- High-impact or disputed stories: seek two independent evidence paths, with a primary artifact where relevant.
- Lower-ranked routine stories: one strong source may be enough when the claim is straightforward and non-disputed.

## Fetch policy

Use `web_fetch` only for URLs that survived shortlisting.

Normal budget:

- Fetch up to two sources for each top-three story.
- Fetch one strong source for most other selected stories.
- Keep total full-page fetches around 10-14 for a normal edition.
- Exceed the budget only for a material conflict, extraordinary claim, or unclear primary source.

If a page is paywalled, blocked, or JS-only, do not infer hidden details. Use the visible Brave snippet and seek another accessible source.

## Search budget

A normal edition should usually fit within:

- 6-8 discovery searches;
- up to 12 targeted verification searches;
- about 10-14 `web_fetch` calls.

Stop early when the evidence is sufficient. On a major breaking-news day, allow up to four extra targeted searches rather than weakening verification.

## Query quality rules

- Search for entities and concrete actions, not vague editorial questions.
- Use separate queries for separate beats.
- Search both the event and likely primary source when the event matters.
- Do not repeatedly search the same wording after adequate evidence is found.
- If a query returns poor results, broaden once by removing adjectives or date wording; then change the query angle rather than looping.
