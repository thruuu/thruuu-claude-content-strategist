# thruuu Content Strategist

Turn keyword cluster exports from [thruuu](https://thruuu.com) into prioritized content strategies using Claude Code.

This is not a spreadsheet formula. It's an AI strategist that reasons about your business, your existing content, and your competition to decide what to create, what to optimize, and what to skip.

---

## How It Works

1. You run a keyword clustering project in [thruuu](https://thruuu.com) and download the report
2. You drop the export into the `input/` folder
3. You run Claude Code in this folder
4. Claude learns your business, parses every cluster, and reasons through each one
5. The finished strategy lands in `output/` as a markdown report and an Excel file

The quality of the output depends on the clustering data and the business context you provide. The better both are, the sharper the strategy.

---

## What's in This Repo

| File / Folder | Purpose |
|---|---|
| `CLAUDE.md` | The agent brain. Claude reads this automatically on startup. Defines the full strategy workflow. |
| `input/` | Drop your downloaded thruuu cluster exports here. |
| `input/processed/` | Completed files are moved here after processing. |
| `output/` | Claude saves strategy reports (.md) and spreadsheets (.xlsx) here. |
| `domains/` | Saved business profiles — one per domain, reused across runs. |

---

## Setup

### 1. Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

You need Node.js 18+ and an Anthropic API key. Full installation guide: [docs.anthropic.com/claude-code](https://docs.anthropic.com/en/docs/claude-code/getting-started)

### 2. Clone this repo

```bash
git clone https://github.com/thruuu/thruuu-claude-content-strategist.git
cd thruuu-claude-content-strategist
```

### 3. Run Claude Code

```bash
claude
```

Claude will create any missing folders automatically. No manual setup needed.

---

## First Run

On first run, Claude will read the Info tab from your export to identify the domain, then check for an existing business profile in `domains/`. Since you don't have one yet, it will run a short interview:

- What does your business do?
- What are your core products or features?
- Who is your target audience?
- What are your content goals?

It also runs a `site:` search to understand your existing content footprint. This takes about 2 minutes and is saved to `domains/` so you never repeat it for the same domain.

---

## Running Your First Strategy

### Step 1 — Generate your cluster export in thruuu

Go to your thruuu account, open a keyword clustering project, and click **Download Report**.

Don't have a thruuu account? [Start for free at thruuu.com](https://thruuu.com)

For a walkthrough of the clustering process:

- [thruuu Keyword Clustering Tool](https://thruuu.com/keyword-clustering-tool) — overview and features
- [How to Create Topic Clusters with thruuu](https://thruuu.com/learn/create-topic-cluster-tool/) — step-by-step guide
- [Video tutorial](https://www.youtube.com/watch?v=W1tZHGWgzog) — full walkthrough

### Step 2 — Drop the file in the input folder

```
thruuu-claude-content-strategist/
└── input/
    └── your-cluster-export.xlsx
```

### Step 3 — Tell Claude how many pieces you want

Claude will ask two questions:

- How many content pieces do you want in this plan? (20 / 50 / 100)
- How many pieces can you produce per week?

### Step 4 — Wait for the strategy

Claude will:

- Parse every cluster from the Topic Clusters tab
- Read the Competitors tab for competitive context
- Flag pages that rank for too many different topics
- Reason through each cluster: action, format, priority
- Generate a content plan, calendar, and AIO monitoring list
- Save the output to `output/` as both .md and .xlsx
- Move the input file to `input/processed/`

---

## What Claude Decides For Each Cluster

| Decision | How it reasons |
|---|---|
| **Action** | Create, optimize, or skip — based on whether the existing page actually matches the cluster's intent, not just whether a URL exists. |
| **Format** | Article, video, forum engagement, free tool — based on SERP feature data (video %, forum %), not assumptions. |
| **Priority** | P1 / P2 / P3 — weighted by product-market fit, volume, competition, and existing coverage. |

---

## Example

The `domains/` folder includes an ActiveCampaign example. Here's what Claude found from 273 keyword clusters:

> Their homepage ranks at position 29 for "marketing automation for startups." Startups are their core audience, but they land on a generic page that says nothing about them.

> Users searching "HubSpot vs Mailchimp" are exactly ActiveCampaign's audience. But there's zero content capturing them.

> Their lead nurturing blog post sits at position 18. One optimization effort lifts 5 related clusters at the same time.

The full strategy output is in `output/` as a reference.

---

## What This Is Not

- It does not replace analyzing clusters in thruuu. The next step after running this is to open each priority cluster in thruuu, review the competing content, and create a content brief.
- It does not generate content. It tells you what to create and why. Once your plan is ready, use [thruuu Claude Writer](https://github.com/thruuu/thruuu-claude-writer) to draft articles from thruuu content briefs — [see how it works](https://thruuu.com/blog/write-seo-content-with-claude/).
- It does not invent topics. It works strictly from the data in your export.

---

## About thruuu

[thruuu](https://thruuu.com) is one of the most comprehensive keyword clustering and SERP analysis platforms available. It clusters keywords by actual SERP similarity — not just semantic guessing — so your topic groups reflect how Google really organizes search results.

Beyond clustering, thruuu gives you deep SERP analysis (up to 100 results), content briefs, AI Overview monitoring, and SERP feature breakdowns (video, forum, AIO, PAA) that most tools don't surface. It's the data layer that makes this entire workflow possible.

[Create a free thruuu account](https://app.thruuu.com/create-account) — you can cluster up to 500 keywords without spending a dime.

---

## License

MIT — use freely, adapt as needed, attribution appreciated.
