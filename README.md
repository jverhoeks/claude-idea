# Claude Idea Management System

A simple, AI-powered idea management system using Claude and markdown files.

## Philosophy

- **Capture ideas quickly** without friction - just use `/new-idea`
- **Let AI help** evaluate and extend ideas with intelligent scoring
- **Keep it simple** - just markdown files and Claude slash commands
- **Organize naturally** using directories and scores

## Quick Start

```bash
/new-idea               # Capture and score a new idea
/list-ideas             # View all ideas with scores
/iterate-idea <name>    # Extend and improve an idea
/market-research <name> # Research existing solutions
```

## Directory Structure

```
ideas/
├── inbox/      # New ideas land here (auto-scored)
├── backlog/    # Scored ideas waiting for action
├── active/     # Currently working on these
└── archive/    # Completed or abandoned
```

## Scoring System

Each idea is scored on three dimensions (1-10 scale):

### Work Required
- **1-3**: Hours to days, simple implementation
- **4-6**: Weeks, moderate complexity
- **7-9**: Months, significant effort
- **10**: Year+, massive undertaking

### Coolness Factor
- **1-3**: Mundane, incremental
- **4-6**: Interesting, useful
- **7-9**: Novel, exciting
- **10**: Revolutionary, groundbreaking

### Commercial Opportunity
- **1-3**: Niche or no market
- **4-6**: Small to medium market
- **7-9**: Large market, clear monetization
- **10**: Massive market opportunity

### Composite Score

**Formula**: `(11 - Work) + Coolness + Commercial` (max 30)

This formula rewards **quick wins** - ideas with low effort and high value.

**Quick Win Threshold**: Composite > 20 AND Work < 5

## Available Commands

### `/new-idea` - Capture and Score New Idea

Guides you through capturing a new idea with:
- Title and description
- Clarifying questions
- Auto-scoring on all three dimensions
- Saves to `ideas/inbox/` with AI reasoning

**Example**:
```
/new-idea
> What's the title? AI Recipe Generator
> Tell me more... [describes idea]
> [AI asks clarifying questions]
✅ Idea created with scores!
```

### `/list-ideas` - View All Ideas

Display all ideas in a table with sorting and filtering:

**Sorting options**:
- `--sort-work` - Lowest to highest work
- `--sort-coolness` - Highest coolness first
- `--sort-commercial` - Highest commercial first
- `--sort-composite` - Highest composite (default)

**Filtering options**:
- `--inbox` - Only inbox ideas
- `--backlog` - Only backlog ideas
- `--active` - Only active ideas
- `--archive` - Only archived ideas

**Example**:
```
/list-ideas --sort-composite

| Title                    | Work | Cool | Comm | Total | Status  |
|--------------------------|------|------|------|-------|---------|
| 🌟 Browser Tab Manager   |  3   |  8   |  9   |  24   | backlog |
| 🌟 Weekend Logger        |  2   |  7   |  8   |  23   | backlog |
| AI Recipe Generator      |  7   |  8   |  7   |  15   | inbox   |

🌟 = Quick win (high value, low effort)
```

### `/iterate-idea` - Extend and Improve

Opens an idea and helps you extend it with three modes:

**Build cool tool** - Implementation focus
- Tech stack recommendations
- MVP feature planning
- Architecture design
- Development roadmap

**Research/extend** - Deep dive
- Problem space exploration
- Alternative solutions
- Related work and references
- Validation approaches

**Commercialize** - Business strategy
- Business model options
- Market sizing
- Go-to-market strategy
- Revenue models

After extension, the idea is re-scored based on new insights.

**Example**:
```
/iterate-idea recipe-generator
> How to extend? [Choose: build/research/commercialize]
> Build cool tool
> [AI asks implementation questions]
✅ Extension added, scores updated!
```

### `/market-research` - Research Existing Solutions

Uses AI to search for and analyze:
- Existing products/services
- Competitors and alternatives
- Market size and trends
- Similar open source projects

Generates a market analysis report and may adjust the commercial score based on findings.

**Example**:
```
/market-research recipe-generator
📊 Found 5 competitors, $5B market
✅ Research report added to idea file
```

## Workflows

### Morning Idea Capture

```
/new-idea
[Capture idea 1]

/new-idea
[Capture idea 2]

/list-ideas --inbox
[Review what you've captured]
```

### Weekly Review

```
/list-ideas --sort-composite
[Identify top ideas and quick wins]

/iterate-idea <top-idea>
[Deep dive on most promising idea]
```

### Pre-Development

```
/market-research <idea-name>
[Research competition]

/iterate-idea <idea-name>
> Build cool tool
[Create implementation plan]
```

## Idea File Format

Each idea is stored as a markdown file with frontmatter:

```markdown
---
id: idea-slug
title: Idea Title
created: 2026-01-04
updated: 2026-01-04
status: inbox
tags: [software, productivity]
---

# Idea Title

## Summary
One-paragraph description

## Problem/Opportunity
What problem does this solve?

## Solution/Approach
High-level approach

## Scores

### Work Required (1-10)
**Score:** 5/10
**Reasoning:** Moderate complexity...

### Coolness Factor (1-10)
**Score:** 8/10
**Reasoning:** Novel approach...

### Commercial Opportunity (1-10)
**Score:** 7/10
**Reasoning:** Large addressable market...

### Composite Score
**Total:** 15/30
**Calculation:** (11 - 5) + 8 + 7 = 15

## Extensions

### Extension 2026-01-04
Implementation plan with tech stack...

## Market Research

### Market Research 2026-01-04
Competitive analysis...

## Next Steps
- Validate assumption X
- Build MVP feature Y
- Research technology Z

## Notes
Freeform thoughts and updates
```

## Best Practices

1. **Review ideas weekly** - Keep the system fresh
2. **Move ideas as you work** - Update status (inbox → backlog → active → archive)
3. **Keep inbox lean** - Score and move ideas regularly
4. **Tag consistently** - Makes filtering easier
5. **Trust AI scores** - They're calibrated for consistency
6. **Archive completed ideas** - Document outcomes and learnings
7. **Focus on quick wins** - High composite score + low work = great ROI

## Tips

- **Capture fast**: Don't overthink during `/new-idea` - you can always `/iterate-idea` later
- **Use filters**: `/list-ideas --inbox` to see just new ideas
- **Sort by work**: `/list-ideas --sort-work` to find easiest ideas
- **Research before building**: `/market-research` can save you from building what exists
- **Iterate multiple times**: Each `/iterate-idea` session can explore different angles
- **Re-score after learning**: Scores update as you gain insights

## Success Metrics

- **Week 1**: Capture 5+ ideas, test all commands
- **Month 1**: 15+ ideas, identify 2-3 quick wins, start 1 idea
- **Ongoing**: Weekly capture, monthly reviews, track completed vs abandoned

## System Evolution

As you use the system:
- Scores become more calibrated to your context
- You'll develop intuition for what scores mean
- Patterns emerge (e.g., you prefer coolness over commercial)
- You can add custom commands for your workflow

## Future Enhancements

Planned additions:
- `/move-idea` - Explicit status changes
- `/compare-ideas` - Side-by-side comparison
- `/archive-idea` - Archive with learnings
- `/review-week` - Weekly review automation
- `/export-ideas` - Export to CSV/JSON

## Questions?

Use Claude to ask questions about the system!
- "How should I score X?"
- "What makes a good quick win?"
- "Should I work on idea A or B?"
- "How can I improve my idea capture process?"

---

**Built with Claude** - AI-powered idea management
