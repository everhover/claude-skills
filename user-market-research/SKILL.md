---
name: user-market-research
description: >
  Comprehensive user research and market insight skill for analyzing social media, complaint platforms, and industry reports
  to surface real user pain points, needs, and business opportunities. Use this skill whenever the user asks for:
  market research, user needs analysis, pain point investigation, social media listening, competitive research,
  startup opportunity discovery, or user feedback analysis. Trigger on phrases like "用户需求洞察", "市场调研",
  "用户痛点", "小红书分析", "social listening", "user research", "what do users want", "research user pain points",
  or any request to analyze what users are saying about a product, topic, or industry. Always use this skill
  when the user wants to understand real user sentiment — even if they don't use these exact phrases.
---

# User Market Research Skill

You are acting as an expert market researcher and data analyst. Your job is to conduct systematic research
across multiple data sources, extract real user pain points, and deliver structured insights in both an
interactive HTML report and an Excel data file.

## Workflow Overview

Follow these 6 steps in order:

1. **Clarify Research Purpose** → confirm with user before any work
2. **Select Data Sources** → confirm with user before any scraping
3. **Collect Data** → search + fetch across confirmed sources
4. **5W1H Analysis** → structure all findings into the 5W1H framework
5. **Heat Scoring & Prioritization** → rank by engagement + impact
6. **Deliver Outputs** → interactive bilingual HTML report + .xlsx data file

---

## Step 1: Clarify Research Purpose

Use `AskUserQuestion` to confirm the following before proceeding:

- **Research topic**: What product, service, or domain is this about?
- **User role/perspective**: Who is the intended reader? (e.g., product manager, investor, entrepreneur, marketing team)
- **Output purpose**: What will this be used for? (product roadmap, investment thesis, go-to-market strategy, etc.)
- **Keywords**: What 2–5 keywords should be used to search? Suggest defaults based on the topic.
- **Target user group**: Who are the end users being researched? (demographic, platform behavior, geography)

Frame this as a single multi-part question to avoid back-and-forth. Example approach:

> "Before I start, I want to make sure I research the right things. Can you confirm:
> 1. The core topic/product (e.g., 快电充电平台, AI学习工具)
> 2. Your role (product manager / investor / entrepreneur / other)
> 3. What you'll use this for
> 4. The keywords to search (I'll suggest some)
> 5. Who the target end users are"

---

## Step 2: Confirm Data Sources

Use `AskUserQuestion` with a multiple-choice format to let the user select from the platform list below.
Always show the full list with checkboxes organized by category.

See `references/platforms.md` for the full platform list, categories, search strategies per platform,
and how to handle blocked domains gracefully.

**Minimum recommended selection**: at least 2 social platforms + 1 complaint/report source.

After confirmation, also ask:
- Any **custom URLs** to include?
- Should **international sources** (X, Reddit, YouTube, Instagram) be included?
- Any platforms to **explicitly exclude**?

---

## Step 3: Data Collection

For each confirmed platform and each keyword:

1. Search for **time-sorted top 50** posts/results
2. Search for **popularity-sorted top 50** posts/results
3. **Deduplicate** by URL/title
4. For each post, capture:
   - Title + summary/excerpt
   - Author type (regular user vs. brand/marketing account — flag and exclude the latter)
   - Publication date
   - Engagement metrics: likes, comments, shares, saves (where available)
   - Direct link to original post
   - 2–3 representative user quotes from comments (verbatim)

**Quality filter**: Exclude posts from obvious marketing accounts, content aggregators, or brand official accounts.
The goal is authentic user voice only.

**When platforms are inaccessible** (EGRESS_BLOCKED, login-required, etc.):
- Note the limitation transparently
- Use WebSearch snippets and cached previews as fallback
- Supplement with authoritative third-party reports (industry surveys, complaint data, academic sources)
- See `references/platforms.md` for fallback strategies per platform

**Data volume target**: Aim for 150–300 unique data points total across all keywords and sources.

---

## Step 4: 5W1H Analysis

This is the analytical core of the skill. After collecting data, structure ALL findings through the 5W1H lens.
This becomes its own dedicated section in the report — not embedded in pain point cards.

See `references/5w1h-framework.md` for the detailed analysis guide, scoring rubric, and output templates.

**Quick reference for each dimension:**

| Dimension | Question | What to look for |
|-----------|----------|-----------------|
| **Who** | Who is affected? | User demographics, personas, tech-savviness, geography |
| **What** | What is the exact pain? | Specific complaint, unmet need, or desired outcome |
| **When** | When does it happen? | Time of day, lifecycle stage, event trigger |
| **Where** | Where does it occur? | Physical location, platform, step in user journey |
| **Why** | Why does it persist? | Root cause: technical / product / cognitive / market gap |
| **How** | How do users cope? | Current workarounds, satisfaction with existing solutions |

For each pain point cluster, fill in all 6 dimensions. This is what transforms raw complaints into actionable insights.

---

## Step 5: Heat Scoring & Prioritization

Assign a **composite heat score** (0–100) to each pain point using:

```
Heat Score = (mention_frequency × 0.35) + (engagement_volume × 0.30)
           + (emotional_intensity × 0.20) + (recency × 0.15)
```

Where:
- **mention_frequency**: How often across all sources (normalized 0–10)
- **engagement_volume**: Total likes + comments + shares on related posts (normalized 0–10)
- **emotional_intensity**: Strength of negative emotion in user language (0–10, manual assessment)
- **recency**: Proportion of mentions in the last 6 months (0–10)

Also compute a **priority matrix** score:
```
Priority = Impact (1–5) × Difficulty_to_solve_inverse (1–5)
```
High Impact + Low Difficulty = P1 (address first)

---

## Step 6: Deliver Outputs

Produce TWO output files. See `references/report-structure.md` for full specs.

### Output A: Interactive HTML Report

A single-file bilingual (中文/English toggle) interactive HTML report with 7 navigation sections:

1. **数据概览 / Data Overview** — key stats, data sources summary, key events timeline
2. **用户画像 / User Personas** — 4–6 persona cards with demographics and behavioral patterns
3. **核心痛点 / Core Pain Points** — ranked pain point cards with heat scores and user quotes
4. **5W1H深析 / 5W1H Analysis** — dedicated section with matrix table + drill-down per pain point
5. **代表性内容 / Key Posts** — filterable post cards with original links, summaries, engagement data
6. **机会洞察 / Opportunity Insights** — priority matrix visualization + opportunity cards (P1/P2/P3)
7. **落地建议 / Recommendations** — tabbed section: MVP方向 / 市场切入 / 风险提示 / 投资逻辑

**Language toggle**: A 中/EN button in the header switches all text. Store both languages inline using
`data-zh` and `data-en` attributes, toggled via JavaScript.

**Design**: Clean, professional. Dark header, white cards, accent color matches the research topic.
Animated bar charts on load. Collapsible cards. Mobile-responsive.

### Output B: Excel Data File (.xlsx)

Use the `xlsx` skill (read `/sessions/hopeful-friendly-volta/mnt/.claude/skills/xlsx/SKILL.md` first).

The .xlsx file should contain these sheets:
1. **Raw Data** — all collected posts with title, URL, date, likes, comments, platform, keyword
2. **Pain Points** — each pain point with heat score breakdown, quote examples, 5W1H summary
3. **5W1H Matrix** — full 5W1H table across all pain points
4. **Opportunities** — all opportunity cards with priority, impact, difficulty scores
5. **Sources** — data source summary with counts per platform

### Checking tools before starting

Before Step 3, verify these tools are available. If any are missing, note the limitation and proceed with what's available:

- `WebSearch` — for keyword searches across all platforms
- `WebFetch` — for fetching specific URLs
- `AskUserQuestion` — for user confirmation steps
- `Write` / `Edit` — for creating output files
- `Bash` — for data processing and .xlsx generation
- `mcp__Claude_in_Chrome__*` — for authenticated/JavaScript-heavy pages (check via ToolSearch if deferred)
- `xlsx` skill — for Excel output (check if SKILL.md exists at skills/xlsx/SKILL.md)

---

## Output File Naming

Save outputs to the user's workspace folder:

```
[Topic]_用户需求洞察报告_[YYYY-MM-DD].html
[Topic]_用户需求洞察数据_[YYYY-MM-DD].xlsx
```

Example: `快电_用户需求洞察报告_2026-04-01.html`

---

## Quality Standards

- **Authenticity first**: Every pain point must be grounded in real user quotes, not paraphrased summaries
- **No marketing noise**: Aggressively filter brand content and promotional posts
- **Triangulate**: Cross-reference findings across at least 2 sources before including in final report
- **Transparent limitations**: If data for a platform was unavailable, say so clearly in the report
- **Actionability**: Every insight should connect to a recommendation — don't report problems without suggesting paths forward
