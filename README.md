# Dummy Brief Creator — A Claude Skill

A Claude skill that transforms your raw dataset into a realistic, fictional project brief — so you build dashboards with a real business purpose, not just charts.

---

## The Problem

You download a dataset from Kaggle. You open Power BI, Tableau, or a Jupyter notebook. You start building visuals. And somewhere around the third bar chart, you realize you have no idea what question you're actually answering — or who you're answering it for.

The result is a technically correct dashboard that means nothing to anyone, including a future employer reviewing your portfolio.

**This skill fixes that.** Before you touch a single visual, it creates a fictional — but realistic — business scenario around your actual data, complete with a stakeholder, a company, a business problem, and KPIs that map directly to the columns you have.

---

## What It Does

Paste your dataset headers (or a few sample rows) into Claude. The skill will:

1. Read your columns and understand what kind of data you have
2. Ask you a few targeted questions — what tool are you using, what company type fits the data, how many dashboard pages you want
3. Generate a polished project brief rendered as a visual document inside Claude

**The brief includes:**
- A fictional company name, stakeholder, and business background
- A schema table showing every column with its status (in use / dropped / out of scope)
- Business goals written the way a real stakeholder would describe them
- 8–12 KPIs, each mapped to the actual columns that power them
- Page-by-page dashboard specs with suggested chart types and slicers
- A success criteria statement

If you update your data later — drop a column, change your scope — just tell Claude and it re-renders an updated brief automatically.

---

## Supported Dataset Domains

The skill works across any dataset type. Here are some examples of the fictional companies it can generate:

| Dataset Type | Example Fictional Companies |
|---|---|
| Used car sales | Dealership chain, auto marketplace, fleet management company |
| E-commerce / orders | D2C brand, marketplace platform, logistics company |
| HR / employee data | Tech company, consulting firm, staffing agency |
| Healthcare | Hospital network, health insurance company, wellness app |
| Sports statistics | Sports analytics firm, media company, betting platform |
| Financial transactions | Retail bank, fintech startup, investment firm |
| Retail / point of sale | Chain retailer, franchise operator, FMCG brand |

Compatible with Power BI, Tableau, Looker, Python (matplotlib / seaborn / plotly), and more.

---

## How to Install

This skill is a single `SKILL.md` file that teaches Claude a specific workflow. Installation takes less than a minute.

1. Click on `SKILL.md` in this repository
2. Click the **Download raw file** button to download the file
3. Open [claude.ai](https://claude.ai) and go to **Customize → Skills**
4. Click **Create Skill → Upload a skill** and select the `SKILL.md` you just downloaded

---

## How to Use

Once the skill is installed, start a new conversation and share your dataset by uploading the CSV or simply copying the columns header from the dataset:

```
I have a dataset I want to analyze and build a dashboard on. Here are my columns:

year, make, model, trim, body, transmission, state, condition, odometer, color, interior, sellingprice, saledate

Create me the dummy brief.
```

Claude will ask a few clarifying questions, then generate the full project brief.

**Other prompts that trigger the skill:**
- *"I downloaded a sales dataset from Kaggle and want to build a Power BI dashboard"*
- *"Help me create a project brief for this data"*
- *"I don't want to blindly analyze this — give me a business context first"*
- *"Here are my CSV headers, what kind of dashboard should I build?"*

---

## Example Output

Here is the kind of brief the skill generates, built from a real sales dataset:

**StoreWatch Regional Performance Dashboard**
*Real-time sales monitoring and driver analysis across regional store network — Executive & Operations View*

> Requested by Sarah Chen, VP Operations · RegionalMart Holdings (fictional) · 2 pages · Weekly refresh

The brief includes a full schema table, 12 KPIs each mapped to actual dataset columns, Executive and Detail page specifications, and a clear success criteria statement — all rendered as a clean visual document inside Claude.

**[View the Live Interactive Example here](https://claude.ai/public/artifacts/4c667385-8658-470e-a61e-bbb3aa72bf52)**

<img width="1133" height="897" alt="Portfolio Brief Creator Output Example" src="https://github.com/user-attachments/assets/b305af0a-cad2-465d-a743-0a35aa9059e5" />

---

## Why This Matters for Your Portfolio

Most data portfolios are full of technically correct dashboards with no business story behind them. A dashboard built against a proper brief immediately signals to a reviewer that you understand the difference between making charts and doing analysis.

It also forces you to think through the right questions before you build:
- Who is this dashboard for?
- What decision does it help them make?
- What does the data actually support — and what am I assuming?

Those are the questions that separate a data analyst from someone who just knows the tools.

---

## Built By

[@y0gasara](https://github.com/y0gasara) — this skill came out of a real portfolio-building process. The goal was to stop producing hollow dashboards and start thinking like a stakeholder first, analyst second.

If you find it useful, a ⭐ on the repo is appreciated. If you build something with it, feel free to share.

---

## Contributing

Found a dataset domain that doesn't work well? Have a suggestion for a new company type or KPI pattern? Open an issue or a pull request. The more domains this covers, the more useful it becomes for the community.

---

## License

MIT — free to use, remix, and build on.
