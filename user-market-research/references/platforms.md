# Platform Reference: Data Sources & Search Strategies

## Chinese Social Platforms

### 小红书 (Xiaohongshu / RED)
- **Type**: Lifestyle social media — extremely high signal for real user experience
- **Search URL pattern**: `https://www.xiaohongshu.com/search_result/?keyword={keyword}`
- **Sort options**: 最新 (latest), 热门 (popular)
- **Access**: Requires login; often EGRESS_BLOCKED
- **Fallback**: Search `site:xiaohongshu.com {keyword}` via WebSearch; use snippet data
- **Best for**: Consumer product complaints, lifestyle pain points, Gen Z/Millennial feedback

### 微博 (Weibo)
- **Type**: Twitter-equivalent microblogging
- **Search URL**: `https://s.weibo.com/weibo?q={keyword}&typeall=1&suball=1&timescope=custom`
- **Access**: Often accessible; some content requires login
- **Fallback**: Search `site:weibo.com {keyword}` or `微博 {keyword}` via WebSearch
- **Best for**: Breaking complaints, trending social issues, emotional reactions

### 知乎 (Zhihu)
- **Type**: Q&A platform (China's Quora)
- **Search URL**: `https://www.zhihu.com/search?type=content&q={keyword}`
- **Access**: Partially accessible; often EGRESS_BLOCKED on direct fetch
- **Fallback**: Search `site:zhihu.com {keyword}` or `知乎 {keyword}` via WebSearch
- **Best for**: In-depth user analysis, technical questions, comparative discussions

### 抖音 / TikTok (Douyin)
- **Type**: Short video platform
- **Access**: No public API; login required
- **Fallback**: Search `抖音 {keyword} 评论 用户反馈` via WebSearch; look for news articles analyzing Douyin trends
- **Best for**: Younger demographics (18–30), viral complaint trends

### B站 (Bilibili)
- **Type**: Video + comment platform (anime/gaming-skewed but broadening)
- **Search URL**: `https://search.bilibili.com/all?keyword={keyword}`
- **Access**: Partially accessible
- **Fallback**: Search `site:bilibili.com {keyword}` via WebSearch
- **Best for**: Tech-savvy users, detailed tutorial feedback, long-form user experience sharing

---

## International Social Platforms

### X (Twitter)
- **Type**: Real-time microblogging
- **Search URL**: `https://x.com/search?q={keyword}&f=live`
- **Access**: Login wall; often EGRESS_BLOCKED
- **Fallback**: Search `site:x.com {keyword}` or `twitter {keyword} user complaint` via WebSearch
- **Best for**: Real-time sentiment, global user voices, English-language feedback
- **Note**: Use `mcp__Claude_in_Chrome__*` tools if available and user is logged in

### Reddit
- **Type**: Forum/discussion community
- **Search URL**: `https://www.reddit.com/search/?q={keyword}&sort=relevance`
- **Recommended subreddits**: Search `reddit.com/r/{relevant_subreddit}`
- **Access**: Generally accessible; JSON API available at `reddit.com/search.json?q={keyword}`
- **API fallback**: `https://www.reddit.com/search.json?q={keyword}&sort=new&limit=50`
- **Best for**: English-language deep discussions, candid user feedback, niche communities
- **Note**: Reddit is often the most accessible English source — prioritize it

### Instagram
- **Type**: Photo/video social platform
- **Access**: Login required; EGRESS_BLOCKED for most fetches
- **Fallback**: Search `site:instagram.com {keyword}` or search for news articles about Instagram trends
- **Note**: Low value for text-based pain points; mainly useful for visual product feedback

### YouTube
- **Type**: Video platform with rich comment sections
- **Search URL**: `https://www.youtube.com/results?search_query={keyword}`
- **Access**: Search results often accessible; comment data requires API or Chrome MCP
- **Fallback**: Search `youtube {keyword} review complaints users` via WebSearch for video summaries
- **Best for**: In-depth product reviews, tutorial frustration, "why I stopped using X" content
- **Note**: Use `mcp__Claude_in_Chrome__*` to read comment sections if available

---

## Complaint & Review Platforms

### 黑猫投诉 (Heimao)
- **URL**: `https://tousu.sina.com.cn/`
- **Search**: `https://tousu.sina.com.cn/?keyword={keyword}`
- **Access**: Often EGRESS_BLOCKED
- **Fallback**: Search `黑猫投诉 {keyword}` via WebSearch — news coverage is usually rich
- **Best for**: Formal consumer complaints, quantified complaint volumes

### 消费者协会 / 中消协
- **URL**: `https://www.cca.org.cn/`
- **Best for**: Official complaint statistics, 315 annual reports
- **Strategy**: Search `中消协 {keyword} 2025` or `315投诉 {keyword}` via WebSearch

### 聚投诉
- **URL**: `https://www.ju.taobao.com/` (Taobao complaints)
- **Fallback**: Search `聚投诉 {keyword}` via WebSearch

---

## Industry Reports & Data Sources

### CNNIC (中国互联网络信息中心)
- **URL**: `https://www.cnnic.net.cn/`
- **Best for**: Official Chinese internet statistics, user behavior data
- **Strategy**: Search `CNNIC {year} 互联网发展状况统计报告` — PDFs often accessible

### 艾媒咨询 (iiMedia)
- **URL**: `https://www.iimedia.cn/`
- **Access**: Often EGRESS_BLOCKED
- **Fallback**: Search `艾媒咨询 {keyword} {year}` via WebSearch for report summaries in news

### QuestMobile
- **Best for**: Mobile app usage data, demographic breakdowns
- **Strategy**: Search `QuestMobile {keyword} {year}` for published data snippets

### Stanford AI Index
- **URL**: `https://aiindex.stanford.edu/`
- **Access**: Generally accessible
- **Best for**: AI adoption data, global comparisons

### 前程无忧 / Boss直聘 / 脉脉
- **Best for**: Workplace AI usage, job market trends, professional user feedback
- **Strategy**: Search news coverage of their annual reports

---

## Fallback Strategy When Platforms Are Blocked

When direct access fails, use this waterfall approach:

1. **WebSearch for site-specific content**: `site:{platform}.com {keyword}`
2. **News aggregation**: Search `{keyword} 用户反馈 投诉 2025` — journalism often quotes real user voices
3. **Report snippets**: Search `{keyword} 调研报告 2024 2025` for published survey data
4. **Academic/think tank**: Search for university or NGO studies on the topic
5. **Competitor analysis**: If platform A is blocked, search what users say about competitors — the pain points often transfer

Always note in the report which sources were directly accessed vs. accessed via fallback methods.
