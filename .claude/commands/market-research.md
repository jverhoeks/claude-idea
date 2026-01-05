---
description: Research existing solutions and market opportunities for an idea
---

# Market Research

You are helping the user research the market for one of their ideas using web searches. Follow this workflow:

## Step 1: Find the Idea

Search for matching idea files using Glob tool: `ideas/**/*[search-term]*.md`
- If multiple matches: Ask user to select
- If one match: Confirm and proceed
- If no match: End workflow

## Step 2: Read and Understand the Idea

Read the idea file and extract:
- Title, Summary, Problem/Opportunity, Solution/Approach
- Current commercial score from:
  - New format: `scores.commercial` in frontmatter
  - Old format: "### Commercial Opportunity" section in body
- Formulate search queries based on content

## Step 3: Conduct Market Research

Use WebSearch tool to research (conduct 3-5 searches):

**Search 1: Existing Products/Services**
- Query: `[idea keywords] product | service | app 2026`
- Goal: Find direct competitors

**Search 2: Market Size and Trends**
- Query: `[industry] market size | trends 2026`
- Goal: Understand market size and growth

**Search 3: Similar Startups/Projects**
- Query: `[keywords] startup | company | open source`
- Goal: Find companies in the space

**Search 4: User Discussions/Pain Points**
- Query: `[problem] reddit | forum site:reddit.com`
- Goal: Understand demand

**Search 5: Industry Analysis (Optional)**
- Query: `[industry] analysis | competitive landscape`

## Step 4: Analyze Findings

Synthesize research into:

**A. Existing Solutions** (5-10 products)
- Name, Description, Scale, Strengths, Weaknesses, Pricing

**B. Market Analysis**
- Market Size (TAM estimate)
- Growth Rate
- Key Trends
- Demand Signals

**C. Competitive Landscape**
- Competition Level
- Market Leaders
- Gaps in existing solutions
- Differentiation Opportunities

**D. Risks and Challenges**
- Market, Competition, Timing, Execution risks

**E. Opportunities**
- Underserved Segments
- Emerging Needs
- Market Gaps

## Step 5: Generate Market Research Report

Create comprehensive markdown report with:
- Executive Summary
- Existing Solutions table
- Market Analysis
- Competitive Landscape
- Risks and Challenges
- Opportunities and Recommendations
- Key Insights (✅ Positives, ⚠️ Yellow Flags, 🚩 Red Flags)
- References with URLs
- Overall Market Attractiveness
- Recommendation (Pursue/Caution/Pivot/Abandon)

## Step 6: Reassess Commercial Score

Based on research, update commercial score if warranted:
- Bigger opportunity → Increase score
- Smaller opportunity → Decrease score
- Confirms assessment → Keep same

Update reasoning to reference research findings.

## Step 7: Update the Idea File

1. Update frontmatter:
   - If commercial score changed:
     - Update `scores.commercial` with new value
     - Update `scores.composite` with new calculation: `(11 - work) + coolness + commercial`
   - Update `last_reviewed: YYYY-MM-DD` to today's date
   - Keep all other frontmatter fields unchanged

2. Add market research report to "## Market Research" section in body
3. If commercial score changed, update "## Scores" section in body
4. Keep previous research (append, don't overwrite)

## Step 8: Display Summary

```
✅ Market research completed for [Title]

📊 Key Findings:
   - Existing solutions: [X] competitors
   - Market size: [Estimate]
   - Competition level: [Crowded/Moderate/Few]
   - Market attractiveness: [High/Medium/Low]

🎯 Recommendation: [Pursue/Caution/Pivot/Abandon]

[If score changed:]
📈 Commercial Score: [OLD] → [NEW]/10
   Composite: [OLD] → [NEW]/30

Top insights:
- [Insight 1]
- [Insight 2]
- [Insight 3]

Full report added to: ideas/[dir]/[filename].md
```

## Important Guidelines

- Conduct actual searches, don't make up data
- Be honest about market reality
- Cite sources with URLs
- Prioritize recent data (2024-2026)
- Show both opportunities and risks
- Only change commercial score if research clearly warrants it

Ready to research the market! Which idea would you like me to research?
