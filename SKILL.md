---
name: content-factory
description: >
  Build a complete client-ready viral content strategy — paid AI ads + organic — based on
  live trend research across TikTok, Instagram, YouTube. The headline deliverable is a
  polished HTML Content Strategy Brief built around the viral formats that are actually
  winning right now (street interviews, podcast clips, UGC challenges, talking-head
  reviews, unboxings, ASMR, founder POV, day-in-life vlogs). After client approval, the
  same skill executes: generating AI ad videos via Higgsfield Marketing Studio for
  AI-renderable formats, producing detailed shot lists + scripts for real-shot formats
  (podcast clips, founder stories), generating the image asset pack via GPT Image 2, and
  scheduling to Meta Ads + an organic calendar. Closes with a cost-savings report.
  Button-driven UX — clicks, no typed commands. Trigger on a product image + content
  request, or phrases like 'content strategy', 'viral content plan', 'content brief for a
  client', 'build a content factory', 'create a campaign', 'content for [client]'.
---

# Content Factory

A 5-stage pipeline: **Research → Brief → Produce → Publish → Report.**

**The headline deliverable is the Client Strategy Brief — a polished HTML document built
on live viral research, mapped across the formats dominating feeds right now.** Everything
downstream (AI-generated videos, real-shot scripts, asset pack, paid + organic schedule,
cost report) is the execution layer. The brief is what the client signs off on.

**Coverage:** paid AI ads (rendered in Higgsfield Marketing Studio) AND organic content
(shot lists + scripts the client's team or a creator films in real life). Most viral
content right now blends both — interview + podcast formats need real humans on camera;
challenges, reviews, and ASMR can be AI-rendered. The brief tells the client exactly
what's getting produced where.

**UX is button-driven.** Every clarifying question MUST be asked via AskUserQuestion with
2–4 concrete option buttons. Never ask a free-form "type your answer" question for
navigation, confirmation, or routing. Free-form typing is reserved ONLY for content the
user must originate (product image / URL / variant names), and even then offer a smart
default they can accept with one click.

**User-facing language rule (HARD).** Do NOT narrate technical mechanics — no MCP tool
names, no slug-mismatch tables, no UUID resolutions, no "running parallel searches", no
"calling media_upload + curl + media_confirm", no enhanced-prompt internals. All of that
runs silently behind the scenes. Send ONE clear stage banner each time a stage starts:

| Stage | Banner |
|---|---|
| 1 | **🔍 Stage 1: Viral research — starting now.** I'm scanning what's actually winning this week in your product's niche across TikTok, Instagram, and YouTube. |
| 2 | **🗂️ Stage 2: Client Strategy Brief — starting now.** I'm building the polished HTML brief you'll send to the client — every format, hook, calendar slot, and production route mapped. |
| 3 | **🎬 Stage 3: Production — starting now.** I'm producing your AI ad videos in Higgsfield and packaging shot lists for the real-shot formats. |
| 3 (image step) | **🖼️ Image asset pack — starting now.** I'm generating social posts, hero banners, and product stills via GPT Image 2. |
| 4 | **📅 Stage 4: Scheduling — starting now.** I'm wiring your paid campaigns into Meta Ads and exporting the organic posting calendar. |
| 5 | **💰 Stage 5: Cost report — starting now.** I'm compiling the savings report — what you actually spent versus what this volume would cost the traditional way. |

Between stages send a brief "Stage [N] done — [deliverable]" line, then the next banner.

**Internal mechanics — keep silent.** "Probe capability," "resolve hook_id at runtime,"
"set `mode` to title-case slug," "8 mandatory searches in parallel," "media_upload → curl
PUT → media_confirm," "slug mismatch fix" — execute silently; never narrate. If the user
asks "how does it work under the hood," explain. Otherwise stay silent.

---

## ONBOARDING — single-shot, no pauses

Send ALL onboarding questions in ONE AskUserQuestion call. Never sequence.

**Step A — Higgsfield MCP connection** (button)
"Yes — connected" · "Not yet — I'll connect now" · "Skip — brief only (no video generation)"

**Step B — Starting stage** (button)
- "Stage 1 — Full pipeline (Recommended — needs product image)"
- "Stage 2 — Build the brief only (skip production)"
- "Stage 3 — Produce now (I have a brief)"
- "Stage 4 — Schedule (content is ready)"

**Step C — Campaign volume** (button + Other)
"50 videos" · "100 videos (Recommended)" · "150 videos" · "200 videos" · Other → any number.

Store as `[VIDEO_COUNT]`. Image pack count = `floor(VIDEO_COUNT / 5)`.

The split across the 8 viral formats (defined below) is `floor(VIDEO_COUNT / 8)` per
format, with the remainder distributed starting from format 1. **Do not show the split to
the user at this step** — it surfaces naturally inside the Stage 2 brief as a consequence
of what the research showed, not as a config card.

**Step D — Product / brief input** (file attach prompt in the same message)
"Attach the product image to this message OR drop a URL — that's all I need to start."

If a product image is already attached, skip D.
If user picked Stage 3+ in Step B, swap D with: "Drop your approved brief or paste it here."

**Single-message rule:** A/B/C buttons + D prompt go out in ONE message. User clicks, attaches
the product, and the pipeline starts.

---

## THE 8 VIRAL FORMATS — the campaign mix

Every Content Factory campaign distributes evenly across these 8 formats. They are the
formats actually dominating feeds across every consumer niche right now. Each format
includes a **production route** flag — `AI` (renderable in Higgsfield Marketing Studio)
or `REAL` (requires real-shot footage; the skill delivers a shot list + script instead).

| # | Format | Production route | What it is | Why it wins |
|---|---|---|---|---|
| 1 | **Street Interview** | AI (Higgsfield UGC + Interview hook) | Erewhon-style sidewalk interviews, "rate this out of 10," "sing for the product," "$100 challenge" | High-trust feel, "real people" energy, novelty hook |
| 2 | **Podcast Clip** | **REAL** | 30–60s extracted clip from a long-form founder podcast — bold claim, soundbite, talking-head with chyron + waveform | Authority signal, founder-built credibility, replayable |
| 3 | **Founder POV / Story** | **REAL** (some AI variants) | Founder talks straight to camera — origin story, "why I built this," confession-style hook | Direct, founder-led trust; works best in the founder's own voice |
| 4 | **Day-in-Life Vlog** | **REAL** | Creator's day with the product naturally integrated — morning routine, gym, café, work-from-home | Native to feed, doesn't read as an ad |
| 5 | **UGC Entertainment / Challenge** | AI (Higgsfield UGC) | Blind taste tests, "do it for $100" challenges, dare-with-a-payoff, deadpan reaction | Pattern-interrupt, save-worthy, share-driven |
| 6 | **Talking-Head Product Review** | AI (Higgsfield Product Review) | Honest review with product in hand — ingredient reveal, side-by-side, "I tried this for X days" | Conversion-driving; the format buyers research |
| 7 | **Unboxing** | AI (Higgsfield Unboxing) | Premium reveal — ribbon-pull, paper rustle, hangtag macro, trio reveal | Save / send-to-friend rate is highest on this format |
| 8 | **ASMR Close-up** | AI (Higgsfield UGC + audio on) | Sound-led close-ups — cap unscrewing, condensation slide, pour into glass, no music | Save-driver, watch-through completion, calming feed moment |

**Distribution rule:** `per_format = floor(VIDEO_COUNT / 8)` with remainder starting at
format 1. Worked examples below.

| Total | Street Int. | Podcast | Founder POV | Vlog | Challenge | Review | Unbox | ASMR |
|---|---|---|---|---|---|---|---|---|
| **50** | 7 | 7 | 6 | 6 | 6 | 6 | 6 | 6 |
| **100** | 13 | 13 | 13 | 13 | 12 | 12 | 12 | 12 |
| **150** | 19 | 19 | 19 | 19 | 19 | 19 | 18 | 18 |
| **200** | 25 | 25 | 25 | 25 | 25 | 25 | 25 | 25 |

**AI vs REAL split** (by default): 5 of 8 formats are AI-renderable (Street Int., Challenge,
Review, Unbox, ASMR). 3 are real-shot (Podcast, Founder POV, Vlog). So roughly **5/8 (≈63%)
of the campaign volume gets AI-generated** and **3/8 (≈37%) is delivered as shot lists +
scripts** for the client to film. The brief makes this split visible to the client up front.

**Format definitions in detail** are in the appendix below. The skill picks varied
**concept seeds** within each format so no two videos in the same format are identical.

---

## MARKETING STUDIO CAPABILITY GROUND TRUTH

Always honor these constraints. Query Higgsfield for live values in Stage 1 Step 0.

### Hard limits
- **Duration:** 4–15s per single clip. Longer narrative → multi-clip sequence (1/2, 2/2).
- **Aspect ratios:** auto · 21:9 · 16:9 · 4:3 · 1:1 · 3:4 · 9:16
- **Resolution:** 480p · 720p · 1080p
- **Audio:** optional via `generate_audio` — true for ASMR.
- **Reference media:** product image always; avatar image (UGC family).

### Marketing Studio presets (reference snapshot)

| Preset (slug) | Built for | Picklist hook + setting? |
|---|---|---|
| `ugc` | Realistic person + product, social-media native | ✅ |
| `tutorial` | Step-by-step how-to / recipe | ✅ |
| `ugc_unboxing` | Box reveal, premium unbox | ✅ |
| `hyper_motion` | Kinetic product hero shots (splash, pour, spin) | ❌ |
| `product_review` | Talking-head honest review | ✅ |
| `tv_spot` | Cinematic narrative spots | ❌ |
| `wild_card` | Surreal one-shot creative | ❌ |
| `ugc_virtual_try_on` | Casual try-on (apparel, eyewear) | ✅ |
| `virtual_try_on` | Premium studio try-on | ✅ |

**Mapping the 8 Content Factory formats to Marketing Studio presets:**

| Content Factory format | Higgsfield preset | Mode value |
|---|---|---|
| Street Interview | `ugc` + `Interview` hook + `Street` setting | `"UGC"` |
| UGC Challenge | `ugc` + Product Hit / Product Crash / Epic Fail hook | `"UGC"` |
| Talking-Head Review | `product_review` | `"Product Review"` |
| Unboxing | `ugc_unboxing` | `"Unboxing"` |
| ASMR | `ugc` + audio on + Kitchen/Bathroom/Bedroom setting | `"UGC"` |

The real-shot formats (Podcast Clip / Founder POV / Day-in-Life) don't route to a preset —
they're produced via shot list, not API call.

### What Marketing Studio CANNOT do

- ❌ Single clips longer than 15s
- ❌ Reliable lip-synced dialogue from non-human characters
- ❌ Multi-character coordinated dialogue with consistent identities across cuts
- ❌ Single output with multiple settings / split-screen
- ❌ Free-form `hook_id` or `setting_id` outside the picklist
- ❌ Consistent multi-scene podcast clip with the same host across 5 different setups

**This is why Podcast Clip / Founder POV / Day-in-Life are flagged REAL.** Don't try to
fake them in Marketing Studio — quality drops and identity drifts.

### Escape hatch (rare)

If an idea genuinely needs lip-sync or longer narrative AND the user wants AI generation
for it, route to: **Wan 2.7** (sync audio + identity), **Veo 3.1** (cinematic), **Cinema
Studio Video 3.0**, **Seedance 2.0** (reference-driven multi-SKU), or **Kling 3.0**. Use
sparingly. Default = real-shot delivery for the REAL formats.

---

## STAGE 1 — Viral Research

**Banner:** 🔍 Stage 1: Viral research — starting now. (See banner table.)

### Step 0 — Probe Marketing Studio *(internal — silent)*

1. `show_marketing_studio(action='presets')`
2. `show_marketing_studio(action='list', type='hook', size=100)`
3. `show_marketing_studio(action='list', type='setting', size=100)`
4. `show_marketing_studio(action='list', type='avatar', size=100)`

Cache hook + setting UUIDs and preset avatars. Pass straight to Stage 3 calls.

### Step 1 — Auto-detect product & niche *(silent — DO NOT ask the user)*

From the product image: category, variants, packaging style, color palette, demographic
cues. From the URL (if provided): `web_fetch` for product name, brand voice, claims.

- **Niche keyword:** category in plain English ("cold-pressed coffee," "running shoes")
- **Target market:** default Global / English-speaking unless packaging signals a region
- **Primary goal:** default Mixed (awareness + conversion) unless user stated otherwise

Send ONE status line — NOT a question. Frame as a marketer's read on the trend, not a
config card. Do NOT enumerate the 8 formats here.

> "Got it — looks like a [niche descriptor] with [variants]. I'll target a [market]
> audience and lean into what's actually moving in this category right now — street-level
> interview content, podcast-style clipped soundbites, founder-led POV, day-in-life
> creator vlogs, challenge clips, honest reviews, premium unboxings, and audio-first ASMR
> close-ups."

Then proceed straight to Step 2.

### Step 2 — Run 8 mandatory web searches *(internal — silent, parallel)*

Replace `[niche]` and `[current month year]`:

1. `[niche] TikTok trending videos this week [month year]`
2. `viral [niche] Instagram Reels [month year]`
3. `[niche] YouTube Shorts trending [month year]`
4. `[niche] podcast clips viral [month year]`
5. `[niche] street interview content [month year]`
6. `[niche] UGC ads working Meta [month year]`
7. `[niche] hooks that stop the scroll [month year]`
8. `[niche] competitor brands social strategy [month year]`

Extract: format, hook patterns, visual style, brands, engagement.

### Step 3 — Fetch 2+ source pages in parallel

`web_fetch` the most useful URLs. Pull verbatim hook lines and creative patterns to seed
the brief.

### Step 4 — Synthesize the Viral Content Brief (internal markdown — Stage 2 builds HTML)

Translate every trend into one of the 8 formats. Required fields per idea:

```
N. [Title]
- Format: [1 of 8 from the format library]
- Production: [AI | REAL]
- Preset (if AI): [slug] · Mode: [title-case]
- Duration: [4–15s for AI; up to 60s for REAL podcast clip]
- Aspect: 9:16 | 1:1 | 16:9
- Setting: [picklist value or "n/a"]
- Hook (if AI): [picklist value or "none"]
- Audio: [true/false]
- Scene prompt OR shot list: [prompt for AI; shot list for REAL]
- Social caption: [post copy — NEVER rendered on-screen]
- Inspired by: [specific trend / competitor]
- Why viral now: [specific reason tied to research]
```

### Producibility self-check (every idea, before adding)

1. Duration ≤15s for AI ideas? If no, route to REAL or split.
2. Format matches its strength (review → talking head, unbox → reveal, challenge → UGC)?
3. Hook + setting are picklist values for AI ideas?
4. No lip-sync / multi-character / split-screen on AI ideas?
5. REAL formats include a shot list with framing, lens, location, talent direction?

### Step 5 — Internal approval gate (button)

Don't present the raw research brief to the user — Stage 2 does that as a polished HTML
doc. Just confirm scope:

> "Research done — [X] viral trends pulled, [Y] competitor brands analyzed. Ready to
> build the Client Strategy Brief?"
> - "Yes — build the brief (Recommended)"
> - "Add more research (pull more trend searches)"
> - "Refocus on a different angle"

---

## STAGE 2 — Client Strategy Brief (the headline deliverable)

**Banner:** 🗂️ Stage 2: Client Strategy Brief — starting now.

### Goal

One polished HTML document the user sends to the client. This is what gets approved
before any production happens. Premium design, brand-aware colors derived from the
product image, dense with research evidence.

### Step 1 — Confirm campaign details (single AskUserQuestion, all buttons + smart defaults)

Auto-derive defaults from research + product image. Ask only what can't be inferred:

- **Campaign name** — "Use auto: [Brand] Viral Content Campaign [month year]" · "Custom"
- **Date range** — "Next 30 days" · "Next 60 days (Recommended)" · "Next 90 days" · "Custom"
- **Variants** — multiSelect listing every variant detected on the product

Goal, brand colors, target market, the 8-format split are all auto-derived. No
"breakdown" confirmation — that exposes the mechanic.

### Step 2 — Generate the HTML brief

**Required sections (in order):**

1. **Cover** — client name, brand name, brief date, "Viral Content Strategy" title, brand-derived hero color
2. **Executive Summary** — 1 paragraph: niche, target audience, the bet (what formats will dominate), expected output ([VIDEO_COUNT] videos + image pack), production timeline
3. **The Trend Landscape** — table of trends pulled from research, each with: trend name, where it's winning (TikTok / IG / YouTube / podcasts), example brands using it, why it works
4. **Competitor Audit** — table of 5–10 competitor brands, format mix they're using, what they're missing
5. **Recommended Content Mix** — woven naturally, not as a config card. Show the 8-format breakdown with counts ("13 street interviews, 13 podcast clips, 13 founder POV, 13 day-in-life vlogs, 12 challenge clips, 12 talking-head reviews, 12 unboxings, 12 ASMR close-ups") AS A CONSEQUENCE of the trends the research surfaced. Use language like: "Based on what's actually winning this week in [niche], here's how the campaign breaks down…"
6. **AI vs Real-Shot Split** — explicit table showing which formats are AI-generated (Higgsfield) vs real-shot (creator + product on camera). Counts per route. Why this split: AI handles the volume + variety on formats where consistency matters less; real shot handles the trust-driven formats (founder voice, podcast credibility, vlog authenticity).
7. **The 8 Format Battle Cards** — one card per format with: definition, why it wins, 3 concept seeds (titles only — full prompts in production), example hook line, recommended posting cadence
8. **Hook Library** — verbatim hook lines from research, organized by format. The client can see exact language being used.
9. **Production Calendar** — date-by-date table for the campaign window: Date · Format · Production route · Concept · Where it posts (paid / organic / both)
10. **Paid vs Organic Distribution** — which videos go into Meta paid campaigns, which go to organic feed posts only, which run both. Default split: top 30% performance creatives → paid; everything → organic feed.
11. **Production Plan** — Stage 3 preview: how the AI batches will run, what shot lists the client/creator gets, image asset pack contents
12. **What Happens Next** — 4-step plain-English: (1) Client signs off on this brief, (2) AI videos generate in 24h, (3) Shot lists handed off to creator + filmed within 7 days, (4) Everything scheduled to Meta + posted organic on approved dates
13. **Cost Note** — brief line: "Full cost breakdown — actual spend vs traditional production — delivered after Stage 5."

**Design rules for the HTML:**
- Brand-derived hero color (pull from product image)
- Premium typography (Inter / Söhne / system stack with weighted hierarchy)
- Tables with subtle borders, generous padding, NO em dashes anywhere
- Format cards laid out in a 2- or 3-column grid
- Mobile-responsive (≤768px collapses to single column)
- Print-friendly (the client may print and review on paper)

**Save to:** `/mnt/user-data/outputs/[brand]-content-strategy-brief.html`

### Step 3 — Present the brief + button approval

> "Brief is ready — [link to file]. This is what you send the client. Ready to produce?"
> - "Client approved — start production (Stage 3)"
> - "Wait — I need to send to the client first"
> - "Revise sections (which one?)"
> - "Add more concepts to a specific format"

If "Wait — send to client first," pause the pipeline. The user resumes when they get
approval (next turn or next session).

---

## STAGE 3 — Production

**Banner:** 🎬 Stage 3: Production — starting now.

### Goal

Execute the brief. AI-renderable formats run through Higgsfield in batches with permission
gates. Real-shot formats get polished shot-list documents the client hands to a creator.
Image asset pack closes Stage 3.

### Step 1 — Upload product image to Higgsfield *(silent)*

`media_upload` → curl PUT → `media_confirm` → product UUID. Pass as reference in all
AI generations. Friendly status line acceptable: "Getting your product ready…"

### Step 2 — Resolve hook_id, setting_id, preset avatar at runtime *(silent)*

For each AI-format row: resolve hook name → UUID, setting name → UUID, pick a preset
avatar matching the format persona (see avatar routing below).

**Avatar routing per format:**
- **Street Interview** — rotate 2 preset avatars per scene (interviewer + stranger). Casual, "real people" look.
- **UGC Challenge** — energetic Gen-Z creator, casual outfit. Rotate 2–4 per batch.
- **Talking-Head Review** — authentic mid-20s–30s reviewer. Rotate 2–4 per batch.
- **Unboxing** — hands-only preferred; sometimes lifestyle creator partial face.
- **ASMR** — hands-only preferred; intimate / soft persona if face shown.

**Hard rule:** Every `generate_video` call MUST pass `avatars: [{id: <preset_uuid>, type: "preset"}]`.
Never empty array — that causes a fresh random face per render and kills consistency.

If no preset avatars surface for the account, fall back to empty AND warn the user:
"Heads up — no preset avatars found. Faces in this batch will vary per video."

### Step 3 — Per-batch permission gates (REQUIRED — do not skip)

Process the AI batches in this order (5 batches total). Real-shot deliverables come after.

| Batch | Format | Higgsfield preset / mode |
|---|---|---|
| 1 | Street Interview | `ugc` / `"UGC"` + `Interview` hook + `Street` setting |
| 2 | UGC Challenge | `ugc` / `"UGC"` |
| 3 | Talking-Head Review | `product_review` / `"Product Review"` |
| 4 | Unboxing | `ugc_unboxing` / `"Unboxing"` |
| 5 | ASMR | `ugc` / `"UGC"` + `generate_audio: true` |

Before each batch, AskUserQuestion (single round-trip, all buttons):

> "Ready to generate the **[N] [Format]** videos? ([resolution], [9:16], audio [on/off])"
> - "Yes — generate all [N]"
> - "Start with 3 for a quality check first (Recommended)"
> - "Skip this batch for now"
> - "Change settings before generating"

Wait for click. Only then fire `generate_video`. After each batch: `job_display` to show
results, then auto-prompt the next batch.

### Step 3a — Set `mode` explicitly on every call *(silent — never narrate slug-mismatch table)*

Without explicit `mode`, Marketing Studio defaults to UGC and rewrites prompts. Use the
title-case `mode` value from `presets[].mode` (server normalizes both forms):

| Format | mode value |
|---|---|
| Street Interview / Challenge / ASMR | `"UGC"` |
| Talking-Head Review | `"Product Review"` |
| Unboxing | `"Unboxing"` |

### Step 4 — Prompt template per row (NO on-screen text, EVER)

**HARD RULE:** Zero rendered text — no captions, subtitles, watermarks, lower-thirds, or
typography of any kind in the generated video. Social captions live as upload metadata, NEVER as overlays.

```
[Scene prompt from brief].
Product: [name], [packaging detail — color, label, hangtag].
Style cues: [preset-specific — "authentic, handheld, natural daylight" for UGC;
             "intimate ASMR close-up, no music, audible product handling" for ASMR;
             "polished cinematic, golden hour" for TV Spot].
Negative: no text overlay, no captions, no subtitles, no on-screen text, no watermarks,
no lower-third, no graphic typography, no brand callout banners. Clean image only.
```

Never paste the social caption / post copy into the prompt — it's metadata for upload.

### Step 5 — Real-shot deliverables (Podcast Clip / Founder POV / Day-in-Life Vlog)

After all AI batches are complete, generate the real-shot production package as ONE
deliverable:

**File:** `/mnt/user-data/outputs/[brand]-real-shot-production-guide.html`

**Contents per concept:**
- Concept title + format (Podcast / Founder POV / Vlog)
- Duration target (Podcast Clip: 30–60s · Founder POV: 15–45s · Vlog: 30–60s)
- Setup: location, time of day, props, wardrobe, lighting note
- Shot list: numbered shots with framing (wide / medium / close), lens recommendation, action
- Verbatim script (Founder POV) OR conversation prompts (Podcast Clip) OR action beats (Vlog)
- Caption / chyron suggestion (for Podcast Clip — text appears on-screen for these in post)
- Hook line (first 3 seconds)
- CTA line (last 3 seconds)
- Inspired by: [specific viral example from research]

These are the formats the client's team or creator films in real life. The skill is not
generating these — it's writing the playbook so the human shoot goes fast and on-brand.

### Step 6 — Image asset pack (auto-generated via GPT Image 2)

After videos AND real-shot guide are done, fire ONE permission gate:

> "Production done. Ready for the image asset pack — [N] images via GPT Image 2?"
> - "Yes — generate all [N] (Recommended)"
> - "Yes — but skip with-people shots"
> - "Yes — but skip without-people shots"
> - "Skip image pack entirely"

**Pack count:** `floor(VIDEO_COUNT / 5)`. Breakdown: **40% Social · 20% Hero · 20% With-people · 20% Without-people.**

| Videos | Pack total | Social | Hero | With-people | Without-people |
|---|---:|---:|---:|---:|---:|
| 50 | 10 | 4 | 2 | 2 | 2 |
| 100 | 20 | 8 | 4 | 4 | 4 |
| 150 | 30 | 12 | 6 | 6 | 6 |
| 200 | 40 | 16 | 8 | 8 | 8 |

Generate via Higgsfield `generate_image` with `model: "gpt_image_2"`, passing product
UUID in `medias[]` (role: `image`). Aspect ratio: 1:1 for social, 16:9 for hero, mixed
for with/without-people. `quality: "high"`, `resolution: "2k"`.

**Save to:** `/mnt/user-data/outputs/[brand]-asset-pack/` with descriptive filenames
(`social-01-watermelon-kitchen.png`, `hero-02-lifestyle.png`, etc.).

### Step 7 — Production complete

> "Production wrapped. AI videos: [N] · Real-shot scripts: [M] · Image pack: [P]. Continue?"
> - "Yes — schedule everything (Stage 4 — Recommended)"
> - "Re-do specific assets"
> - "Pause here"

### Standalone modes

**Brief-only mode:** if user picks Stage 2 in onboarding (Step B), stop after delivering the
HTML brief. No production. The brief is the deliverable; client can use it standalone.

**Image-pack-only mode:** if user explicitly asks "generate just the image pack" / "make
static visuals only," skip Stages 1–2 + AI video batches. Auto-detect product silently, ask
only for image-pack count, fire `generate_image` directly. Same 40/20/20/20 breakdown.

### Failure handling

If `generate_video` fails (rate limit, MCP error), log failed plan-row IDs and offer to
retry. Don't silently skip.

---

## STAGE 4 — Scheduling

**Banner:** 📅 Stage 4: Scheduling — starting now.

### Step 1a — Meta MCP connection check (FIRST question, always)

Before anything else in Stage 4:

> "Quick check — is Meta Ads MCP connected to your workspace?"
> - "Yes — Meta MCP is connected (Recommended)"
> - "Not connected — help me install it now"
> - "Skip live scheduling — export the calendar instead"

**If "Yes":** proceed to Step 1b.

**If "Not connected":** surface the install path. Call `search_mcp_registry` with `["meta ads", "facebook ads", "meta marketing"]`, then `suggest_connectors` so an install card renders. Fallback line: "If the install card doesn't show, open Settings → Connections and search 'Meta Ads.'" After install confirmation, loop back to Step 1a.

**If "Skip — export calendar":** export `[brand]-content-calendar.csv` with columns:
Date · Time · Format · Production route · Preset (if AI) · Video filename · Image filename
· Social caption · Goal · Paid/Organic · Notes. Save to outputs. Skip rest of Stage 4 →
Stage 5.

### Step 1b — Meta Ads campaign details (single AskUserQuestion, all buttons)

- **Objective:** "Awareness" · "Traffic" · "Conversions" · "Mixed (Recommended)"
- **Budget tier:** "$500" · "$1,500 (Recommended)" · "$5,000" · "Custom"
- **Date range:** "Match brief dates (Recommended)" · "Next 30 days" · "Custom"

Ad account auto-detected from MCP. Only ask if multiple accounts surface.

### Step 2 — Content calendar review (button approval)

Present the calendar, then:

> "Schedule looks good?"
> - "Yes — schedule everything"
> - "Yes — but start with week 1 only"
> - "Adjust dates first"

### Step 3 — Create Meta campaigns via MCP

For each batch:
- Create Ad Campaign with the objective
- Create Ad Sets with targeting (AskUserQuestion: "Auto-target lookalike from product image" / "Use saved audience" / "Define new")
- Upload Higgsfield videos + images as creatives
- Schedule per the calendar dates

### Step 4 — Organic calendar export

In parallel with Meta scheduling, export the organic posting calendar (`[brand]-organic-calendar.csv`):
- Date · Platform (TikTok / IG Reels / YT Shorts) · Format · Video filename · Hook line · Caption · Hashtag block · CTA

The client's social manager posts these organically per the calendar.

### Step 5 — Confirm scheduling

Summary table by week (paid + organic side by side). Final button gate:

> "Scheduling done — continue to Stage 5?"
> - "Yes — render cost report (Recommended)"
> - "Pause one of the paid campaigns"
> - "Generate more content"
> - "Skip Stage 5 — close pipeline"

---

## STAGE 5 — Cost Report

**Banner:** 💰 Stage 5: Cost report — starting now.

### Goal

Polished HTML report comparing **actual Higgsfield credit + USD spend** against
**traditional production cost** for the same volume. Savings ratio + time savings.

### Step 1 — Pull live spend from Higgsfield *(silent)*

Call `transactions(limit=200)`. Filter to jobs created during the Stage 3 generation
window. Sum:
- Credits per preset (UGC / Product Review / Unboxing — only the AI batches)
- Credits for image generation (GPT Image 2)
- Total credits

Convert credits → USD using the user's plan rate (Creator ≈ $0.02/credit, Team/Pro ≈
$0.01–$0.005/credit). If plan rate isn't surfaced, present credits-only and note that USD
is plan-dependent.

### Step 2 — Apply traditional production cost model (industry midpoints, 2026)

Default cost model — show low/mid/high range, cite "Industry-average estimates, 2026":

| Asset type | Low | Mid | High | Why the range |
|---|---:|---:|---:|---|
| UGC creator video (TikTok / Reels) | $250 | $750 | $1,500 | Creator fee + light production |
| Talking-head review video | $300 | $900 | $2,000 | Talent + setting + edit |
| Street interview video | $400 | $1,200 | $2,500 | Crew + on-location + edit |
| Unboxing video | $300 | $800 | $1,500 | Box prep + creator + edit |
| ASMR close-up video | $250 | $700 | $1,400 | Audio engineer + macro shoot |
| Podcast clip (real-shot, included in podcast budget) | $0 | $200 | $500 | Edit-only if podcast already filmed |
| Founder POV (real-shot, DIY camera) | $0 | $300 | $800 | DIY → light edit |
| Day-in-life vlog (real-shot, creator hire) | $400 | $1,000 | $2,200 | Creator fee + multi-location |
| Social image (lifestyle still) | $150 | $400 | $900 | Photographer + edit |
| Hero banner image (16:9 cinematic) | $300 | $800 | $1,800 | Studio + retouch |

### Step 3 — Build the comparison

For each AI-generated asset, multiply count × mid rate. Sum to total traditional cost.
For real-shot deliverables (Podcast / Founder POV / Vlog), use the mid range — these are
delivered as shot lists, but the client still pays the creator. Make this distinction
explicit in the report so the savings number is honest.

**Compute:**
- Actual spend (Higgsfield credits + USD)
- Traditional cost low / mid / high
- Savings (USD + percentage)
- Time savings (hours saved vs traditional production timeline)

### Step 4 — Render the HTML report

**Save to:** `/mnt/user-data/outputs/[brand]-cost-savings-report.html`

**Sections:**
1. **Headline number** — "$[X] saved vs traditional production" (mid estimate)
2. **What you actually spent** — Higgsfield credits + USD breakdown by format
3. **What traditional would have cost** — low/mid/high estimates with the asset-rate table
4. **Time saved** — production days (Higgsfield ~24h vs traditional ~30 days for [VIDEO_COUNT])
5. **Savings ratio** — visual: "$X spent / $Y saved / Z% efficiency"
6. **Caveats** — credit-to-USD rate is plan-dependent; real-shot deliverables still incur creator fees; quality variation across AI batches
7. **What's next** — schedule the next campaign / scale the winning formats / production-ready brand library accumulated

### Step 5 — Present and close

> "Cost report ready — [link to file]. Anything to follow up on?"
> - "Schedule the next campaign"
> - "Generate more content for a winning format"
> - "Export everything (brief + assets + calendar + report) as one ZIP"
> - "All done — close out"

---

## APPENDIX — Concept seeds per format

Generate varied concepts within each format using these seeds. No two videos in the same
format should share the same concept seed.

### Format 1 — Street Interview
- "What's your favorite [niche] right now?" → stranger pulls product from bag
- "Sing for the product" — sing a jingle, get the bottle
- "Rate this [product] out of 10" — sip then score
- "Try this on a hot day" — first-sip face from a real stranger
- "Trade me your coffee for this" — bartering bit
- Two strangers blind opinion → reveal the brand
- "$100 if you can drink it without smiling" — challenge gone wrong
- "How much do you think this costs?" → guess vs reveal

### Format 2 — Podcast Clip (REAL)
- Bold claim from founder ("Most [niche] brands are lying about this")
- 90-second origin story ("Why I quit my job to build this")
- Hot-take controversy ("Why ingredient X is a scam")
- Behind-the-scenes reveal ("Here's what most brands don't tell you")
- Industry stat callout ("78% of [niche] in stores has Z" — cite source)
- Customer story ("This guy DM'd me and changed how we do everything")
- Future bet ("Why we're betting everything on [angle]")
- Quick-fire Q&A clip (5 questions in 60s)

### Format 3 — Founder POV / Story (REAL)
- "I built this because…" — confession to camera
- "Stop buying [generic category] — here's why" — contrarian PSA
- "Day 1 vs Day 365" — split-screen progress (real DIY edit)
- "Three things nobody tells you about [niche]" — listicle to camera
- "My biggest mistake" — vulnerability hook
- "Why I'll never go back to [old way]" — conversion story
- "What's actually in your [product category]" — ingredient deep dive
- "The DM that changed everything" — customer-driven moment

### Format 4 — Day-in-Life Vlog (REAL)
- 5am routine with product baked in
- Coffee shop day, product on the table
- Gym day → post-workout product moment
- Travel day vlog → product as the constant
- Work-from-home, mid-afternoon product hit
- Saturday errands → product cameo at each stop
- Date night setup → product reveal
- Sunday reset → product in the routine

### Format 5 — UGC Challenge / Entertainment (AI)
- Blind taste try — guess which one is [brand]
- "$100 if you try it" street challenge
- "Will it pour?" — pour on something absurd
- Product flying into frame deadpan reaction
- Failed dare → recover → review pivot
- Backflip → land badly → unflappable product hold
- "Drink this in 10 seconds" timer challenge
- Two people, one product, one wins

### Format 6 — Talking-Head Product Review (AI)
- Two-ingredient test — read label, raise eyebrow, sip
- Cold-side-of-the-fridge ranking
- Side-by-side — generic shatters → restored shot of brand
- 7-day diary — empty bottles on counter
- Beauty-editor mirror review (Bathroom + Spicy hook)
- Final flavor ranking — all variants lined up
- "I expected to hate this" reversal
- Honest pros/cons — quick-cut

### Format 7 — Unboxing (AI)
- Trio reveal — three flavors / variants in pastel paper
- Solo drop with slow ribbon-pull
- Subscription box drop with brand note
- Premium gift-set unbox (ribbon, handwritten tag)
- Hangtag macro series — close-ups on tags
- Crate / wooden-straw "picked today" reveal
- Mystery box reveal — guess before open
- Two-layer reveal — outer box, then inner

### Format 8 — ASMR (AI)
- Macro cap-unscrew + glug pour into iced glass
- Condensation-bead slide on chilled bottle, then open
- Spoon-clink + ice-drop into tall glass + product pour
- Bottle-on-marble tap-and-rotate
- Ribbon-pull / paper rustle (when crossed with unboxing)
- Two bottles clinking gently, no soundtrack
- Pour into wood, splash micro-sound
- Bag-crinkle + open + scoop (snacks)

---

## OPEN HOOKS (PICKLIST REFERENCE)

UGC-family hooks seen live in Marketing Studio (resolve UUIDs at runtime via Step 0):

Product Hit · Spicy · Interview · Random Object Mic · Product Crash · Blizzard · Camera
Bump · Product Dodge · Epic Fail · (and "none" for ASMR / Unbox)

Settings (UGC family) — realistic: Bedroom · Bathroom · Kitchen · Office · In Car · Street
· Gym · Nature. Unrealistic: Airplane Wing · Roofing · Volcano Rim · Tiny Reviewer · Car
Roof · Train Surf.

---

## KEY CONTRASTS WITH THE OLD VIDEO-ONLY PIPELINE

If you've used the prior version of this skill, note these changes:

1. **Headline deliverable shifted** — was a video plan; now a client-ready strategy brief.
2. **Format library expanded from 5 to 8** — added Podcast Clip, Founder POV, Day-in-Life Vlog. These are the trust-driven formats that need real humans on camera.
3. **AI vs REAL split is explicit** — the brief tells the client which videos are AI-generated and which they need to film. No surprise on production day.
4. **Coverage = paid + organic** — Stage 4 exports both Meta Ads schedule AND an organic posting calendar. The campaign isn't done when paid is set up; organic is half the engine.
5. **Brief-only mode** — Stage 2 can be the final deliverable for clients who want strategy without execution.

Everything else (button UX, silent internals, banners, "no on-screen text" rule, Higgsfield
mechanics) carries over identically.
