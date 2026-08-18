# OpenClaw Runtime Profile

This skill is optimized for OpenClaw with GPT-5.6 Sol, xhigh reasoning, and Brave Search.

## Required behavior

Configure the model and reasoning level in OpenClaw, not inside the skill. Pin the managed web-search provider to Brave so direct OpenAI Responses routes do not silently select native OpenAI search.

Recommended JSON5 shape:

```json5
{
  agents: {
    defaults: {
      model: { primary: "openai/gpt-5.6-sol" },
      thinkingDefault: "xhigh",
    },
  },
  tools: {
    web: {
      search: {
        enabled: true,
        provider: "brave",
        maxResults: 10,
        timeoutSeconds: 30,
        cacheTtlMinutes: 15,
      },
    },
  },
}
```

Set the Brave credential with the OpenClaw web configuration wizard or in the Gateway environment:

```bash
export BRAVE_API_KEY="YOUR_KEY"
```

For a Gateway install, the environment can be stored in `~/.openclaw/.env`. Do not put the API key in this skill.

## Tool expectations

The agent must be able to call:

- `web_search` for Brave discovery and targeted verification.
- `web_fetch` for readable content at shortlisted URLs.

Do not deny these tools in the active OpenClaw tool policy. A browser is optional and should not be necessary for the normal briefing path.

## Model behavior

- Keep `thinkingDefault: "xhigh"` for the dedicated news agent or session.
- Do not encode the reasoning level in the model id.
- The skill should not change `/model` or `/think` state.
- Use xhigh reasoning primarily for event deduplication, evidence reconciliation, ranking, and synthesis rather than for generating longer prose.

## Installation

Place the whole skill directory under the target agent workspace, for example:

```text
<workspace>/skills/morning-news-brief/
  SKILL.md
  references/
  agents/
```

Or install from a trusted local directory with OpenClaw's local skill installer. The whole directory is required because `SKILL.md` loads reference files on demand.
