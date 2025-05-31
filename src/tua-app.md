---
title: Collection of Underground App Distribution URLs on Telegram
separator: <!--s-->
verticalSeparator: <!--v-->
theme: simple
highlightTheme: github
css: custom.css
revealOptions:
  transition: 'slide'
  transitionSpeed: fast
  center: false
  slideNumber: "c/t"
  width: 1000
---

<style>
:root {
  --r-main-font: "Times New Roman", "LXGW WenKai Screen", sans-serif;
  --r-heading-font: "JetBrains Mono", "LXGW WenKai Screen", sans-serif;
  --r-code-font: "Times New Roman", "LXGW WenKai Screen", sans-serif;
}
</style>

<!-- .slide: data-background="tua-app/cover.png" -->


<!--v-->
<!-- .slide: data-background="tua-app/background.png" -->

<h2 style="color: #337ab7;">Content</h2>

- Introduction
- Background
- Methodology
- Data Overview
- Conclusion
- References

<!--v-->
<!-- .slide: data-background="tua-app/background.png" -->

<h2 style="color: #337ab7;">Introduction</h2>

**Telegram**, due to its end-to-end encryption, anonymous user identity, and weak content moderation, has increasingly become a distribution platform for **underground mobile applications**.
These apps are often banned or restricted on mainstream app stores and include:

<div class = 'mul-cols'>
  <div class = 'col'>
    <ul>
            <li>Pornographic content</li>
            <li>Gambling platforms</li>
            <li>Pirated software</li>
            <li>Apps involved in fraud, phishing, and privacy violations</li>
        </ul>
  </div>
  <div class = 'col'>
    <img src="tua-app/tg-intro.png" style="width: 80%">
  </div>
  <div class = 'col'>
    <img src="tua-app/tg-woman.png" style="width: 90%">
  </div>
  </div>
</div>

In this project, we aim to systematically collect, extract, and identify Telegram URLs associated with underground app distribution through multi-stage automation, providing a foundation for further analysis.

<!--s-->
<!-- .slide: data-background="tua-app/background.png" -->

<h2 style="color: #337ab7;">Background</h2>

- Underground apps often hide behind:
  - Search bots that **promote links via keywords**
  - Forwarded messages across **interlinked channels**
- Prior study [Guo et al., ACM IMC 2024]:
  - Used 300+ keywords and multiple bots
  - Retrieved 70k+ potential channels
- Our task replicates and engineers this discovery pipeline.

<!--s-->
<!-- .slide: data-background="tua-app/background.png" -->

<h2 style="color: #337ab7;">Methodology</h2>

**Step 1: Collect Bots and Keywords**

- Collected top 15 Telegram bots (e.g. `@hao1234bot`)  
- Compiled 300 keywords in **Chinese and English**  
  > e.g., "VPN", "91", "Crack", "Young girl", "暗网"


- For each bot:
  - Automatically join chat
  - Randomly send 2-3 keywords
  - Parse returned message(s) for t.me/channel links

<!--v-->
<!-- .slide: data-background="tua-app/background.png" -->

**Step2

- Some bots return raw text with embedded links.
- Used regex-based extraction instead of entity objects:
```python
re.findall(r'https?://t\.me/\w+', message.message)
```

<!--v-->

<h3 style="color: #337ab7;">Step 3: Export to `url.csv`</h3>

- Collected (URL, Source Bot ID)
- Output format:
```csv
url,channel_id
https://t.me/example1,12345678
https://t.me/example2,87654321
```

<!--s-->
<!-- .slide: data-background="tua-app/background.png" -->

<h2 style="color: #337ab7;">Data Overview</h2>

| Item              | Count     |
|-------------------|-----------|
| Bots Collected    | 15        |
| Keywords Used     | 300       |
| Keyword/Bot Queries | 500+    |
| Channels Identified | ~2000   |
| Valid URLs Extracted | 1400+  |
| Output Format     | `.csv`    |


<!--s-->
<!-- .slide: data-background="tua-app/background.png" -->

<h2 style="color: #337ab7;">Conclusion</h2>

- We implemented a **semi-automated crawler** to interact with Telegram search bots.
- Successfully extracted **1400+ URLs** pointing to potentially underground app promotion channels.
- This list is the foundation for:
  - Historical message crawling (Stage 2)
  - App promotion link identification (Stage 3)

> 🔜 Next: Crawl messages & detect promotion patterns.


<!--v-->
<!-- .slide: data-background="tua-app/background.png" -->

<h2 style="color: #337ab7;">Challenges Encountered</h2>

- ❗ Some bots do not return links but plain text
- ❗ Flooding too many messages leads to muted accounts
- ❗ Channel links are ephemeral — many were **deleted within 24h**
- ✅ Solved with:
  - Regex fallback parsing
  - `asyncio.sleep()` between queries
  - Repeated crawling rounds


<!--s-->
<!-- .slide: data-background="tua-app/end.png" -->
