# Output Format

Use this as the default structure. Select 6-10 distinct event-level stories for a normal daily edition. Adapt section count to the actual news mix; do not pad quiet sections.

# 早报｜YYYY年M月D日

> 覆盖：最近24小时 · 共X条 · 预计阅读：约5分钟

## 今天最重要的 3 件事

1. **[一句话标题]** — [一句极简事实摘要。]
2. **[一句话标题]** — [一句极简事实摘要。]
3. **[一句话标题]** — [一句极简事实摘要。]

> 上述 Top 3 只是导读，必须对应下方 6-10 条正式新闻中的三条，不额外增加事件数量。

## AI

### **1. [事实型标题]**
[正文 80-120 个中文字符：核心事实 → 关键数字/时间 → 必要背景或最新进展。不要单列“为什么重要/影响/意义/解读”。]

原文：[来源名称](https://example.com/original-article)

## 科技

### **2. [事实型标题]**
[正文 80-120 个中文字符。]

原文：[来源名称](https://example.com/original-article)

## 财经 / 市场

### **3. [事实型标题]**
[正文 80-120 个中文字符。]

原文：[来源名称](https://example.com/original-article)

## 国际

### **4. [事实型标题]**
[正文 80-120 个中文字符。]

原文：[来源名称](https://example.com/original-article)

[继续按重要性补足至总计 6-10 条；无需每个栏目都有新闻。]

## 今天值得继续关注

- [未来24小时内可能影响新闻面的已知事件、数据、发布、会议或关键节点。]
- [只写已知将发生/值得观察的事项，不写空泛预测。]

## Writing rules

- Select 6-10 distinct event-level stories in total. The Top 3 block is a preview of three selected stories, not three additional stories.
- Make every formal story headline bold. Use the form `### **N. 标题**`.
- For every formal story, write 80-120 Chinese characters of body text. Treat this as a hard default constraint; tighten or expand wording before sending so each item fits the range.
- Keep the body factual and compact: what happened, the most useful figures/timing, and only the background necessary to understand the update.
- Do not add a separate “为什么重要”, “影响”, “意义”, “解读”, or similar commentary field.
- End every formal story with exactly one original-source link on its own line: `原文：[来源名称](URL)`.
- Prefer the primary/authoritative source for the original link. If no suitable primary source exists, use the strongest accessible original report. Avoid aggregators, reposts, tracking redirects, and search-result URLs when the original page is available.
- The per-story original link does not replace internal verification: major claims may still be cross-checked against multiple sources during research.
- Do not append a “主要来源”, “Sources”, bibliography, citation roundup, or source list at the end of the full briefing.
- Use factual, compact headlines. Avoid clickbait, rhetorical questions, and exaggerated adjectives.
- Explain unfamiliar acronyms on first use.
- Prefer concrete numbers and dates when they materially improve understanding.
- If a story is uncertain, place the uncertainty in the first sentence rather than burying it.
- Do not add generic advice, motivational language, or a closing invitation unless requested.

## Optional compact mode

If the user explicitly asks for “极简/3分钟/只看重点”, output 4-6 items unless the user gives another number. Keep bold headlines and one original link per item; body length may be shorter than 80-120 characters only in this explicitly requested compact mode.
