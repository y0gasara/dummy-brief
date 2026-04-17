---
name: dummy-brief-creator
description: >
  Generates a realistic, fictional business project brief for self-learners who have a dataset
  and want to build a meaningful data analytics portfolio project (Power BI, Tableau, Looker,
  Python, etc.). Use this skill whenever a user shares a dataset, CSV columns, or data headers
  and wants to: build a dashboard, do an analysis project, create a portfolio piece, practice
  data analytics, or avoid "blindly analyzing data." Also trigger when users say things like
  "I have a dataset and want to build something", "help me make a project brief", "give me a
  business context for this data", or "I want my dashboard to feel like a real project."
  The skill asks targeted clarifying questions about the data and desired scope, then produces
  a polished rendered visual brief with a fictional company, stakeholder, business goals, KPIs
  mapped to actual dataset columns, and dashboard page specifications — all grounded in what
  the data can actually support.
---

# Dummy Brief Creator

Turns a raw dataset into a realistic fictional project brief — so learners build dashboards with
business purpose, not just charts.

## The Problem This Solves

Most learners get a Kaggle dataset and jump straight into building visuals with no business
context. The result: technically correct but strategically hollow dashboards. This skill
creates a believable fictional business scenario around the user's actual data, forcing them
to think like an analyst responding to real stakeholder needs.

---

## Workflow

### Step 1 — Receive the data context

The user will provide one of:
- Full CSV paste (with headers + sample rows)
- Just the column headers
- A description of the dataset

**Extract from this:**
- Column names and inferred data types
- Likely domain/industry (sales, health, finance, sports, etc.)
- What's available vs. what's missing (e.g. no date column = no time-series KPIs)

Do NOT generate the brief yet. Move to Step 2.

---

### Step 2 — Ask clarifying questions (always do this)

Ask the following using the `ask_user_input_v0` tool. Never skip this step — the brief
quality depends entirely on these answers. Keep it to 2–3 questions max per round.

**Required questions to cover (split across 1–2 tool calls):**

**Round 1 — Business framing:**
- What tool will they build with? (Power BI / Tableau / Python / other)
- What type of fictional company fits the data? Offer 3–4 plausible options based on the domain
- What is the main business goal? (offer options: monitor performance, understand trends,
  identify opportunities, support strategic decisions, or "all of the above")

**Round 2 — Dashboard scope:**
- How many dashboard pages? (1 page / 2 pages: Executive + Detail / let me decide)
- Any columns they've already dropped or plan to exclude?

**Data-specific follow-ups (ask only when relevant):**
- If there's a numeric "condition" or "rating" column: should it be kept as numbers or remapped
  to labels?
- If there's a date column: should time-based trends be a primary focus?
- If there are ID/key columns: confirm they'll be excluded from visuals

After clarifying questions are answered, move to Step 3.

---

### Step 3 — Generate the brief as a rendered visual widget

Call `visualize:read_me` with `["mockup"]`, then call `visualize:show_widget` to render
the full brief as a polished HTML widget.

**The brief must include all of these sections:**

#### 1. Header
- Tag: "Project Brief · [Tool Name]"
- Version tag if this is a revision (e.g. "v2 — schema-adjusted")
- Fictional project/dashboard name (make it sound real, e.g. "DriveIQ Performance Dashboard")
- Subtitle describing the dashboard's focus
- Meta row: Requested by (fictional name + title), Company (fictional), Pages, Data source, Refresh cadence

#### 2. Business background (2 short paragraphs)
- What the fictional company does
- What business pain point this dashboard solves
- Write from the stakeholder's perspective, not a data analyst's

#### 3. Available data columns (schema table)
Render as a table with columns: Column name | Type | Notes | Status

Status badges:
- Green "in use" — column directly powers a KPI or slicer
- Gray strikethrough "dropped" — removed during data cleaning
- Gray strikethrough "out of scope" — present but not used in this brief

Add a note box (amber left-border) for any remapping decisions (e.g. condition 1–5 → labels).

#### 4. Business goals (bullet list)
5 goals written as business pain points, not technical tasks.
Example: "Understand which vehicle brands generate the most revenue" — NOT "plot make vs sellingprice"

#### 5. Primary audience (pills)
2–4 fictional roles. Match to the company type. Remove any role that can't be served by
the available data.

#### 6. KPIs & metrics (card grid)
Each card shows:
- KPI name (business language)
- Short description (what question it answers)
- Source columns (e.g. "← make + sellingprice") in a blue tinted label

**Rules for KPI selection:**
- Only propose KPIs that can be built from the actual columns in the dataset
- If the user excluded a column, do not use it
- Flag if a commonly expected KPI (e.g. time trend) is impossible due to missing data
- Aim for 8–12 KPIs total across the dashboard

#### 7. Dashboard page specs
One card per page. Each card includes:
- Page number badge (blue for page 1, green for page 2+)
- Page title and short description (who is this page for, what question does it answer)
- Visual tags: list of chart types and slicers as pills

**Page logic:**
- 1 page: combine executive KPIs + key detail visuals
- 2 pages: Page 1 = leadership overview (answer "how are we doing?" in 30 seconds),
  Page 2 = operational detail (deeper slices for analysts/managers)
- 3+ pages: break by theme (e.g. Sales / Pricing / Geography)

#### 8. Success criteria (short paragraph)
What does "done" look like? Write it as: "The dashboard is successful when [role] can answer
[specific questions] without opening a spreadsheet."

---

## Visual styling guide

Use these CSS patterns consistently across all brief widgets:

```
Colors:
- Page 1 badge: background #E6F1FB, color #0C447C
- Page 2 badge: background #EAF3DE, color #3B6D11
- KPI source label: color #378ADD (blue, small, no background)
- Note box: background #FAEEDA, border-left 3px solid #EF9F27, color #633806
- "in use" badge: background #EAF3DE, color #3B6D11
- "dropped/out of scope": background var(--color-background-secondary), strikethrough

Typography:
- Section labels: 11px, uppercase, letter-spacing 0.08em, var(--color-text-tertiary)
- Card titles: 13px, font-weight 500
- Body text: 14px, line-height 1.75, var(--color-text-secondary)
- Meta labels: 11px uppercase, meta values: 13px font-weight 500

Layout:
- KPI grid: repeat(auto-fill, minmax(220px, 1fr))
- Dividers: 0.5px solid var(--color-border-tertiary)
- All containers: transparent background (let host provide bg)
```

---

## Handling revisions

If the user shares more data context after the brief is generated (e.g. "I dropped the seller
column" or "I actually have MMR data too"), update the brief:
- Add a "v2 — schema-adjusted" version tag to the header
- Update the schema table status badges
- Add/remove KPIs accordingly
- Update audience if a removed column was their primary data source
- Re-render the full widget (do not just describe the changes in text)

---

## Domain examples

The skill works across any dataset domain. Example fictional company types by domain:

| Dataset domain | Fictional company types |
|---|---|
| Used car sales | Dealership chain, auto marketplace, fleet management company |
| E-commerce | D2C brand, marketplace platform, logistics company |
| HR / employee data | Mid-size tech company, consulting firm, staffing agency |
| Healthcare | Hospital network, health insurance company, wellness app |
| Sports / ATP tennis | Sports analytics firm, media company, betting platform |
| Financial transactions | Retail bank, fintech startup, investment firm |
| Retail / POS | Chain retailer, franchise operator, FMCG brand |

When proposing fictional company options in Step 2, offer 3–4 from this list adapted to the
user's actual dataset. Always make the company name sound real (e.g. "AutoNation Central",
"Meridian Health Group", "Apex Retail Partners").

---

## What NOT to do

- Do not generate the brief before asking clarifying questions
- Do not propose KPIs that require columns the user has dropped
- Do not use technical column names in business goal descriptions
- Do not include MMR, ID, or key columns in KPIs unless explicitly asked
- Do not output the brief as markdown — always render as a visual widget
- Do not make the fictional company too exotic — keep it believable for a portfolio reviewer
