# 5W1H Analysis Framework

## Overview

The 5W1H framework transforms raw user complaints and feedback into structured, actionable insights.
It answers the six fundamental questions about every user pain point. This becomes its own dedicated
section in the final report — NOT just a sub-item inside pain point cards.

## The Six Dimensions

### WHO (谁 / 用户画像)
**Question**: Who experiences this pain point?

Capture:
- **Demographics**: Age range, gender distribution, geography (tier-1 vs tier-3 city, urban vs rural)
- **Tech-savviness**: Early adopter / mainstream / late majority / non-tech
- **Occupation / lifestyle context**: Student, professional, parent, senior, freelancer
- **Platform behavior**: Power user vs. casual, mobile-first vs. desktop
- **Psychographic**: Price-sensitive, convenience-driven, status-conscious, efficiency-focused

Output format per pain point:
```
WHO: 主要为25–35岁职场白领，三线以下城市占比约40%，移动端为主，
     对价格敏感但更看重便利性；英文版: Primarily 25-35 year old
     white-collar workers, ~40% from tier-3+ cities, mobile-first,
     price-aware but convenience-driven.
```

---

### WHAT (什么 / 痛点描述)
**Question**: What exactly is the pain, and what is the desired outcome?

Capture:
- **Current state**: What is the user experiencing that they dislike?
- **Desired state**: What outcome do they want instead?
- **Gap statement**: The specific delta between current and desired
- **Verbatim quote**: At least one real user quote that captures the essence

Output format:
```
WHAT: 用户想找附近有空位的充电桩，但APP显示信息与实际严重不符，
      导致"空跑"现象频发。期望：实时准确的占用状态 + 到达前预约功能
      英: Users want accurate real-time charger availability but app
      data is stale, causing wasted trips. Desired: real-time status + reservations.
```

---

### WHEN (什么时候 / 时间维度)
**Question**: When does this pain point occur?

Capture:
- **Time of day / week / season**: Is this peak-hour problem? Weekend problem?
- **User journey stage**: Discovery → consideration → purchase → usage → support → renewal
- **Trigger event**: What specific moment or action causes the pain to surface?
- **Frequency**: How often does the user encounter this? Daily / weekly / per-transaction?
- **Duration**: How long does the pain last each time?

Output format:
```
WHEN: 主要发生在节假日、周末、雨天等用车高峰期。
      用户旅程阶段：使用中（寻找充电桩时）。
      触发点：打开APP搜索附近充电站。频率：每次充电均可能遇到。
      EN: Primarily during holidays, weekends, rainy days (peak demand).
      Trigger: opening the app to search for nearby chargers. Frequency: every charging session.
```

---

### WHERE (在哪里 / 场景维度)
**Question**: Where does this pain point occur?

Capture:
- **Physical location**: Highway, urban parking garage, residential area, shopping mall, highway rest stop
- **Digital touchpoint**: Which screen, app feature, or step in the digital flow
- **Platform context**: Which social platform are users venting on? (indicates severity/community)
- **Geographic patterns**: Is this problem worse in certain regions or city types?

Output format:
```
WHERE: 物理场景：高速公路服务区、大型商场地下停车场；
       数字触点：APP首页地图 → 选桩 → 导航到桩这一流程；
       投诉平台：黑猫投诉、小红书为主要吐槽阵地
       EN: Physical: highway rest stops and mall parking garages.
       Digital touchpoint: map → charger selection → navigation flow.
       Complaint hub: Heimao + Xiaohongshu.
```

---

### WHY (为什么 / 根本原因)
**Question**: Why does this pain point exist and persist?

This is the deepest analytical dimension. Identify the ROOT CAUSE, not just the symptom.

Cause categories:
- **Technical**: System architecture limits, real-time data sync failures, hardware reliability
- **Product/UX**: Poor information architecture, missing features, confusing flows
- **Cognitive**: User mental model mismatch, terminology confusion, learning curve
- **Market/structural**: Incentive misalignment, fragmented ecosystem, regulatory issues
- **Business model**: Cost pressures that lead to underinvestment in quality
- **Data quality**: Inaccurate third-party data feeds, no ground truth verification

Output format:
```
WHY (root cause): 根本原因是充电桩运营商与聚合平台之间的数据同步延迟
（通常5–15分钟），加上运营商缺乏动力维护实时数据准确性（无SLA惩罚机制）。
EN root cause: Data sync lag (5-15 min) between charger operators and the aggregation
platform, compounded by operators having no SLA incentive to maintain data accuracy.
```

---

### HOW (如何 / 现有解法与满意度)
**Question**: How are users currently dealing with this pain? How satisfied are they?

Capture:
- **Current workarounds**: What do users do today to cope?
- **Alternative products/services**: Are they using competitors? Switching entirely?
- **Satisfaction level**: Are workarounds "good enough" or deeply frustrating?
- **Switching intent**: How many express intent to leave or have already left?
- **Unmet need signal**: The gap between workaround satisfaction and desired solution indicates market opportunity size

Output format:
```
HOW: 现有解法：用多个APP交叉验证（特来电+快电+小桔充电同时开），
     或加入微信群由群友实时播报空桩。满意度：极低，用户称之为"破解版充电"。
     流失信号：约30%帖子提及考虑换车或自装家用桩。
     EN: Workaround: running 3 apps simultaneously to cross-check availability,
     or joining WeChat groups with real-time human updates. Satisfaction: very low.
     Churn signal: ~30% of posts mention considering home charger installation.
```

---

## 5W1H Report Section Structure

The dedicated 5W1H section in the HTML report should have:

### Section Layout
```
[Section Header: 5W1H深析 / 5W1H Deep Analysis]

[Intro paragraph explaining the framework and how it was applied]

[Pain Point Selector: dropdown or tab to select which pain point to analyze]

For each selected pain point:
┌─────────────────────────────────────────────────────┐
│  Pain Point Name + Heat Score                        │
├──────────┬──────────────────────────────────────────┤
│  WHO     │  [content]                               │
│  WHAT    │  [content]                               │
│  WHEN    │  [content]                               │
│  WHERE   │  [content]                               │
│  WHY     │  [content — highlighted as root cause]  │
│  HOW     │  [content + satisfaction gauge]          │
└──────────┴──────────────────────────────────────────┘

[Representative user quote block]
[Opportunity implication → links to Section 6]
```

### Cross-Pain-Point Matrix View

Also include a summary matrix showing ALL pain points in a compact 5W1H table:

| Pain Point | WHO | WHAT | WHEN | WHERE | WHY | HOW |
|------------|-----|------|------|-------|-----|-----|
| Pain #1    | ... | ...  | ...  | ...   | ... | ... |
| Pain #2    | ... | ...  | ...  | ...   | ... | ... |

This matrix view is collapsible. It gives readers a quick cross-comparison.

---

## Analysis Tips

1. **WHY is the most valuable dimension** — invest the most time here. Surface-level analysis says "users complain about X"; deep analysis explains the systemic root cause that makes X inevitable without structural change.

2. **WHO informs prioritization** — a pain point affecting 10% of users who each pay 10x more is worth more than one affecting 80% of low-value users. Always connect WHO to economic value.

3. **WHEN reveals seasonality and urgency** — if a pain only happens during peak periods, the solution may be demand-shaping rather than capacity expansion.

4. **HOW reveals the opportunity size** — the worse and more expensive the current workaround, the more valuable a real solution is. If users are already paying for imperfect workarounds, they'll pay for a real fix.

5. **Cross-reference 5W1H across pain points** — often the same root cause (WHY) drives multiple pain points (WHAT). Solving the root cause addresses all symptoms simultaneously — this is a "10x opportunity."
