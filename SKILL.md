---
name: zh-distribute
description: Adapt one piece of source content (母本) into platform-native posts for the five main Chinese-distribution surfaces — 掘金 / 微信公众号 / X(Twitter) / 小红书 / B站 — and schedule them on a staggered, anti-spam-friendly cadence. Use when the user wants to repurpose one article/repo-roundup/newsletter into multi-platform Chinese posts, build a "daily pack" of copy-paste-ready variants, or plan a staggered posting schedule. Pure methodology + per-platform dossiers; honest about the fact that auto-posting is blocked on most of these surfaces, so the real zero-cost path is AI-generated copy + manual paste.
whenToUse: The user says "把这篇分发到掘金/公众号/X/小红书/B站", "一键分发", "把母本适配成各平台格式", "做个每日分发包", "错峰排期怎么排", "X thread / 小红书 / 公众号怎么写", or wants one source of truth to become N platform-native posts without rewriting from scratch each time.
---

# 中文分发路由器 — one 母本 → five platform-native posts + staggered schedule

This skill is a **methodology + per-platform dossiers** package. It takes **one structured source block** (the 母本) and turns it into one copy-paste-ready post per target platform, each in that platform's native "头部博主" format, plus a staggered posting schedule. It is distilled from a real daily-pack publisher that produced a 5-minute-paste bundle every morning.

It is **honest about one thing first**, because every other decision flows from it:

## The honest reality of auto-posting on Chinese surfaces

Most Chinese distribution surfaces **cannot be auto-posted to for free.** Do not design a pipeline that assumes otherwise.

| Surface | Auto-post (free)? | Why |
|---|---|---|
| X / Twitter | ❌ | 2025 credits system; Free tier = 0 credits; auto-post returns `402 credits depleted`. |
| 微信公众号 | ❌ | 订阅号 has no write API. |
| 小红书 | ❌ | No official API; cookie-based automation is fragile and against ToS. |
| B站 | ❌ | No open free publish API; dynamic/video upload needs official (restricted) APIs. |
| 掘金 | ⚠️ | Has an API but it is auth-gated and rate-limited; not a reliable free auto path. |

**The real zero-cost distribution model:** the system generates per-platform copy every day (AI produces the variants from the 母本), stores them in one `daily-pack-DATE.md`, pushes the pack to a notification channel (Feishu/Discord/Slack webhook), and a **human spends ~5 minutes pasting** each block into the right platform. AI production + manual distribution. Auto-posting only becomes worth paying for (official paid APIs) once traffic justifies the cost — not before.

So this skill's job is: **make the 5-minute paste as effective as possible**, by giving each platform a faithful native format and a sensible staggered time. It does **not** promise auto-posting.

## What this skill can and cannot do

**Can:** give you the 母本 source-block schema; give you a per-platform dossier (audience, format, length, tone, tags, CTA, gotchas) for 掘金/公众号/X/小红书/B站; give you the per-platform adaptation prompt shape; give you the one-pack output format; give you a staggered schedule and the anti-spam reasoning behind it.

**Cannot:** post for you; bypass platform anti-spam; make X Free-tier credits appear; or guarantee reach — format fidelity raises the floor, it does not buy distribution.

## The 母本 (source block) — one source of truth

Every platform variant is generated from the **same** structured source block. Keep it platform-neutral (no emoji, no platform-specific framing) so adaptation does the work, not the source. Schema:

```
今日日期: YYYY-MM-DD
数据源日期: YYYY-MM-DD

今日选题(母本):
1. <item title>
   链接: <url>
   一句话价值: <what it is / why it matters>
2. ...

机会雷达(可作选题/缺口):
- <one-line opportunity hypothesis>
- ...
```
3–5 items is the sweet spot — enough to fill a thread and a 公众号 section, few enough that 小红书 stays readable. The 母本 is the **only** thing you curate by hand; everything below is generated from it.

## Per-platform dossiers

For each platform, the dossier is the "house style" of the head creators in the tech/AI-tools/open-source lane. The adaptation prompt asks the model to imitate that style strictly and to output **only** the post body (no explanation, no prefix/suffix). Temperature ~0.7 for voice, but the structure is fixed by the dossier.

### 掘金 (Juejin)
- **Audience:** developers; Markdown-literate; rewards technical specificity.
- **Format:** Markdown. Title pattern: `GitHub每日精选 | 今日3个值得关注的开源项目`. Body: a `###` heading per item → repo + GitHub link → technical read (language / core idea / why it's worth following / who it's for). End: `👍点赞+收藏,每日更新` + tags `#GitHub #开源`.
- **Tone:** developer-to-developer; code blocks allowed; no hype words.
- **Length:** 600–1000 字.
- **CTA:** 点赞 + 收藏.
- **Gotcha:** 掘金 dislikes link-farm posts; lead with the technical takeaway, link second.

### 微信公众号 (WeChat Official Account)
- **Audience:** broader tech readers (类比 量子位 / 机器之心 / Github Trending).
- **Format:** Title slightly long with a value hook, e.g. `今日GitHub热门:这3个AI项目值得收藏`. Opening 2 sentences = intro + today's summary. Body = `##` sections, one per item: repo + 简介 + 为何值得关注 + 适合谁. End: `关注+在看,每日更新`.
- **Tone:** accessible but credible; less jargon than 掘金.
- **Length:** 800–1100 字.
- **CTA:** 关注 + 在看.
- **Gotcha:** external links are not clickable inside 公众号 articles; put the repo name prominently and tell readers to search it, or route to a "阅读原文" that leaves the platform.

### X / Twitter
- **Audience:** tech/AI-tools lane (类比 levelsio / 宝玉). Thread format.
- **Format:** Thread. Tweet 1 = hook (`🔥` + a number + a pain point). Each following tweet = one item (repo name + one-line value + link). Last tweet = CTA `Follow @<handle> 不迷路`. Separate tweets with `---`.
- **Tone:** punchy, no filler; 1 emoji per tweet max; each tweet < 200 字.
- **Length:** N+1 tweets for N items.
- **CTA:** Follow.
- **Gotcha:** Free tier cannot auto-post (402 credits); this is a manual paste. Don't tag-spam.

### 小红书 (Xiaohongshu / RED)
- **Audience:** 工具效率号 readers (类比 效率工具指南). Visual-first feed.
- **Format:** Title in `【】` + a number + a pain word, e.g. `【3个AI神器】程序员效率翻倍`. Body: emoji-segmented, each item one line starting with `1️⃣2️⃣3️⃣` → item name + one-line value + link. End: `点❤️收藏不迷路✨` + 8 `#` hashtags (`#GitHub #开源 #程序员 #AI工具 #独立开发 #工具推荐 #效率 #宝藏`).
- **Tone:** enthusiastic, scannable; emoji is structural, not decorative.
- **Length:** < 450 字 (feed cuts long notes).
- **CTA:** 点赞 + 收藏.
- **Gotcha:** external links are suppressed/not clickable; the value is the *save* — make the note worth bookmarking even without a working link. No API; manual paste.

### B站 (Bilibili)
- **Audience:** dev/科技区 viewers; dynamic (动态) + video description lane.
- **Format:** 动态 post: hook title + 3–5 line body (one line per item: name + one-line value) + a pinned link in comments. For a video: the description field mirrors the 动态 body + timestamps. Tags: `#GitHub #开源 #编程 #AI #效率工具`.
- **Tone:** casual, community voice; can be shorter than 公众号.
- **Length:** 动态 140–300 字; description 300–600 字.
- **CTA:** 一键三连 / 关注.
- **Gotcha:** B站 rewards the *video*, not the text; if you only have text, the 动态 + pinned-comment-link is the honest ceiling. No free publish API.

## The adaptation call (shape, not code)

For each platform, one LLM call: a system message setting the persona ("你是<平台>科技/AI工具/开源赛道的头部博主级内容运营,严格按该平台头部博主格式生成内容"), a user message = the platform dossier + the 母本 + "按上述格式生成一条<平台>分发内容。只输出内容本身,不要解释,不要前后缀。". Collect outputs into one pack file. If a platform's generation fails, record the failure inline (`[生成失败: ...]`) and continue — one failed platform must not abort the pack.

## The one-pack output format

```
# 📦 一键分发包 YYYY-MM-DD  (母本日期 YYYY-MM-DD)
> 5 平台 · 各按头部博主格式 · 5 分钟发完

## ── 1. 掘金（复制即发）──
<variant>

## ── 2. 微信公众号（复制即发）──
<variant>

## ── 3. X / Twitter（复制即发）──
<variant>

## ── 4. 小红书（复制即发）──
<variant>

## ── 5. B站（复制即发）──
<variant>
```
Push the pack (or per-platform chunks, capped to the webhook's message size) to your notification channel. A human opens it in the morning and pastes each block. That is the whole loop.

## Staggered schedule (错峰排期)

Do **not** paste all five platforms in the same minute. Two reasons: (a) each platform's algorithm rewards *freshness* on its own clock — posting when its audience is active gets more initial velocity; (b) cross-posting identical content simultaneously is a mild anti-spam signal on several platforms. Stagger by platform peak time.

Suggested times (Beijing time, tech/AI lane; adjust to your audience):

| Platform | Suggested slot | Why |
|---|---|---|
| X / Twitter | 09:00 / 12:00 / 21:00 | Global dev scroll peaks; thread gets re-read across the day. |
| 小红书 | 12:00–13:00 / 20:00–21:00 | Commute + bedtime browse; visual feed favors these windows. |
| 微信公众号 | 08:00–09:00 (morning read) | 订阅号 morning push habit; readers open on commute. |
| 掘金 | 10:00–11:00 / 14:00–15:00 | Dev focus window; better than early morning. |
| B站 | 18:00–22:00 | Evening video/dynamic peak. |

**Anti-spam discipline (non-negotiable):**
- Never paste the **identical** text across platforms in one minute. The variants exist precisely so each platform gets a native-shaped post; use them.
- Respect each platform's daily volume norms. A daily pack is fine; 10 packs/day is spam and will get the account throttled regardless of format quality.
- Keep a CTA consistent across platforms (e.g. the same `@handle` / "每日更新") so cross-platform readers can find you, but let the format differ.
- Manual paste is a feature here: a human in the loop means you read each post once before it ships, which catches the model's occasional hallucinated repo name or broken link before it goes public.

## Honest limits

- **No auto-posting on the free tier** for X/公众号/小红书/B站. This skill generates the copy + schedule; a human pastes. Paying for official APIs is a later-stage decision, not the default.
- **External links are mostly dead on CN surfaces.** 公众号 and 小红书 suppress clickable external links; design each post so it is *worth saving* even without a working link (prominent repo name, searchable).
- **Reach is not guaranteed.** Format fidelity raises the floor of each post; it does not buy distribution. Traffic compounds over weeks of daily posting, not on day one.
- **The model will hallucinate.** Always read the generated variant before pasting — verify repo names and links against the 母本. Manual paste is your last line of defense.
- **Don't spam.** This skill gives you a daily cadence, not a license to flood. Respect each platform's rules and volume norms.
