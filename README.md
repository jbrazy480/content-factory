# Content Factory

> A Claude Code skill that turns an offer + a product image into a complete client-ready viral content strategy — and then executes it end to end. AI ads, real human-shot content, or both. Lead-gen first.

The headline deliverable is a polished HTML **Client Strategy Brief** built around the formats actually winning feeds right now: street interviews, podcast clips, UGC challenges, talking-head reviews, unboxings, ASMR close-ups, founder POV, day-in-life vlogs.

Where most "AI ad builder" skills generate generic videos from a product photo, Content Factory starts with a **Phase 0 discovery conversation** — what you sell, who buys, what action you want them to take — and biases every downstream decision toward lead gen since most clients are running lead campaigns, not ecommerce purchases.

After the client signs off, the same skill executes:

- Generates the AI ad videos via [Higgsfield](https://higgsfield.ai) Marketing Studio
- Produces detailed shot lists + scripts for real-shot formats (podcast clips, founder stories, vlogs)
- Renders the static image asset pack via GPT Image 2.0
- Schedules paid creatives to Meta Ads and exports an organic posting calendar
- Closes with a cost-savings report (Higgsfield credits + crew spend vs traditional agency pricing)

UX is **button-driven** — clicks, not typed commands. Internal mechanics (MCP tool names, UUIDs, slug mismatches) stay silent. The user sees stage banners and deliverables.

---

## What's new in v1.1

- **Phase 0 — Offer / Audience / CTA discovery.** A 4-question conversation before research even starts, so every hook is anchored to a specific offer transformation, not a generic template.
- **Track choice.** Pick AI ads only (Higgsfield required), real human-shot only (zero AI generation — useful when you have a creator team), or Both (the default).
- **Built-in Higgsfield walkthrough.** If you're not connected yet, the skill walks you through account creation, plan selection, MCP connection, and access verification — under 5 minutes.
- **Real competitor research.** Stage 1 now does a structured competitor scan (5–10 brands, format mix, posting cadence, the gap to own) instead of just aggregating trend searches.
- **Hook Library workshop.** 30+ hooks generated before any production — split across Curiosity, Pattern Interrupt, Pain-Named, Cost/Receipt, **Funny / Podcast-Style** (the format dominating right now), and Founder Confession categories.
- **CTA Library workshop.** 8 CTAs matched to your Phase 0 action choice. Form fills, booked calls, free trials, ecommerce, DMs — each with friction-reducer scripts.
- **Lead-gen primary mode.** Default Meta Ads objective auto-sets to Leads. Format mix biases toward conversion-driving formats (Talking-Head Review, Founder POV, Street Interview). Qualifier defaults baked in.

---

## What you get

| Stage | Deliverable |
|---|---|
| 0 | Offer + ICP + CTA profile — the foundation everything else builds on |
| 1 | Viral trend research + competitor scan + Hook Library (30+ hooks) + CTA Library (8 scripted closers) |
| 2 | **Client Strategy Brief (HTML)** — the document you send to the client |
| 3 | AI video batch (Higgsfield) + real-shot production guide + image asset pack (GPT Image 2) |
| 4 | Paid scheduling on Meta Ads + organic posting calendar export |
| 5 | Cost-savings report — actual spend vs traditional industry midpoints |

Brief-only mode (stop after Stage 2), image-pack-only mode, and real-shot-only mode are all supported.

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
