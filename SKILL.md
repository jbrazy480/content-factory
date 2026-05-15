---
name: content-factory
description: >
  Build a complete client-ready viral content strategy and execute it end to end. Starts
  with a Phase 0 discovery conversation that captures the OFFER (what they sell, price,
  who buys), the AUDIENCE (real ICP, pain, current alternatives), and the CTA (form fill,
  booked call, free trial, demo) — biased toward lead gen since most clients are running
  lead campaigns. Lets the user choose their production track: AI-generated ads (Higgsfield
  Marketing Studio, with a built-in setup walkthrough if they're not connected yet), real
  human-shot content (delivered as shot lists + scripts), or both. Stage 1 runs real
  competitor research and a dedicated hook-and-CTA workshop because the hook makes or
  breaks the ad — funny podcast-style hooks especially. Stage 2 ships a polished HTML
  Client Strategy Brief built around the 8 viral formats winning right now (street
  interviews, podcast clips, founder POV, day-in-life vlogs, UGC challenges, talking-head
  reviews, unboxings, ASMR). Stage 3 produces the AI videos in Higgsfield and the
  real-shot production guides. Stage 4 schedules paid creatives to Meta Ads and exports
  the organic calendar. Stage 5 renders a savings report. Button-driven UX — clicks, not
  typed commands. Trigger on a product image + content request, or phrases like 'content
  strategy', 'viral content plan', 'content brief for a client', 'build a content factory',
  'create a campaign', 'lead gen ads', 'help me with ads for my offer', 'content for
  [client]'.
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

## PHASE 0 — DISCOVERY (run BEFORE the technical onboarding)

> ⚠️ A great strategy is downstream of a great offer + audience + CTA. The skill MUST
> capture these before doing research, otherwise the brief will be generic. Phase 0 is a
> structured conversation, NOT a form. Use AskUserQuestion buttons with smart defaults
> that the user can accept in one click — typing is only required for content the user
> must originate (offer name, price, audience descriptor).

Send Phase 0 as a **SINGLE AskUserQuestion call** with multiple questions. Auto-detect
defaults from any product image / URL already provided so most answers are one click.

### The 4 Phase 0 questions

**Q1 — The offer (what are they selling?)** [button + Other]
Auto-detect a default from the product image / URL and offer it as the first button. The
user clicks to accept or picks Other to type the real thing.

- "Use auto: [detected — e.g. 'Cold-pressed coffee subscription · $39/mo']"
- "Physical product (one-time purchase)"
- "Subscription / membership"
- "Service / done-for-you offer"
- *Other → type the actual offer in one line: WHAT it is + PRICE + format (one-time / monthly / project-based)*

**Q2 — The ICP (who actually buys it?)** [button + Other]
Auto-detect demographic cues from packaging style. Offer 3 plausible ICP buckets the user
can accept or override.

- "Use auto: [detected — e.g. 'Wellness-leaning Millennials/Gen Z, urban, $80k+ HH income']"
- "Service business owners (HVAC, dental, medspa, fitness, real estate)"
- "Sales teams / sales managers (5–50 reps doing outbound)"
- *Other → type the real ICP: who they are + what they currently use instead*

**Q3 — The desired action (the CTA)** [button-only — this is critical]
Bias toward lead gen since most MetaTech clients are running lead campaigns. The CTA
shapes every hook, every script ending, every form field.

- "**Form fill (lead gen — Recommended for service businesses)**"
- "Booked call / demo via calendar link"
- "Free trial signup / free-to-start activation"
- "Direct purchase (ecommerce)"
- "DM the brand (Instagram-first lead capture)"
- *Other → type the specific desired action and where it happens (URL, landing page, DM, etc.)*

**Q4 — Tone / personality** [button]
This determines hook style. Funny podcast-style ads are wildly viral right now — surface
that as a first-class option, not buried.

- "**Funny / podcast-style (Recommended — winning hook style right now)**"
- "Authoritative / educational"
- "Confessional / founder-direct (vulnerable, raw)"
- "High-energy / hype (challenge content, Gen Z)"
- "Premium / aspirational (luxury, beauty, fashion)"

### Storing the answers

Cache all 4 answers in working memory as the **Offer Profile**. Every downstream stage
references the Offer Profile:

- Stage 1 trend research queries use the OFFER + ICP keywords
- Competitor research uses the OFFER category
- Hook Library generation uses the TONE
- Format Mix biases by CTA (lead-gen CTAs → favor Talking-Head Review + Founder POV +
  Street Interview; ecommerce CTAs → favor Unboxing + ASMR + Hyper Motion)
- Stage 2 brief positions the strategy around the OFFER + ICP, NOT the product alone
- Stage 3 prompts include the OFFER value prop in every scene description
- Stage 4 Meta Ads campaign objective auto-sets from the CTA (form fill → Leads objective;
  booked call → Leads objective; trial → Conversions; purchase → Sales)

### One-line summary back to the user (after Phase 0)

> "Got it — [OFFER] for [ICP], driving to [CTA] with a [TONE] flavor. Pulling up the
> production options now."

Then proceed to ONBOARDING (technical setup) below.

### When Phase 0 can be auto-skipped

If the user already provided all four pieces in their initial message ("I'm running a
$39/mo coffee subscription targeting wellness Gen Z, need lead gen form fills, want funny
podcast-style ads"), confirm the auto-detected Offer Profile back to them in ONE
AskUserQuestion ("Looks like [summary]. Confirm and start?" / "Adjust the offer" /
"Adjust the ICP" / "Adjust the CTA") and proceed if they confirm.

### Why Phase 0 matters

Without it, the brief reads like a template. With it, every hook, scene, and CTA in the
brief is anchored to a specific offer transformation ("Service business owners using $97/
seat dialers" vs "Anyone in the market for a dialer") — and that's the entire
differentiator between a brief the client signs and a brief that gets edited to death.

---

## ONBOARDING — single-shot, no pauses

Send ALL onboarding questions in ONE AskUserQuestion call. Never sequence.

**Step A — Production track** (button — THE most important choice)
Determines which formats are in scope and whether we even need Higgsfield.

- "**AI ads + Real-shot — Both (Recommended)**" — full 8-format mix, ~63% AI / ~37% real
- "AI ads only" — Higgsfield required; campaign uses 5 AI formats only (no podcast clip, no founder POV, no vlog); cheaper, faster, less authentic
- "Real-shot only (no AI generation)" — campaign uses the 3 real-shot formats + real Street Interview; we deliver shot lists + scripts; no Higgsfield needed
- "I'm not sure — explain my options" — see "Track choice explained" below

**Step A.1 — Higgsfield setup (CONDITIONAL — only fires if Track = AI or Both)** (button)
- "Yes — Higgsfield is connected"
- "Not yet — walk me through setup"
- "I'll set it up later — start with the brief only"

If user picks "Walk me through setup," fire the **Higgsfield Walkthrough** (see below).
Skip Step A.1 entirely if Track = Real-shot only.

**Step B — Starting stage** (button)
- "Stage 1 — Full pipeline (Recommended — needs product image)"
- "Stage 2 — Build the brief only (skip production)"
- "Stage 3 — Produce now (I have a brief)"
- "Stage 4 — Schedule (content is ready)"

**Step C — Campaign volume** (button + Other)
"50 videos" · "100 videos (Recommended)" · "150 videos" · "200 videos" · Other → any number.

Store as `[VIDEO_COUNT]`. Image pack count = `floor(VIDEO_COUNT / 5)`.

**Volume split logic by track:**
- **Both** — `floor(VIDEO_COUNT / 8)` per format, remainder starts at format 1
- **AI only** — `floor(VIDEO_COUNT / 5)` per AI format (Street Interview, Challenge, Review, Unboxing, ASMR); remainder starts at Street Interview
- **Real-shot only** — `floor(VIDEO_COUNT / 4)` per real-shot format (Street Interview-real, Podcast Clip, Founder POV, Day-in-Life Vlog); remainder starts at Podcast Clip

Do NOT show the split at this step. It surfaces naturally inside the Stage 2 brief.

**Step D — Product / brief input** (file attach prompt in the same message)
"Attach the product image to this message OR drop a URL — that's all I need to start."

If a product image is already attached, skip D.
If user picked Stage 3+ in Step B, swap D with: "Drop your approved brief or paste it here."

**Single-message rule:** Step A + (A.1 only when AI/Both) + B + C buttons + D prompt go out
in ONE message. User clicks, attaches the product, and the pipeline starts.

### Track choice explained (only shown if user clicks "I'm not sure")

Send this as a follow-up message, then re-ask Step A:

> **Quick read on your options:**
>
> 🤖 **AI ads only.** Fastest + cheapest. We render everything in Higgsfield Marketing
> Studio — no crew, no shoot day. Best for: testing a new offer, scaling a winner, brands
> without an in-house creator. Trade-off: AI faces still read as "ad" to some viewers.
> Avoid for podcast / founder content — credibility drops.
>
> 🎥 **Real-shot only.** Most authentic. You (or a hired creator) shoot the content; we
> deliver scripts, shot lists, hooks, and CTAs. Best for: founder-led brands, podcast
> clips, day-in-life content, premium positioning. Trade-off: takes 1–2 weeks longer and
> costs more (creator fees).
>
> ⚡ **Both (Recommended).** The mix that actually wins right now. AI handles volume on
> formats where consistency doesn't matter much (unboxings, challenges, ASMR, reviews).
> Real shoots handle the trust-driven moments (podcast clips, founder voice, vlogs).
> This is the default because most viral campaigns blend both.

### Higgsfield Walkthrough (only fires if user picks "Walk me through setup")

Send these instructions inline + a follow-up button confirmation:

> **Higgsfield setup — takes about 5 minutes:**
>
> 1. **Go to [higgsfield.ai](https://higgsfield.ai)** and create an account. Use the same
>    email you use for Claude so connection is smooth.
> 2. **Pick a plan.** Creator (≈$0.02/credit) for testing, Team or Pro
>    (≈$0.01–0.005/credit) for production. A 50-video campaign typically runs $30–60 on
>    Creator, $15–40 on Team/Pro.
> 3. **Connect Higgsfield to Claude.** Open Claude → **Settings** → **Connectors** →
>    search for **Higgsfield** → click **Connect** and authenticate.
> 4. **Check the connection.** Open a new chat in Claude. Type *"What models does
>    Higgsfield have?"* — if Claude returns a real model list, you're set.
> 5. **Come back here** and click "Done — connected" below.
>
> *If the Higgsfield connector isn't in the Connectors list, your Claude plan may not
> have third-party connectors enabled yet. Pick "Skip — brief only" and I'll deliver
> the Strategy Brief as a standalone deliverable (you can run production later).*

AskUserQuestion follow-up:
- "Done — connected" → proceed to Step B
- "Skipped — give me the brief only" → set Track = Real-shot for purposes of this run, proceed to Step B
- "Need help — Higgsfield site isn't loading / something's broken" → offer fallback to brief-only mode + flag a manual install ticket

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

### Step 2 — Run 10 mandatory web searches *(internal — silent, parallel)*

Use the Offer Profile from Phase 0 to make searches specific. Replace `[niche]`,
`[offer_category]`, `[ICP_descriptor]`, and `[current month year]`:

1. `[niche] TikTok trending videos this week [month year]`
2. `viral [niche] Instagram Reels [month year]`
3. `[niche] YouTube Shorts trending [month year]`
4. `[niche] podcast clips viral [month year]`
5. `[niche] street interview content [month year]`
6. `[niche] UGC ads working Meta [month year]`
7. `[niche] hooks that stop the scroll [month year]`
8. `[niche] competitor brands social strategy [month year]`
9. `[offer_category] ads targeting [ICP_descriptor] [month year]` (NEW — direct ad-spy)
10. `funny podcast-style ads [niche] [month year]` (NEW — humor/podcast format spy)

Extract per result: format, hook patterns, visual style, brands, engagement.

### Step 3 — Competitor scan (NEW — structured, not just a search aggregate)

> Goal: identify 5–10 direct competitors in this offer category, document what they're
> doing on each platform, find the gap. This goes into the Stage 2 brief as the
> **Competitor Audit** table — clients pay attention to this.

**Method:**

1. **Identify competitors silently** by combining: (a) brand names that surfaced in the
   Step 2 trend searches, (b) `Facebook Ad Library` search via web_fetch for the offer
   category, (c) `Meta Ad Library` direct URL pattern:
   `https://www.facebook.com/ads/library/?active_status=all&ad_type=all&country=US&q=[offer_keyword]`,
   (d) any competitor URLs the user mentioned in Phase 0.

2. **For each competitor (target 5–10), capture:**
   - Brand name + website
   - Primary platform they're winning on (TikTok / IG / YouTube / Meta paid)
   - Format mix (estimate the dominant 2–3 formats)
   - Approximate posting cadence (daily / 3x week / weekly)
   - 2–3 example hook lines they're using right now (verbatim if found in research)
   - **The gap** — what they're NOT doing that we can own. This is the unlock.

3. **Identify the angle nobody owns yet.** Examples:
   - Competitor A dominates Unboxing but never does podcast clips → we own podcast.
   - Competitor B does only authoritative tone → we own funny.
   - Nobody is running Street Interview in this category → first-mover advantage.

The competitor scan is structured output — store as a working memory table the Stage 2
brief renders verbatim.

### Step 4 — Fetch 3+ source pages in parallel *(silent)*

`web_fetch` the most useful URLs from Steps 2 + 3 (target: 3+ pages, prioritize competitor
ad library pages, viral TikTok/IG examples, and any podcast-clip viral threads). Pull
verbatim hook lines and creative patterns to seed the brief.

### Step 5 — Hook Library workshop (NEW — hooks are the single highest-leverage element)

> The hook is what stops the scroll. The CTA is what drives the action. Everything in
> between is the bridge. Most ads die in the first 3 seconds because the hook is generic.
> This stage produces a **Hook Library** — 30+ hook variations the user can pick from
> before any production happens.

**Generate 30+ hooks organized by category** (tone from Phase 0 weights the mix):

**Category 1 — Curiosity hooks** (8 hooks)
- Pattern: open with a question the viewer needs answered.
- Examples: "Does this actually work?" · "Why is nobody talking about [thing]?" · "Is
  [common belief] a scam?" · "What if I told you [contrarian claim]?"
- Generate 8 specific to the OFFER.

**Category 2 — Pattern interrupts** (6 hooks)
- Pattern: visual or verbal jolt in the first 2 seconds.
- Examples: "STOP scrolling if you [target descriptor]…" · "Watch what happens when…" ·
  "I just realized [counter-intuitive thing]" · "This is going to make [audience] mad…"
- Generate 6 specific to the OFFER.

**Category 3 — Pain-named hooks** (6 hooks)
- Pattern: name the exact pain the viewer feels in the first sentence.
- Examples: "Tired of [specific pain]?" · "If you're still [common painful behavior],
  you're falling behind…" · "Watching [audience] [waste / lose / miss] [thing] is making
  me crazy…"
- Generate 6 specific to the OFFER + ICP pain points.

**Category 4 — Cost / receipt hooks** (4 hooks)
- Pattern: open with a specific dollar amount or stat.
- Examples: "You're losing $[X] a month to [pain]" · "$[Price] for [thing] is insane —
  here's what to do instead" · "[X]% of [audience] are doing this wrong"
- Generate 4. Numbers must be real and grounded in ICP economics.

**Category 5 — Funny / podcast-style hooks** (6 hooks — the winning style right now)
- Pattern: setup → punchline. Tone of a podcast moment that got clipped because it was
  hilarious. Often self-deprecating, contrarian, or shocking.
- Examples: "I gotta get this off my chest…" · "Hot take: [niche tradition] is dumb" ·
  "Three years ago I was wrong about [thing] and here's the receipt" · "Why I'll never
  go back to [old way]"
- Generate 6 in funny/podcast tone. This is the format James specifically called out as
  viral right now — over-index here unless Tone = Premium.

**Category 6 — Founder confession hooks** (4 hooks)
- Pattern: founder vulnerability up front.
- Examples: "I almost shut this down last year" · "The customer DM that changed
  everything" · "My biggest mistake building [company]" · "I built this because [pain]"
- Generate 4. These power the Founder POV format.

**Hook validation rules:**
1. Every hook must be ≤12 words for AI-format videos, ≤20 words for real-shot podcast clips.
2. Every hook must pass the "scroll test": would a stranger pause at this in their feed?
3. Every hook must work for the OFFER + ICP combo from Phase 0. If a generic hook
   wouldn't work for THIS client, swap it.
4. Avoid em dashes in spoken hooks. Avoid "Discover," "Unlock," "Revolutionary,"
   "Game-changing" — these are corporate words, not viral words.

### Step 6 — CTA Library workshop (NEW — biased toward the Phase 0 CTA choice)

> Most ads end with "Click the link." That's not a CTA, that's a sentence. Generate 8
> CTAs specific to the chosen action — these become the scripted endings of every video.

**Generate 8 CTAs** matched to the Phase 0 CTA choice. Examples by CTA type:

**If CTA = Form fill (lead gen):**
1. "Click the link below, drop your info, and we'll [specific value delivery in 24h]."
2. "Tap the link, answer 4 questions, and we'll [outcome]."
3. "Hit the link, leave your email, and we'll [deliverable] — no call required."
4. "Click below, fill out the form, and we'll [next step] within [timeframe]."
5. "If this is you, click the link and let us know — we'll handle the rest."
6. "The link below takes you to a 30-second form. Fill it out, we'll [action]."
7. "Drop your details below and we'll [outcome] — no pressure, no hard sell."
8. "Click the link, tell us [qualifier], and we'll [next step]."

**If CTA = Booked call:**
1. "Click below to book a 15-minute call — we'll [specific outcome]."
2. "Hit the link, pick a time on my calendar, let's talk."
3. "Tap below to book — first 10 spots this week."
4. "Click the link to grab a slot — bring your [specific input]."
5. "Drop your time below and we'll send a confirmation in 60 seconds."
6. *(Continue pattern for 8 total)*

**If CTA = Free trial / activation:**
1. "Click the link, drop your number, AI calls you in 30 seconds. If it sounds robotic,
   don't use it." *(This is the proven RizzDial CTA pattern — clone for similar offers.)*
2. "Tap the link, start your free [trial type], no card needed."
3. "Click to activate — takes 60 seconds, free forever."
4. *(Continue pattern for 8 total)*

**If CTA = Direct purchase (ecommerce):**
1. "Tap below — first 100 ship today."
2. "Click the link, use code [code] for [discount]."
3. "Snag yours below — the [size/variant] always sells out first."
4. *(Continue pattern for 8 total)*

**If CTA = DM the brand:**
1. "DM us the word '[trigger word]' and we'll send [deliverable]."
2. "Comment '[word]' below and we'll DM you the [thing]."
3. *(Continue pattern for 8 total)*

**CTA validation rules:**
1. Every CTA must reference the SPECIFIC desired action (no generic "click below").
2. Every CTA must include a benefit + a reduction of friction (free, no card, takes 30 sec,
   no pressure, no hard sell, money-back guarantee).
3. Every CTA must be sayable in 2 seconds or less (or 1 line of caption text).

### Step 7 — Synthesize the Viral Content Brief (internal markdown — Stage 2 builds HTML)

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

### Step 8 — Internal approval gate (button)

Don't present the raw research brief to the user — Stage 2 does that as a polished HTML
doc. Confirm scope AND surface the hook + CTA library counts so the user feels the depth
of work done:

> "Research done. Here's what I pulled:
> - [X] viral trends across TikTok / IG / YouTube / podcast clips
> - [Y] direct competitors mapped with format gaps
> - [Z] hooks generated across 6 categories (curiosity, pattern interrupt, pain-named,
>   cost/receipt, funny/podcast, founder confession)
> - 8 CTAs matched to your [chosen CTA from Phase 0]
>
> Ready to build the Client Strategy Brief?"
> - "Yes — build the brief (Recommended)"
> - "Show me the hooks first — I want to pick favorites before the brief"
> - "Add more competitor research"
> - "Refocus on a different angle"

**If user picks "Show me the hooks first":** present the full Hook Library inline (all 6
categories, all 30+ hooks), then AskUserQuestion as a multiSelect: "Which hooks are
must-have in the brief? (Pick up to 12.)" Filter the brief's hook section to those
favorites + auto-add the top 3 from each unselected category for variety.

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

**Required sections (in order — every section must appear):**

1. **Cover** — client name, brand name, brief date, "Viral Content Strategy" title, brand-derived hero color
2. **Executive Summary** — 1 paragraph: the offer, who buys it, the desired action (CTA from Phase 0), the bet (what formats will dominate), expected output ([VIDEO_COUNT] videos + image pack), production timeline
3. **The Offer Profile** *(NEW — explicit, referenced throughout)* — card showing: what they sell + price + format · who buys (ICP descriptor) · the desired action / CTA · the tone direction. This is the foundation the rest of the brief is anchored to.
4. **The Trend Landscape** — table of trends pulled from research, each with: trend name, where it's winning (TikTok / IG / YouTube / podcasts), example brands using it, why it works
5. **Competitor Audit** — table of 5–10 competitor brands, format mix they're using, posting cadence, **example hook lines** they're using right now, **the gap** column (what they're NOT doing that we can own)
6. **Recommended Content Mix** — woven naturally, not as a config card. Show the format breakdown with counts AS A CONSEQUENCE of the trends the research surfaced. Use language like: "Based on what's actually winning this week in [niche] + what your competitors aren't doing, here's how the campaign breaks down…" Adjust counts per the user's chosen track (All 8 / AI only / Real-shot only).
7. **Production Track Choice** *(NEW)* — explicit table: which formats are in scope (based on user's Step A choice), which are AI-generated vs real-shot, and why. If user picked AI-only or Real-only, this section says so clearly.
8. **The Format Battle Cards** — one card per active format with: definition, why it wins for THIS offer + ICP combo, 3 concept seeds, example hook line, recommended posting cadence
9. **Hook Library** *(MAJOR EXPANSION)* — full Hook Library from Stage 1 Step 5 organized by the 6 categories: Curiosity / Pattern Interrupt / Pain-Named / Cost-Receipt / Funny-Podcast / Founder Confession. Each category gets 4–8 hooks listed verbatim, copy-pastable. If the user pre-selected favorites in Stage 1 Step 8, mark those with a ⭐.
10. **CTA Library** *(NEW)* — 8 CTAs matched to the Phase 0 CTA choice, copy-pastable, each tied to a specific desired action. Bias toward lead gen if the user picked form fill or booked call. Include 1–2 "friction-removal" variants ("no card needed," "30-second form," "no hard sell").
11. **Production Calendar** — date-by-date table for the campaign window: Date · Format · Production route · Concept · Hook used · CTA used · Where it posts (paid / organic / both)
12. **Paid vs Organic Distribution** — which videos go into Meta paid campaigns, which go to organic feed posts only, which run both. Default split: top 30% performance creatives → paid; everything → organic feed.
13. **Production Plan** — Stage 3 preview: AI batch order, shot list deliverables, image asset pack contents
14. **KPIs & Reporting** *(NEW)* — what success looks like for THIS campaign, anchored to the Phase 0 CTA. Lead-gen KPIs: CTR, CPM, **CPL**, **lead-to-call rate**, **show-up rate**, **close rate**, total qualified pipeline. Ecommerce KPIs: CTR, CPM, ROAS, CPA. Reporting cadence: weekly creative review, biweekly performance review.
15. **What Happens Next** — 4-step plain-English: (1) Client signs off on this brief, (2) AI videos generate in 24h (if AI track), (3) Real-shot scripts handed off to creator + filmed within 7 days (if real-shot track), (4) Everything scheduled to Meta + posted organic on approved dates
16. **Cost Note** — brief line: "Full cost breakdown — actual spend vs traditional production — delivered after Stage 5."

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
