# Report Structure Reference

## Output A: Interactive HTML Report

### Technical Spec
- Single `.html` file — no external dependencies except CDN-hosted chart library (Chart.js or inline SVG)
- Bilingual: Chinese default, English toggle via `data-zh` / `data-en` attributes
- Mobile-responsive (CSS Grid/Flexbox, max-width: 1200px centered)
- No localStorage — all state managed in JavaScript variables

### Bilingual Toggle Implementation

```html
<!-- Language toggle button in header -->
<button id="langToggle" onclick="toggleLang()">EN</button>

<!-- Elements with both languages -->
<span data-zh="用户痛点" data-en="User Pain Points">用户痛点</span>

<script>
let lang = 'zh';
function toggleLang() {
  lang = lang === 'zh' ? 'en' : 'zh';
  document.querySelectorAll('[data-zh]').forEach(el => {
    el.textContent = el.getAttribute('data-' + lang);
  });
  document.getElementById('langToggle').textContent = lang === 'zh' ? 'EN' : '中';
}
</script>
```

### Navigation Structure

```
[Fixed top nav bar]
  Logo / Report Title (bilingual)  |  Nav links  |  中/EN toggle

[Hero section]
  4 key stats with large numbers

[Section 1: 数据概览 / Data Overview]
  - Data collection summary (how many posts, sources, date range)
  - 2 bar charts: mentions by keyword / engagement by platform
  - Key events timeline (relevant news/incidents that explain spike patterns)
  - Core insight box (1-sentence summary of biggest finding)

[Section 2: 用户画像 / User Personas]
  - 4–6 persona cards, each with:
    · Name + role + avatar icon
    · Age / location / device
    · Primary goal
    · Main pain points (2–3 bullets)
    · Representative quote (verbatim)

[Section 3: 核心痛点 / Core Pain Points]
  - Heat score legend
  - 6–10 expandable pain point cards, sorted by heat score (highest first)
  - Each card:
    · Pain point name (bilingual)
    · Heat score indicator (filled dots ●●●●○ or percentage bar)
    · 1-sentence description
    · [Expand] → shows: detailed description, verbatim user quotes (2–3),
      source links, mention count, platform breakdown

[Section 4: 5W1H深析 / 5W1H Analysis]
  - Framework explanation (2 sentences)
  - Pain point selector (tabs or dropdown)
  - For selected pain point: 6-row table (WHO / WHAT / WHEN / WHERE / WHY / HOW)
    · WHY row highlighted in accent color (most important)
    · HOW row includes satisfaction indicator
  - Summary matrix (all pain points × 6 dimensions, collapsible)

[Section 5: 代表性内容 / Key Posts]
  - Filter bar: [全部/All] [小红书] [微博] [Reddit] [X] [黑猫投诉] + keyword filter
  - 10–15 post cards, each with:
    · Platform icon + publication date
    · Title/headline
    · 2-sentence summary
    · Key user quote (verbatim, styled as blockquote)
    · Engagement metrics (likes / comments / shares)
    · [原文链接 / View Original] button → opens in new tab

[Section 6: 机会洞察 / Opportunity Insights]
  - Priority matrix visualization (2×2 grid: Impact vs. Difficulty)
    · Each opportunity placed as a labeled dot
  - 6–8 opportunity cards, each with:
    · Priority badge: P1 / P2 / P3
    · Opportunity name (bilingual)
    · 1-sentence description
    · Target persona
    · Estimated market signal strength
    · Relevant pain points it addresses

[Section 7: 落地建议 / Recommendations]
  - 4 sub-tabs:
    · MVP方向 / MVP Direction — what to build first and why
    · 市场切入 / Go-to-Market — who to target, which channel, what message
    · 风险提示 / Risk Flags — key assumptions that could be wrong; failure modes
    · 投资逻辑 / Investment Thesis — market size framing, defensibility, timing rationale

[Footer]
  - Data sources list with access method (direct / WebSearch fallback / third-party report)
  - Research date and keywords used
  - Disclaimer about data limitations
```

### Color & Design Guidelines

- **Header background**: Dark (e.g., `#1a1a2e` or topic-appropriate dark color)
- **Section backgrounds**: Alternating white `#ffffff` and light gray `#f8f9fa`
- **Accent color**: Choose based on topic (e.g., #e63946 for complaints, #2196F3 for tech, #4CAF50 for growth)
- **Pain point heat dots**: Filled = `#e63946`, Empty = `#dee2e6`
- **P1 badge**: `#dc3545` | P2: `#fd7e14` | P3: `#6c757d`
- **Card hover**: Subtle box-shadow lift (`0 4px 15px rgba(0,0,0,0.1)`)
- **Font**: System font stack — `-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`

### Animations

```javascript
// Animate bars on section load using IntersectionObserver
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.querySelectorAll('.bar-fill').forEach(bar => {
        bar.style.width = bar.getAttribute('data-width') + '%';
      });
    }
  });
}, { threshold: 0.3 });
```

---

## Output B: Excel File (.xlsx)

### Sheet 1: 原始数据 / Raw Data

| Column | Description |
|--------|-------------|
| ID | Sequential number |
| 平台/Platform | Source platform name |
| 关键词/Keyword | Search keyword used |
| 标题/Title | Post title or headline |
| 摘要/Summary | 1–2 sentence excerpt |
| 原文链接/URL | Direct link to original |
| 发布时间/Date | Publication date |
| 点赞/Likes | Like count (0 if unavailable) |
| 评论/Comments | Comment count |
| 转发/Shares | Share count (0 if unavailable) |
| 作者类型/Author Type | 普通用户/Regular user or 营销号/Marketing |
| 痛点标签/Pain Tag | Which pain point category this belongs to |
| 数据来源方式/Access Method | 直接抓取/Direct or 搜索摘要/Search snippet or 报告引用/Report |

### Sheet 2: 痛点分析 / Pain Point Analysis

| Column | Description |
|--------|-------------|
| 痛点名称/Pain Point | Name |
| 热度评分/Heat Score | 0–100 composite score |
| 提及频率/Frequency Score | 0–10 |
| 互动量/Engagement Score | 0–10 |
| 情绪强度/Emotion Score | 0–10 |
| 时效性/Recency Score | 0–10 |
| 影响力/Impact | 1–5 |
| 解决难度/Difficulty | 1–5 |
| 优先级/Priority | P1 / P2 / P3 |
| 代表引用/Quote | Best user quote |
| 涉及平台/Platforms | Comma-separated |
| 数据点数量/Data Points | Count of posts supporting this |

### Sheet 3: 5W1H矩阵 / 5W1H Matrix

| Column | Description |
|--------|-------------|
| 痛点/Pain Point | Name |
| Who | User segment description |
| What | Pain description and desired state |
| When | Time/trigger context |
| Where | Location/touchpoint context |
| Why | Root cause analysis |
| How | Current workarounds + satisfaction |
| 机会信号/Opportunity Signal | Key takeaway for product/business |

### Sheet 4: 机会卡片 / Opportunities

| Column | Description |
|--------|-------------|
| 机会名称/Opportunity | Name |
| 优先级/Priority | P1 / P2 / P3 |
| 影响力/Impact | 1–5 |
| 实现难度/Difficulty | 1–5 |
| 目标用户/Target Persona | Which persona |
| 解决的痛点/Addresses | Pain point names |
| 简述/Description | 1–2 sentence summary |

### Sheet 5: 数据来源 / Data Sources

| Column | Description |
|--------|-------------|
| 平台/Platform | Source name |
| 类型/Type | 社交媒体/行业报告/投诉平台 |
| 访问方式/Access | 直接/搜索摘要/报告引用 |
| 收集条数/Count | Number of data points |
| 关键词/Keywords | Searched keywords on this platform |
| 备注/Notes | Any limitations or caveats |

### Formatting Requirements for xlsx

- **Header row**: Bold, dark background (`#1a1a2e`), white text
- **Heat score column**: Conditional formatting — red (>80), orange (60–80), yellow (40–60), green (<40)
- **Priority column**: Color-coded cells — P1=red, P2=orange, P3=gray
- **URL columns**: Hyperlinked, blue text
- **Auto-fit column widths**: Set appropriate widths so content is readable without scrolling
- **Freeze top row**: Header row frozen for easy navigation
