# Content Factory

> A Claude Code skill that builds a complete client-ready viral content strategy — paid AI ads + organic real-shot content — based on live trend research, and then executes it end to end.

The headline deliverable is a polished HTML **Client Strategy Brief** built around the formats actually winning feeds right now: street interviews, podcast clips, UGC challenges, talking-head reviews, unboxings, ASMR close-ups, founder POV, day-in-life vlogs.

After the client signs off, the same skill executes:

- Generates the AI ad videos via [Higgsfield](https://higgsfield.ai) Marketing Studio
- Produces detailed shot lists + scripts for real-shot formats (podcast clips, founder stories, vlogs)
- Renders the static image asset pack via GPT Image 2.0
- Schedules paid creatives to Meta Ads and exports an organic posting calendar
- Closes with a cost-savings report (Higgsfield credits + crew spend vs traditional agency pricing)

UX is **button-driven** — clicks, not typed commands. Internal mechanics (MCP tool names, UUIDs, slug mismatches) stay silent. The user sees stage banners and deliverables.

---

## What you get

| Stage | Deliverable |
|---|---|
| 1 | Viral trend research across TikTok / Instagram / YouTube — competitor scan + hook library |
| 2 | **Client Strategy Brief (HTML)** — the document you send to the client |
| 3 | AI video batch (Higgsfield) + real-shot production guide + image asset pack (GPT Image 2) |
| 4 | Paid scheduling on Meta Ads + organic posting calendar export |
| 5 | Cost-savings report — actual spend vs traditional industry midpoints |

Brief-only mode (stop after Stage 2) and image-pack-only mode are both supported.

---

## The 8 viral formats

Every campaign distributes evenly across these eight formats. Each one is flagged for production route:

| # | Format | Route | What it is |
|---|---|---|---|
| 1 | Street Interview | **AI** | Erewhon-style sidewalk interviews, "rate this out of 10," $100 challenges |
| 2 | Podcast Clip | **REAL** | 30–60s clip from a long-form founder podcast — chyron + waveform |
| 3 | Founder POV / Story | **REAL** | Founder talks straight to camera — origin, confession, contrarian PSA |
| 4 | Day-in-Life Vlog | **REAL** | Creator's day with the product naturally integrated |
| 5 | UGC Entertainment / Challenge | **AI** | Blind taste tests, dare-with-a-payoff, deadpan reactions |
| 6 | Talking-Head Product Review | **AI** | Honest review with product in hand, ingredient reveal |
| 7 | Unboxing | **AI** | Premium reveal — ribbon-pull, hangtag macro, trio reveals |
| 8 | ASMR Close-up | **AI** | Sound-led close-ups — cap unscrews, condensation, pours |

Default split: ~63% AI-generated · ~37% real-shot. The brief makes this split explicit to the client up front.

---

## Install

### Prerequisites

- [Claude Code](https://claude.com/claude-code) (CLI, Desktop app, or VS Code extension)
- For Stage 3 generation: the **Higgsfield** MCP server installed in Claude
- For Stage 4 scheduling: the **Meta Ads** MCP server installed in Claude

The skill gracefully degrades — Stages 1+2 (research + brief) work without any MCP integrations. Stage 3 needs Higgsfield. Stage 4 needs Meta Ads.

### Quick install (one command)

```bash
mkdir -p ~/.claude/skills && \
  git clone https://github.com/jbrazy480/content-factory.git ~/.claude/skills/content-factory
```

Restart Claude Code (or open a new chat). The skill auto-loads.

### Manual install

```bash
git clone https://github.com/jbrazy480/content-factory.git
ln -s "$(pwd)/content-factory" ~/.claude/skills/content-factory
```

To update later:

```bash
cd ~/.claude/skills/content-factory && git pull
```

See [INSTALL.md](INSTALL.md) for full details, including MCP server setup.

---

## How to use it

In any Claude Code session, drop a product image (or paste a product URL) and say something like:

- *"Build me a viral content strategy for this product."*
- *"Create a campaign for [client name]."*
- *"I need a content brief for a client."*

Or invoke directly:

```
/content-factory
```

The skill onboards in a single message (4 buttons + product attachment), then runs the pipeline.

### Standalone modes

- **Brief only** — picks Stage 2 in onboarding, exits after the HTML brief is saved.
- **Image pack only** — say "generate just the image pack" or "make the static visuals only." Skips Stages 1–2 and the video batches.

---

## What's in the box

```
content-factory/
├── SKILL.md          The skill itself (Claude Code reads this)
├── README.md         This file
├── INSTALL.md        Install instructions + MCP server setup
├── LICENSE           MIT
└── examples/         Sample outputs from real campaigns (coming soon)
```

---

## Philosophy

**Research-first.** Every campaign starts with eight live web searches across TikTok / Instagram / YouTube / Meta Ad Library / podcast clips. The brief cites specific trends and competitor examples — never generic best practices.

**Client-grade output.** The Stage 2 HTML brief is built to send to a paying client. Premium typography, brand-derived hero color, mobile responsive, print-friendly. Not a wireframe.

**AI + real-shot, not AI-only.** The formats that dominate right now mix both. Podcast clips, founder POV, vlogs — these need real humans on camera. The skill writes the shot lists for those instead of trying to fake them in AI.

**Silent mechanics.** Tool names, UUIDs, slug mismatches, and avatar resolution stay invisible. The user sees stage banners and deliverables, not a tool log.

**Button-driven UX.** Every confirmation is 2–4 buttons. The only typed input is the product image / URL paste.

---

## Built by

[MetaTech AI](https://metatech.ai) / [EveryThingAI](https://evrythingai.com) — high-production advertising and AI-powered lead follow-up automation for service businesses.

Companion product: [RizzDial](https://rizzdial.com), the AI dialer.

---

## License

[MIT](LICENSE) — use it, fork it, ship it, sell strategy briefs with it.

If you build something cool on top of this skill, send it our way.
