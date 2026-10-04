# dsh-skill-zh-distribute

> A **DeepSeek Harness skill** that turns one piece of source content into platform-native posts for the five main Chinese-distribution surfaces — 掘金 / 微信公众号 / X / 小红书 / B站 — on a staggered, anti-spam schedule.

[简体中文](#简体中文) · [English](#english)

---

<a id="english"></a>
## What it is

`dsh-skill-zh-distribute` is a pure-guidance skill for [DeepSeek Harness (DSH)](https://www.npmjs.com/package/@deepseek-ai/dsh). It is a publishing router: one structured **母本** (source block) → one copy-paste-ready post per platform, each in that platform's native "头部博主" format, plus a staggered posting schedule.

It is **honest first**: auto-posting is blocked on most Chinese surfaces (X Free = 402 credits; 公众号/小红书/B站 have no free write API). The real zero-cost model is **AI generates the per-platform copy → one `daily-pack-DATE.md` → a human pastes each block in ~5 minutes**. This skill makes that 5-minute paste as effective as possible.

What it gives you: the 母本 source-block schema; per-platform dossiers (掘金/公众号/X/小红书/B站: audience, format, length, tone, tags, CTA, gotchas); the adaptation call shape; the one-pack output format; and a staggered schedule with anti-spam reasoning.

What it does **not** do: post for you, bypass anti-spam, make X Free-tier credits appear, or guarantee reach.

## Install (zero-code skill)

DSH discovers skills from the filesystem skill roots (`~/.dsh/skills/`, `<project>/.dsh/skills/`, `~/.agents/skills/`), one level deep: `<root>/<name>/SKILL.md`. The bundled installer links `SKILL.md` into `~/.dsh/skills/zh-distribute/`:

```sh
npx dsh-skill-zh-distribute            # one command (recommended)
# or
npm i -g dsh-skill-zh-distribute && dsh-skill-zh-distribute
# or manual
mkdir -p ~/.dsh/skills/zh-distribute && cp SKILL.md ~/.dsh/skills/zh-distribute/SKILL.md
```

Restart DSH (or let its watcher pick it up). The skill `zh-distribute` appears in the catalog; the model loads it on demand.

> `dsh plugin add` installs Cordis **bundles** (code plugins). A zero-code skill has no bundle, so it loads via the skill filesystem provider — which is what the linker above does.

## Usage

In a DSH conversation, describe the distribution goal; the catalog's "Use when…" routes this skill:

- "把这篇 GitHub 精选分发到掘金/公众号/X/小红书/B站"
- "做一个每日分发包,5 分钟发完"
- "X thread / 小红书 / 公众号 各自怎么写?"
- "错峰排期怎么排?为什么不能同一分钟发五个平台?"

## Example pack

```
# 📦 一键分发包 2026-10-03  (母本日期 2026-10-03)
> 5 平台 · 各按头部博主格式 · 5 分钟发完

## ── 1. 掘金（复制即发）──
### GitHub每日精选 | 今日3个值得关注的开源项目
...

## ── 2. 微信公众号（复制即发）──
今日GitHub热门:这3个AI项目值得收藏
...

## ── 3. X / Twitter（复制即发）──
🔥 3 个今天挖到的 AI 宝藏
---
repo名 · 一句话价值 · 链接
...
Follow @<handle> 不迷路

## ── 4. 小红书（复制即发）──
【3个AI神器】程序员效率翻倍
1️⃣ ... 2️⃣ ... 3️⃣ ...
点❤️收藏不迷路✨ #GitHub #开源 ...

## ── 5. B站（复制即发）──
动态:今天3个宝藏项目👇 ...
```

## Honest limits

- **No free auto-posting** on X/公众号/小红书/B站. AI copy + manual paste is the zero-cost path; paid official APIs are a later-stage decision.
- **External links are mostly dead on CN surfaces** (公众号/小红书 suppress them). Design each post to be worth *saving* even without a clickable link.
- **Reach is not guaranteed** — format fidelity raises the floor, traffic compounds over weeks.
- **The model hallucinates** — read each variant before pasting; manual paste is your last defense.
- **Don't spam** — daily cadence, not flood; respect each platform's volume norms.

## License

MIT.

---

<a id="简体中文"></a>
## 这是什么

`dsh-skill-zh-distribute` 是 [DeepSeek Harness (DSH)](https://www.npmjs.com/package/@deepseek-ai/dsh) 的纯指导 skill,一个发布路由器:一条结构化**母本** → 每个平台一条"复制即发"的本土化帖子(掘金/公众号/X/小红书/B站),外加错峰排期。

**先说大实话**:中文分发平台大多**不能免费自动发**(X Free = 402 credits;公众号/小红书/B站无免费写 API)。真正零成本的模型是 **AI 生成各平台文案 → 存一个 `daily-pack-DATE.md` → 人 5 分钟复制粘贴**。本 skill 就是让这 5 分钟粘贴尽量高效。

给你的:母本 schema、五平台 dossier(受众/格式/长度/口吻/标签/CTA/坑)、适配调用形状、分发包输出格式、错峰排期+反垃圾理由。**不给**你:替你发、绕过反垃圾、凭空给 X Free 额度、保证流量。

## 安装(零代码 skill)

DSH 从文件系统 skill 根(`~/.dsh/skills/`、`<项目>/.dsh/skills/`、`~/.agents/skills/`)一层深发现 `<root>/<name>/SKILL.md`。本包带一键安装器:

```sh
npx dsh-skill-zh-distribute          # 推荐:一键链接
# 或
npm i -g dsh-skill-zh-distribute && dsh-skill-zh-distribute
# 或手动
mkdir -p ~/.dsh/skills/zh-distribute && cp SKILL.md ~/.dsh/skills/zh-distribute/SKILL.md
```

链好后重启 DSH,`zh-distribute` 出现在目录里,模型按需加载。

> `dsh plugin add` 装的是 bundle(代码插件);零代码 skill 走 skill 文件系统 provider,用上面的链接器。

## 用法

在 DSH 对话里直接描述分发目标,目录里的 "Use when…" 会自动路由:

- "把这篇 GitHub 精选分发到掘金/公众号/X/小红书/B站"
- "做一个每日分发包,5 分钟发完"
- "X thread / 小红书 / 公众号 各自怎么写?"
- "错峰排期怎么排?为什么不能同一分钟发五个平台?"

## License

MIT。
