# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an AI-powered idea management system built entirely on Claude Code slash commands and markdown files. The system helps users capture, evaluate, prioritize, and develop ideas using structured workflows and AI-powered scoring.

## Core Concepts

### Idea Lifecycle
Ideas flow through four states:
- **inbox/** - Newly captured ideas awaiting review
- **backlog/** - Scored and prioritized ideas waiting for action
- **active/** - Ideas currently being worked on (limit 1-3)
- **archive/** - Completed or abandoned ideas

### Scoring System
Each idea receives three independent scores (1-10 scale):
1. **Work Required** - Complexity and time needed (lower is better)
2. **Coolness Factor** - Innovation and excitement level (higher is better)
3. **Commercial Opportunity** - Market potential (higher is better)

**Composite Score Formula**: `(11 - Work) + Coolness + Commercial` (max 30)
- This formula rewards "quick wins" - low effort, high value ideas
- Quick Win Threshold: Composite > 20 AND Work < 5

### Idea File Format
Each idea is a markdown file with YAML frontmatter:
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
[One paragraph description]

## Problem/Opportunity
[What problem this solves]

## Solution/Approach
[High-level approach]

## Scores

### Work Required (1-10)
**Score:** 5/10
**Reasoning:** [2-3 sentences explaining the score]

### Coolness Factor (1-10)
**Score:** 8/10
**Reasoning:** [2-3 sentences explaining the score]

### Commercial Opportunity (1-10)
**Score:** 7/10
**Reasoning:** [2-3 sentences explaining the score]

### Composite Score
**Total:** 20/30
**Calculation:** (11 - 5) + 8 + 7 = 20

## Extensions
[Added by /iterate-idea command]

## Market Research
[Added by /market-research command]

## Next Steps
[Actionable items]

## Notes
[Freeform thoughts]
```

## Available Slash Commands

The system provides four main commands implemented as Claude Code skills:

### `/new-idea`
**Purpose**: Capture and score new ideas quickly

**Workflow**:
1. Gather idea information (title, summary, problem, solution, tags)
2. Ask 1-3 clarifying questions for accurate scoring
3. Score on all three dimensions using `.claude/prompts/scoring-framework.md`
4. Generate unique slug from title
5. Save to `ideas/inbox/[slug].md` with frontmatter and structured content

**Key Implementation Notes**:
- Be conversational and encouraging during capture
- Use scoring framework consistently for all ideas
- Create proper YAML frontmatter with all required fields
- Generate composite score automatically
- Provide clear reasoning for each score (2-3 sentences)

### `/list-ideas`
**Purpose**: Display all ideas in formatted table with sorting/filtering

**Arguments**:
- Sorting: `--sort-composite` (default), `--sort-work`, `--sort-coolness`, `--sort-commercial`
- Filtering: `--inbox`, `--backlog`, `--active`, `--archive`

**Workflow**:
1. Find all `ideas/**/*.md` files (exclude `.gitkeep`)
2. Parse frontmatter and scores from each file
3. Apply filters and sorting
4. Display as formatted table with 🌟 markers for quick wins
5. Show summary statistics

**Key Implementation Notes**:
- Handle missing scores gracefully with "-" placeholders
- Calculate composite if not present in file
- Quick win marker: Composite > 20 AND Work < 5
- Default sort: composite score descending

### `/iterate-idea`
**Purpose**: Deep dive on an idea with three extension modes

**Arguments**: `<idea-name>` (supports fuzzy search)

**Workflow**:
1. Find idea file by fuzzy matching name/slug
2. Present three modes:
   - **Build cool tool** - Implementation planning (MVP, tech stack, architecture, roadmap)
   - **Research/extend** - Problem space exploration (alternatives, validation, assumptions)
   - **Commercialize** - Business strategy (market sizing, business model, GTM, pricing)
3. Ask mode-specific questions
4. Generate comprehensive extension section
5. Re-score based on new insights
6. Append extension with timestamp to idea file
7. Update scores and composite

**Key Implementation Notes**:
- Each mode has specific question templates and output structure
- Extensions are additive - append, don't replace
- Re-scoring should reflect new learnings (can go up or down)
- Keep original scores in history

### `/market-research`
**Purpose**: Research existing solutions and market landscape using web search

**Arguments**: `<idea-name>` (supports fuzzy search)

**Workflow**:
1. Find idea file by fuzzy matching
2. Use WebSearch to find:
   - Direct competitors
   - Indirect alternatives
   - Market size and trends
   - Similar open source projects
3. Analyze findings and generate report covering:
   - Existing solutions (5-10 competitors)
   - Market analysis (size, growth, demand)
   - Competitive landscape (gaps, differentiation opportunities)
   - Risks and opportunities
4. Adjust commercial score if warranted
5. Append research section with timestamp to idea file

**Key Implementation Notes**:
- Use multiple search queries for comprehensive results
- Be objective about market reality vs. enthusiasm
- May lower commercial score if market is crowded
- Include links to competitors in report

## Scoring Framework

The scoring framework in `.claude/prompts/scoring-framework.md` defines detailed criteria for consistent evaluation. Key principles:

### Work Required (1-10)
- 1-2: Minimal (hours)
- 3-4: Light (1-2 days)
- 5-6: Moderate (weeks)
- 7-8: Significant (months)
- 9-10: Massive (year+)

Consider: development time, technical complexity, expertise needed, dependencies, research required

### Coolness Factor (1-10)
- 1-2: Boring (mundane)
- 3-4: Incremental (slight improvement)
- 5-6: Interesting (notably useful)
- 7-8: Novel (exciting innovation)
- 9-10: Revolutionary (paradigm-shifting)

Consider: novelty, excitement factor, creative use of technology, wow factor, personal interest

### Commercial Opportunity (1-10)
- 1-2: No market
- 3-4: Tiny niche (hundreds of users)
- 5-6: Small/medium market (thousands, $10K-$100K/year potential)
- 7-8: Large market (millions, $100K-$1M+/year)
- 9-10: Massive opportunity (billions, unicorn potential)

Consider: market size, pain intensity, willingness to pay, monetization clarity, competition, growth trends

### Scoring Best Practices
- Score each dimension independently
- Be realistic, not optimistic
- Use full scale (most ideas are 4-7 on each dimension)
- Provide 2-3 sentence reasoning for each score
- Don't let one dimension influence others
- Re-score when new information is learned

## Common Workflows

### Morning Capture
User runs `/new-idea` multiple times to quickly capture ideas without friction. System asks questions, scores automatically, saves to inbox.

### Weekly Review
User runs `/list-ideas --inbox` to see new ideas, then `/list-ideas --sort-composite` to identify top priorities and quick wins.

### Pre-Development Validation
1. Run `/market-research <idea>` to check competition
2. Run `/iterate-idea <idea>` with "Research/extend" to validate assumptions
3. Run `/iterate-idea <idea>` with "Build cool tool" to create implementation plan

## File Organization

```
ideas/
├── inbox/      # New ideas (status: inbox)
├── backlog/    # Scored, waiting (status: backlog)
├── active/     # Working on (status: active)
└── archive/    # Done/abandoned (status: archive)

.claude/
├── prompts/
│   └── scoring-framework.md    # Detailed scoring criteria
└── skills/
    ├── new-idea.prompt.md      # /new-idea implementation
    ├── list-ideas.prompt.md    # /list-ideas implementation
    ├── iterate-idea.prompt.md  # /iterate-idea implementation
    └── market-research.prompt.md # /market-research implementation
```

## Architecture Notes

### Skill Implementation Pattern
Each slash command is implemented as a `.prompt.md` file with:
- YAML frontmatter (name, description)
- Step-by-step workflow instructions
- Question templates for user interaction
- Output format specifications
- Error handling guidance

### Fuzzy Idea Matching
When finding ideas by name:
1. Try exact slug match first
2. Try partial slug match (contains query)
3. Try title match (case insensitive)
4. If multiple matches, ask user to clarify
5. If no matches, list available ideas

### State Management
- Status field in frontmatter drives organization
- Files can live in any directory (status is source of truth)
- Best practice: keep file location synced with status

### Scoring Consistency
- All scoring uses the same framework from `scoring-framework.md`
- Reasoning must be included for each score
- Composite calculation must be explicit: `(11 - Work) + Coolness + Commercial`
- Re-scoring preserves history in Extensions sections

## Design Philosophy

1. **Capture quickly** - Minimal friction during idea capture
2. **AI-powered evaluation** - Consistent, calibrated scoring
3. **Simple storage** - Just markdown files, easy to search/edit
4. **Guided workflows** - Structured prompts for different development modes
5. **Progressive refinement** - Capture → Score → Extend → Research → Build
6. **Quick wins focus** - Formula optimized to surface low-effort, high-value ideas

## When Working on Skills

### Adding New Commands
1. Create `.claude/skills/new-command.prompt.md`
2. Include YAML frontmatter with name and description
3. Write step-by-step workflow with clear instructions
4. Document expected inputs and outputs
5. Test with various inputs and edge cases

### Modifying Scoring
- Always reference `scoring-framework.md` for consistency
- Update framework if criteria change
- Re-score existing ideas if framework changes significantly
- Keep historical scores when re-scoring

### Extending Idea Format
- Preserve backward compatibility with existing ideas
- Make new fields optional
- Document new sections in this file
- Update skill prompts to generate new format
