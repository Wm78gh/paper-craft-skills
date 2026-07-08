# paper-craft-skills

English | [中文](./README.zh.md)

**6 AI-powered skills for academic papers: method figures, deep articles, slide decks, surveys, posters, and summaries — zero config, one command.**

<p align="center">
  <img src="examples/paper-illustrated/attention-is-all-you-need/transformer-overview-paper-figure.png" width="700" alt="Transformer architecture — generated from Attention Is All You Need"/>
</p>

<p align="center">
  From arxiv link to publication-ready visuals, AIGC slide decks, deep articles, comparison surveys, conference posters, and visual summaries.<br/>
  Drop a paper, pick a style, get output that looks like a human expert made it.
</p>

---

## How to install

**Copy this into Codex or Claude Code:**

```
Please install zsyggg/paper-craft-skills for me.
GitHub: https://github.com/zsyggg/paper-craft-skills
```

That's it. The agent handles clone, symlink, and registration. **No API keys. No accounts.** If you prefer a terminal:

```bash
npx skills add zsyggg/paper-craft-skills
```

**Works with:** Codex · Claude Code · Cursor · Windsurf

---

## What's inside

### 🎨 paper-comic — Paper → Method Figures

Reads your paper → proposes what to draw → you confirm → generates.

| Style | Vibe |
|-------|------|
| **paper-figure** | Publication-grade diagrams |
| **sketchnote** | Bright, warm hand-drawn study notes |

```bash
/paper-comic https://arxiv.org/abs/1706.03762 --style sketchnote
```

### 📄 paper-analyzer — Paper → Deep Articles

Reads the full paper → searches GitHub for open-source code → writes in your chosen style.

| Style | Output |
|-------|--------|
| **storytelling** | Viral blog post style, hooks + analogies + golden takeaway |
| **academic** | Peer-reviewed deep dive, KaTeX formulas, comparison tables |
| **concise** | Cheat sheet, Mermaid diagram + key data table |

Features: KaTeX formulas · Mermaid diagrams · Code cross-reference · Dark mode 🌙

```bash
/paper-analyzer https://arxiv.org/abs/1706.03762 --style academic
```

### 🖼️ paper-deck — Paper → Visual Slide Deck

Plans the deck → generates 16:9 AIGC slide images → exports PPTX/PDF.

| Style | Best for |
|-------|----------|
| **journal-minimal** | Nature/IEEE academic decks, thesis defenses |
| **business-research** | Strategy memos, investor/client briefings |
| **warm-notes** | Teaching, study-note explanations |
| **liquid-glass** | Apple-inspired visual chapters, covers |

```bash
/paper-deck https://arxiv.org/abs/1706.03762 --style journal-minimal --slides 12
```

### 🔬 paper-survey — Multi-Paper → Comparison Survey ✨ NEW

Reads multiple papers → builds structured comparison matrix → generates.

| Mode | Output |
|------|--------|
| **comparison-figures** | AIGC comparison diagrams |
| **survey-deck** | Comparison slides (PPTX/PDF) |
| **survey-article** | Deep comparison HTML article |

Each paper gets a consistent color across all output. Differences are visually highlighted.

```bash
/paper-survey https://arxiv.org/abs/1706.03762 https://arxiv.org/abs/1907.04340
/paper-survey --topic "Position encoding comparison" --papers p1.pdf p2.pdf
```

### 📋 paper-poster — Paper → Conference Poster ✨ NEW

Automatically extracts core content → generates high-res AIGC poster → produces print-ready PDF.

| Style | Size | Use |
|-------|------|-----|
| **conference-wide** | 48×36 in (4:3) | Standard conference poster |
| **defense-poster** | 36×48 in (3:4) | Thesis defense |
| **research-showcase** | 48×36 in (4:3) | Open house, demos |

```bash
/paper-poster https://arxiv.org/abs/1706.03762 --style conference-wide
```

### 📊 paper-summary — Paper → One-Page Visual Summary ✨ NEW

Distills a paper into a single AIGC visual — perfect for sharing.

| Mode | Format | Use |
|------|--------|-----|
| **infographic** | Vertical 2:3 | Social media, WeChat, Twitter |
| **card-summary** | Square 1:1 | Reference managers, Notion |
| **timeline-figure** | Horizontal 16:9 | README, slide insertion |

```bash
/paper-summary https://arxiv.org/abs/1706.03762 --mode infographic --language Chinese
```

---

## Unified CLI

All 6 skills available through a single command:

```bash
python3 scripts/papercraft.py list
python3 scripts/papercraft.py help deck
python3 scripts/papercraft.py comic https://arxiv.org/abs/1706.03762 --style sketchnote
python3 scripts/papercraft.py survey p1.pdf p2.pdf --format survey-article
python3 scripts/papercraft.py poster paper.pdf --style defense-poster
python3 scripts/papercraft.py summary paper.pdf --mode card-summary
```

---

## paper-deck — Visual slide decks that don't look like templates

`paper-deck` turns a paper, article, or technical note into a designed slide deck. It first builds a deck brief and slide-by-slide outline, then writes reproducible visual prompts, generates polished 16:9 slide images, and merges them into `.pptx` and `.pdf`.

It is built for iteration: every page has its own prompt, so you can ask for precise changes like "make slide 5 more journal-like", "replace slide 8 with a real benchmark chart", or "keep the layout but switch the cover to liquid glass".

<p align="center">
  <img src="images/paper_deck_styles.png" width="640"/>
  <br/><sub>Four compact style presets for the same paper topic</sub>
</p>

It also supports real source visuals. When a PDF contains strong figures, tables, plots, or screenshots, the skill plans which slides should use them, where they should be cropped, and how they should be framed.

---

## paper-comic — How it works

```text
/paper-comic https://arxiv.org/abs/1706.03762

Reads the paper, then recommends:

  I suggest 6 figures:
  1. Cover: one-line contribution + visual anchor
  2. Transformer architecture overview
  3. Self-attention mechanism
  4. Multi-head attention detail
  5. Encoder / Decoder Block
  6. Key results

  Or generate only 1 overview figure, or expand to 8 detailed mechanism figures.
  Language? [Chinese / English]  Style? [sketchnote / paper-figure]  Scope and count?
```

### Example outputs

<p align="center">
  <img src="examples/paper-illustrated/attention-is-all-you-need/transformer-overview-paper-figure.png" width="550"/>
  <br/><b>paper-figure</b> — clean, publication-grade
</p>

<p align="center">
  <img src="examples/paper-illustrated/attention-is-all-you-need/self-attention-sketchnote.png" width="350"/>
  <br/><b>sketchnote</b> — bright, warm, approachable
</p>

> Full walkthrough: [examples/paper-illustrated/attention-is-all-you-need](./examples/paper-illustrated/attention-is-all-you-need)

---

## paper-analyzer — Deep articles that read like a human expert wrote them

**Not a paper translator — a re-interpreter.** It reads the full paper, searches GitHub for open-source implementations, cross-references code with the paper, and writes in your chosen style.

### Three writing styles

<p align="center">
  <img src="images/styles_comparison.png" width="700"/>
</p>

| Style | Reads like | Use it for |
|-------|-----------|------------|
| **storytelling** | A viral blog post — hooks, analogies, golden takeaway | WeChat, Twitter, blogs |
| **academic** | A peer-reviewed deep dive — KaTeX formulas, comparison tables | Lab meetings, lit reviews |
| **concise** | A cheat sheet — Mermaid diagram + key data table | Quick understanding |

### Dark Mode Support 🌙

Every paper-analyzer HTML article now supports dark mode — automatically follows system preference, with a manual toggle button.

---

## paper-survey — Compare multiple papers, visually

`paper-survey` extends the same approach to **multiple papers**. It reads each paper independently, builds a structured comparison matrix across 5 dimensions (problem definition, method approach, key design, experimental results, trade-offs), and generates:

| Mode | Output | Use case |
|------|--------|----------|
| **comparison-figures** | AIGC comparison diagrams (PNG) | Quick team overview, tech selection |
| **survey-deck** | 16:9 comparison slides (PPTX/PDF) | Group meeting survey presentations |
| **survey-article** | Deep comparison HTML article | Literature review writing |

```bash
/paper-survey https://arxiv.org/abs/1706.03762 https://arxiv.org/abs/1907.04340
/paper-survey --topic "Transformer position encoding" --papers p1.pdf p2.pdf p3.pdf
```

---

## paper-poster — From paper to conference poster

`paper-poster` extracts core content from a paper and generates a complete AIGC conference poster at 300dpi print resolution. Three layout presets match different scenarios, and the script handles upscaling and PDF export automatically.

```bash
/paper-poster https://arxiv.org/abs/1706.03762 --style conference-wide
/paper-poster paper.pdf --style defense-poster
```

---

## paper-summary — One page, everything clear

`paper-summary` distills an entire paper into a single AIGC visual. Three modes for different sharing scenarios — infographic for social media, card for reference managers, timeline for README insertion.

```bash
/paper-summary https://arxiv.org/abs/1706.03762 --mode infographic --language Chinese
/paper-summary paper.pdf --mode card-summary
```

---

## Requirements

```bash
pip install Pillow python-pptx
```

Optional: `pip install markdown pypdf2` for paper-analyzer HTML generation.

---

## License

MIT

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=zsyggg/paper-craft-skills&type=Date)](https://star-history.com/#zsyggg/paper-craft-skills&Date)
