# Install Guide — Content Factory

Full setup for the Content Factory skill, including the MCP servers it integrates with.

## 1. Install the skill

Pick one of the following.

### Option A — Direct clone into your Claude Code skills folder

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/jbrazy480/content-factory.git ~/.claude/skills/content-factory
```

Restart Claude Code (or open a new chat). The skill registers automatically.

### Option B — Clone anywhere, symlink in

```bash
git clone https://github.com/jbrazy480/content-factory.git
ln -s "$(pwd)/content-factory" ~/.claude/skills/content-factory
```

This is the cleanest setup if you want the skill in your dev folder (for hacking on it) while still being live in Claude.

### Update later

```bash
cd ~/.claude/skills/content-factory && git pull
```

### Verify it's loaded

Start a new Claude Code session and run `/content-factory`. If the skill appears in the available-skills list, you're set.

---

## 2. Install Higgsfield MCP (for Stage 3 — AI video generation)

The skill uses Higgsfield Marketing Studio to render the AI video batches and the static image asset pack.

### Hosted Higgsfield MCP (via claude.ai)

If you're on [claude.ai](https://claude.ai), the Higgsfield MCP server is available as a one-click integration:

1. Open Claude → **Settings** → **Connectors**
2. Search for **Higgsfield**
3. Click **Connect** and authenticate with your Higgsfield account
4. Verify the connection — the skill checks this in onboarding (Question A)

### Self-hosted Higgsfield MCP (Claude Code CLI)

If you're running Claude Code locally and want to wire your own Higgsfield workspace, check Higgsfield's docs for the latest MCP server endpoint. You'll need:

- A Higgsfield account on the **Creator**, **Team**, or **Pro** plan
- API access enabled
- Credits available in your workspace (the skill reports actual spend in Stage 5)

### Credit budget guidance

| Plan | Typical rate | Recommended budget per 50-video campaign |
|---|---|---|
| Creator | ≈ $0.02 / credit | $30–60 |
| Team / Pro | ≈ $0.01–0.005 / credit | $15–40 |

Stage 5's cost report pulls actual spend via the `transactions` API, so the report shows your real number — these are estimates for budgeting.

### Skipping Higgsfield

If you don't have a Higgsfield account, pick **"Skip — brief only"** in onboarding (Question A). Stages 1 and 2 still run end to end and produce the Client Strategy Brief without any AI generation.

---

## 3. Install Meta Ads MCP (for Stage 4 — scheduling)

Stage 4 schedules the paid AI creatives directly to Meta Ads (Facebook + Instagram).

### Hosted Meta Ads MCP (via claude.ai)

1. Open Claude → **Settings** → **Connectors**
2. Search for **Meta Ads** or **Facebook Ads**
3. Click **Connect** and authenticate with your Meta Business account
4. Grant access to the ad accounts you want to schedule into

### Skipping live scheduling

If you don't want live Meta scheduling (or you're handing off to a media buyer), pick **"Skip live scheduling — export the calendar instead"** in Stage 4. The skill exports a CSV calendar with every video, image, caption, and posting date — your media buyer can paste it into Ads Manager directly.

---

## 4. (Optional) GPT Image 2 access

The image asset pack uses Higgsfield's `generate_image` tool with `model: "gpt_image_2"`. This is metered against your Higgsfield credit balance — no separate OpenAI key needed. If your Higgsfield workspace has GPT Image 2 enabled, you're set.

---

## 5. Outputs folder

Every deliverable (HTML brief, real-shot guide, image pack, cost report, calendars) gets saved to:

```
/mnt/user-data/outputs/
```

If you're running Claude Code locally rather than in the hosted environment, the skill will adapt and save to your current working directory. The full path is announced in each stage's confirmation message.

---

## Troubleshooting

### Skill doesn't appear in the available-skills list

- Verify the folder is at `~/.claude/skills/content-factory/` (or symlinked there)
- Verify `SKILL.md` exists in the root of that folder
- Restart Claude Code

### Higgsfield generation fails with "No preset avatars"

- Confirm your Higgsfield plan has access to preset Avatars (Marketing Studio)
- The skill warns once and falls back to random faces; for campaign consistency, upgrade or use a Team workspace with preset library access

### `generate_video` defaults everything to UGC even when the brief says Product Review

The skill passes the title-case `mode` value on every call to prevent this. If you're seeing it, you may be running an older copy — `git pull` to update.

### Meta Ads MCP throws auth errors

- Re-authenticate in Settings → Connectors
- Confirm the Meta Business account has the ad accounts you're trying to schedule into
- For pages, your account needs `ads_management` + `ads_read` scopes

---

## Get help

- Issues: [github.com/jbrazy480/content-factory/issues](https://github.com/jbrazy480/content-factory/issues)
- Built by [MetaTech AI](https://metatech.ai)
