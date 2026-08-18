# Morning Edition Skill

面向 OpenClaw 的高信噪比中文晨间新闻简报 skill。它从实时来源中整理 AI、科技、财经与国际新闻，按事件去重、核验关键事实，并产出约五分钟可读完的编辑式早报。

## 适用场景

可用于以下类型的请求：

- “每日早报”或“晨间新闻简报”
- 过去 24 小时的重要新闻
- AI、科技、财经、国际新闻的定向摘要
- 指定地区、时间范围、篇幅或语气的新闻综述

默认输出为简体中文，覆盖最近 24 小时的 AI、科技、财经/市场和国际事务；通常选择 6–10 条彼此独立的事件。

## 特性

- 以事件为单位去重，避免将同一新闻的多篇转载重复列出。
- 优先使用一手资料和高质量独立报道，并对重要、争议性或市场敏感信息进行交叉核验。
- 按重要性而非发布时间排序，保留必要的数字、时间和背景。
- 每条新闻附一个直达原文链接；无法可靠核验时不会虚构细节。
- 当某个板块没有值得报道的更新时，不会为了凑数而填充内容。

## 运行要求

该 skill 针对 OpenClaw 进行了优化，依赖可用的以下工具：

- `web_search`：由 Brave 提供，用于新闻发现和定向核验。
- `web_fetch`：用于阅读入选来源的正文。

示例 OpenClaw 配置：

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
      },
    },
  },
}
```

请通过 OpenClaw 的配置向导或环境变量提供自己的 Brave 凭据：

```bash
export BRAVE_API_KEY="YOUR_KEY"
```

## 安装

将整个目录保留完整地放到目标 OpenClaw 工作区的 skills 目录中：

```bash
git clone https://github.com/Driannauer/morning-edition-skill.git <workspace>/skills/morning-news-brief
```

安装后目录应包含 `SKILL.md`、`references/`、`agents/` 和 `assets/`。`SKILL.md` 会按需读取 `references/` 内的编辑政策、来源池、搜索策略和输出格式，因此不要只复制单个文件。

## 使用示例

安装并启用后，可以直接用自然语言发起请求：

```text
给我一份今天的早报。
```

```text
整理过去 24 小时最重要的 AI 和科技新闻，控制在三分钟内读完。
```

```text
生成一份面向投资者的中文晨报，重点关注美国市场、半导体和全球宏观事件。
```

显式指定的主题、地区、来源、篇幅、语气和时间范围会优先于默认设置。

## 输出原则

一份正常的晨报会：

1. 先给出最有决策价值的新闻，而不是最新链接的堆叠。
2. 将重复报道合并为一个独立事件。
3. 区分已证实事实、官方声明和仍存在分歧的报道。
4. 在每条新闻末尾提供一个直接原文链接。

完整的搜索、核验、选题和写作规则见 [SKILL.md](SKILL.md) 与 `references/` 目录。

## 目录结构

```text
.
├── SKILL.md                       # 主工作流与质量标准
├── agents/openai.yaml             # 产品展示与调用配置
├── assets/icon.svg                # skill 图标
└── references/
    ├── brave-search-playbook.md   # Brave 检索与核验策略
    ├── editorial-policy.md        # 选题、去重与可靠性规则
    ├── output-format.md           # 成文格式
    ├── source-pool.md             # 来源质量参考
    └── ...
```
