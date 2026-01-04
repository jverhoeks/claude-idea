# Usage Guide

Welcome to the Claude Idea Management System! This guide will help you get started and make the most of the system.

## Quick Start

```bash
# 1. Capture your first idea
/new-idea

# 2. View all your ideas
/list-ideas

# 3. Develop an idea further
/iterate-idea <idea-name>

# 4. Research the market
/market-research <idea-name>
```

That's it! You're ready to manage ideas.

---

## Documentation

The system includes comprehensive documentation:

- **README.md** - Complete system guide with philosophy and examples
- **scoring-framework.md** (`.claude/prompts/`) - Detailed scoring criteria for consistent evaluation
- **USAGE.md** (this file) - Practical usage guide and workflows

---

## Understanding the Scoring System

Every idea is evaluated on three dimensions using a 1-10 scale:

### 1. Work Required (1-10)
**What it measures**: Time, effort, and complexity needed to implement

- **1-3**: Hours to days, simple implementation
- **4-6**: Weeks, moderate complexity
- **7-9**: Months, significant effort
- **10**: Year+, massive undertaking

**Lower scores are better** - less work required

### 2. Coolness Factor (1-10)
**What it measures**: Innovation, excitement, and wow factor

- **1-3**: Mundane, incremental
- **4-6**: Interesting, useful
- **7-9**: Novel, exciting
- **10**: Revolutionary, groundbreaking

**Higher scores are better** - more exciting

### 3. Commercial Opportunity (1-10)
**What it measures**: Market potential and revenue opportunity

- **1-3**: Niche or no market
- **4-6**: Small to medium market
- **7-9**: Large market, clear monetization
- **10**: Massive market opportunity

**Higher scores are better** - more commercial potential

### Composite Score

**Formula**: `(11 - Work) + Coolness + Commercial`

**Maximum**: 30 points

**Why this formula?**
- Inverts work score (lower effort = higher value)
- Rewards "quick wins" - low effort, high payoff ideas
- Creates a single prioritization metric

**Quick Win Threshold**:
- Composite score > 20
- AND Work score < 5
- = High value, low effort ideas you should pursue first!

**Score Interpretation**:
- **25-30**: Exceptional - Top priority
- **20-24**: Strong - Definitely worth pursuing
- **15-19**: Moderate - Consider based on other factors
- **10-14**: Weak - Probably not worth the effort
- **2-9**: Poor - Avoid unless compelling reasons

---

## Command Reference

### `/new-idea` - Capture and Score New Ideas

**Purpose**: Quickly capture a new idea and get AI scoring

**Workflow**:
1. Run `/new-idea`
2. Answer questions about your idea:
   - Title
   - Summary
   - Problem/Opportunity
   - Solution approach
   - Tags/categories
3. Answer clarifying questions
4. Receive automatic AI scoring with reasoning
5. Idea saved to `ideas/inbox/[slug].md`

**Example**:
```
You: /new-idea
Claude: What's the title of your idea?
You: AI-powered recipe generator from fridge photos
Claude: Tell me more about it...
[continues conversation]
Claude: ✅ Idea created: ideas/inbox/ai-recipe-generator.md
        📊 Scores: Work: 7/10, Coolness: 8/10, Commercial: 7/10
        Composite: 15/30
```

**Tips**:
- Don't overthink it - capture quickly, refine later
- Be honest in your answers - helps with accurate scoring
- You can always re-score later with `/iterate-idea`

---

### `/list-ideas` - View All Ideas

**Purpose**: See all your ideas in a sorted, filterable table

**Basic Usage**:
```bash
/list-ideas                    # All ideas, sorted by composite score
```

**Sorting Options**:
```bash
/list-ideas --sort-composite   # Highest total value (default)
/list-ideas --sort-work        # Easiest first (lowest work)
/list-ideas --sort-coolness    # Most exciting first
/list-ideas --sort-commercial  # Best commercial opportunity
```

**Filtering Options**:
```bash
/list-ideas --inbox            # Only new, unprocessed ideas
/list-ideas --backlog          # Scored ideas waiting for action
/list-ideas --active           # Ideas you're currently working on
/list-ideas --archive          # Completed or abandoned ideas
```

**Combining Options**:
```bash
/list-ideas --backlog --sort-work    # Backlog ideas, easiest first
/list-ideas --inbox --sort-composite # Inbox ideas, highest value
```

**Output Format**:
```
📋 All ideas (5 ideas, sorted by composite score)

| Title                    | Work | Cool | Comm | Total | Status  |
|--------------------------|------|------|------|-------|---------|
| 🌟 Browser Tab Manager   |  3   |  8   |  9   |  24   | backlog |
| 🌟 Weekend Task Logger   |  2   |  7   |  8   |  23   | backlog |
| AI Recipe Generator      |  7   |  8   |  7   |  15   | inbox   |

🌟 = Quick win (composite > 20, work < 5)

Summary:
- Total ideas: 5
- Quick wins: 2 🌟
- Next recommended: Browser Tab Manager
```

**Tips**:
- Use `--sort-work` to find quick wins
- Use `--inbox` weekly to process new ideas
- Look for 🌟 markers - these are your best opportunities

---

### `/iterate-idea` - Extend and Improve Ideas

**Purpose**: Deep dive on an idea with guided development modes

**Basic Usage**:
```bash
/iterate-idea <idea-name>           # Exact or partial name
/iterate-idea recipe                # Fuzzy search
/iterate-idea ai-recipe-generator   # Exact filename
```

**Three Development Modes**:

#### 1. Build Cool Tool 🛠️
**When to use**: You want to implement the idea

**What you get**:
- MVP feature list
- Tech stack recommendations
- Architecture overview
- Development phases with timeline
- Risk assessment and mitigations
- Learning plan and resources

**Example questions**:
- "What should the MVP include?"
- "What tech stack are you considering?"
- "How much time can you dedicate?"

#### 2. Research/Extend 🔬
**When to use**: You want to understand the problem space better

**What you get**:
- Problem space deep dive
- Existing solutions landscape
- Unique value proposition
- Key assumptions to validate
- Validation experiments
- Alternative approaches
- Related research and reading

**Example questions**:
- "What aspects are you most uncertain about?"
- "Who would be your ideal first user?"
- "What assumptions need validating?"

#### 3. Commercialize 💰
**When to use**: You want to understand business potential

**What you get**:
- Target customer profiles
- Market sizing (TAM/SAM/SOM)
- Business model options
- Pricing strategy
- Go-to-market plan
- Competitive landscape
- Unit economics
- Traction milestones

**Example questions**:
- "Who is your target customer?"
- "How much would they pay?"
- "How would you reach first 100 customers?"

**After Extension**:
- New extension section added to idea file
- Scores updated based on new insights
- Composite score recalculated
- Summary of changes displayed

**Tips**:
- You can iterate multiple times with different modes
- Each iteration builds on previous work
- Scores may go up OR down - both are valuable learning

---

### `/market-research` - Research Existing Solutions

**Purpose**: Find competitors, analyze market, validate opportunity

**Basic Usage**:
```bash
/market-research <idea-name>
/market-research recipe
/market-research ai-recipe-generator
```

**What It Does**:
1. Searches web for existing solutions
2. Analyzes competition (5-10 competitors)
3. Estimates market size
4. Identifies market gaps
5. Assesses risks and opportunities
6. Generates comprehensive report
7. Updates commercial score if warranted

**Research Areas**:
- **Existing Solutions**: Direct and indirect competitors
- **Market Analysis**: Size, growth, trends, demand signals
- **Competitive Landscape**: How crowded, who leads, what's missing
- **Risks**: Market, competition, timing, execution challenges
- **Opportunities**: Underserved segments, gaps, differentiation

**Output**:
```
✅ Market research completed for AI Recipe Generator

📊 Key Findings:
   - Existing solutions: 8 competitors found
   - Market size: $5B food tech market
   - Competition level: Crowded
   - Market attractiveness: Medium

🎯 Recommendation: Proceed with caution

📈 Commercial Score Updated: 7 → 6/10
   Composite Score: 15 → 14/30

Top insights:
- Large market but many established players
- Photo scanning feature is differentiator
- Consider niche targeting (e.g., dietary restrictions)

Full report added to: ideas/inbox/ai-recipe-generator.md
```

**Tips**:
- Run this BEFORE investing significant time
- Look for gaps in existing solutions
- Pay attention to red flags
- Use findings to refine your approach

---

## Common Workflows

### Daily Idea Capture
**Goal**: Quickly capture ideas without losing momentum

```bash
# Morning: Had 3 ideas in the shower
/new-idea
[Capture idea 1]

/new-idea
[Capture idea 2]

/new-idea
[Capture idea 3]

# Done! Back to your day.
```

**Time**: 5-10 minutes total

---

### Weekly Review
**Goal**: Process inbox, prioritize, plan next actions

```bash
# 1. See what you captured this week
/list-ideas --inbox

# 2. View all ideas sorted by priority
/list-ideas --sort-composite

# 3. Identify quick wins
/list-ideas --sort-work

# 4. Move top idea to active (manually edit the file's status)
# Edit ideas/backlog/best-idea.md and change status to "active"

# 5. Deep dive on your top active idea
/iterate-idea best-idea
> Choose: Build cool tool
```

**Time**: 20-30 minutes weekly

---

### Pre-Development Deep Dive
**Goal**: Validate and plan before building

```bash
# 1. Research the market
/market-research my-idea

# 2. Review research findings
# Read the market research section in the idea file

# 3. If still promising, create build plan
/iterate-idea my-idea
> Choose: Build cool tool

# 4. If uncertain, do more research
/iterate-idea my-idea
> Choose: Research/extend

# 5. If pursuing commercially, plan business
/iterate-idea my-idea
> Choose: Commercialize
```

**Time**: 1-2 hours for thorough validation

---

### Monthly Portfolio Review
**Goal**: Assess overall idea portfolio, archive old ideas

```bash
# 1. View all ideas
/list-ideas

# 2. View active ideas
/list-ideas --active

# 3. View archive to see what you've completed
/list-ideas --archive

# 4. Manually move stale ideas:
# - Active ideas with no progress → back to backlog
# - Completed ideas → archive
# - Ideas you're no longer interested in → archive

# 5. Celebrate wins!
# Review your archive to see what you've accomplished
```

**Time**: 15-20 minutes monthly

---

## File Organization

### Directory Structure
```
ideas/
├── inbox/      # New ideas (unprocessed)
├── backlog/    # Scored, waiting for action
├── active/     # Currently working on (limit to 1-3)
└── archive/    # Completed or abandoned
```

### Moving Ideas Between Directories

Ideas naturally flow through states:
```
inbox → backlog → active → archive
```

**To move an idea**:
1. Edit the idea's markdown file
2. Change the `status:` field in the frontmatter
3. Optionally move the file to the new directory

**Example**:
```markdown
---
id: browser-tab-manager
title: Browser Tab Manager
status: active    # Changed from "backlog"
---
```

Then move the file:
```bash
mv ideas/backlog/browser-tab-manager.md ideas/active/
```

---

## Best Practices

### 1. Capture Quickly, Refine Later
- Don't overthink during `/new-idea`
- Capture the essence, iterate later
- Better to have 10 rough ideas than 1 perfect one

### 2. Review Weekly
- Process inbox regularly
- Keep inbox under 5 ideas
- Prevents backlog buildup

### 3. Limit Active Ideas
- Work on 1-3 ideas max
- More = context switching, less progress
- Move stale active ideas back to backlog

### 4. Trust the Scores
- AI scoring is calibrated for consistency
- Scores help prioritize objectively
- But don't ignore gut feelings

### 5. Research Before Building
- Run `/market-research` before investing time
- 30 minutes of research can save weeks of work
- Look for red flags early

### 6. Iterate Multiple Times
- Use different modes (build/research/commercialize)
- Each iteration reveals new insights
- Scores will evolve with understanding

### 7. Archive Completed Ideas
- Document outcomes (what worked, what didn't)
- Learn from past ideas
- Celebrate completions

### 8. Use Tags Consistently
- Tag ideas by category (software, business, hardware)
- Makes filtering easier later
- Helps identify patterns

---

## Tips and Tricks

### Finding Ideas
```bash
# Quick wins only
/list-ideas --sort-composite
# Look for 🌟 markers

# Easiest ideas
/list-ideas --sort-work

# Most exciting ideas
/list-ideas --sort-coolness

# Best business opportunities
/list-ideas --sort-commercial
```

### Fuzzy Search
```bash
# These all work for "ai-recipe-generator.md"
/iterate-idea recipe
/iterate-idea ai-recipe
/iterate-idea generator
/iterate-idea ai-recipe-generator
```

### Combining Commands
```bash
# Research → Plan → Build workflow
/market-research my-idea
/iterate-idea my-idea
> Research/extend
/iterate-idea my-idea
> Build cool tool
```

### Quick Filtering
```bash
# What should I work on next?
/list-ideas --backlog --sort-composite

# What did I capture this week?
/list-ideas --inbox

# What am I working on?
/list-ideas --active

# What have I completed?
/list-ideas --archive
```

---

## Troubleshooting

### "No idea found matching..."
**Problem**: `/iterate-idea` or `/market-research` can't find your idea

**Solutions**:
1. Run `/list-ideas` to see exact filename
2. Use more specific search term
3. Use full filename: `/iterate-idea ai-recipe-generator`

### Scores seem inconsistent
**Problem**: Similar ideas have very different scores

**Solutions**:
1. Check `.claude/prompts/scoring-framework.md` for criteria
2. Re-score using `/iterate-idea` if needed
3. Remember: AI considers many factors beyond surface similarity

### Too many ideas in inbox
**Problem**: Inbox is overwhelming

**Solutions**:
1. Set weekly review reminder
2. Batch process: `/list-ideas --inbox`
3. Archive ideas you're no longer interested in
4. Move scored ideas to backlog

### Idea file is getting large
**Problem**: Many extensions, hard to read

**Solutions**:
1. This is actually good! Shows deep thinking
2. Use sections to navigate
3. Focus on latest extension and current scores
4. Consider extracting to separate project if ready to build

---

## Advanced Usage

### Custom Tags
Add tags in frontmatter for better organization:
```markdown
---
tags: [software, productivity, weekend-project, react]
---
```

### Manual Score Adjustments
You can manually adjust scores if you disagree with AI:
1. Edit the idea markdown file
2. Update score and reasoning
3. Recalculate composite score

### Linking Related Ideas
Reference other ideas in the Notes or References section:
```markdown
## References
- Related to: [[productivity-dashboard.md]]
- Supersedes: [[old-task-manager-idea.md]]
```

### Exporting Data
Ideas are just markdown files, so you can:
- Version control with git
- Search with grep/ripgrep
- Process with scripts
- Export to other tools

### Adding Custom Skills
Create new skills in `.claude/skills/`:
1. Copy an existing `.prompt.md` file
2. Modify the workflow
3. Update name and description in frontmatter
4. Save and use with `/your-skill-name`

---

## Next Steps

### Getting Started (Week 1)
1. ✅ Run `/new-idea` to capture 3-5 ideas
2. ✅ Run `/list-ideas` to see them all
3. ✅ Pick your top idea and run `/iterate-idea`
4. ✅ Research it with `/market-research`

### Building Momentum (Month 1)
1. Capture 10-15 total ideas
2. Identify 2-3 quick wins
3. Start working on 1 idea actively
4. Establish weekly review habit

### Long-Term Success
1. Capture ideas regularly (weekly)
2. Review and prioritize monthly
3. Complete or abandon ideas (don't hoard)
4. Learn from outcomes
5. Refine your scoring intuition

---

## System Philosophy

**Remember**:
- Ideas are cheap, execution is hard
- Quick wins compound over time
- Not all ideas are worth pursuing
- Scores help decide, but you decide
- The best idea is the one you'll actually build
- Archive liberally, don't be precious

**The goal isn't to have perfect ideas - it's to systematically identify and pursue the ones worth your time.**

---

## Getting Help

- **Documentation**: See README.md for detailed system guide
- **Scoring Criteria**: See `.claude/prompts/scoring-framework.md`
- **Ask Claude**: Just ask questions about the system!
  - "How should I score this?"
  - "What makes a quick win?"
  - "Should I work on idea A or B?"

---

Happy idea managing! 🚀
