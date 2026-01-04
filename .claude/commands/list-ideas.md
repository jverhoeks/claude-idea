---
description: View all ideas with scores, sorting, and filtering options
---

# List Ideas

You are displaying all ideas with their scores in a formatted table. Follow this workflow:

## Step 1: Parse Arguments

The user may provide options like:
- `--sort-work` - Sort by work score (lowest to highest)
- `--sort-coolness` - Sort by coolness score (highest to lowest)
- `--sort-commercial` - Sort by commercial score (highest to lowest)
- `--sort-composite` - Sort by composite score (highest to lowest) - **DEFAULT**
- `--inbox` - Filter to inbox ideas only
- `--backlog` - Filter to backlog ideas only
- `--active` - Filter to active ideas only
- `--archive` - Filter to archive ideas only
- (no filter) - Show all ideas

**Default behavior** (no args): Show all ideas sorted by composite score (highest first)

## Step 2: Find All Idea Files

1. Use Glob tool to find all markdown files in `ideas/` subdirectories
2. Pattern: `ideas/**/*.md`
3. Exclude `.gitkeep` files
4. If no ideas found:
   - Say: "No ideas found! Use /new-idea to create your first idea."
   - End workflow

## Step 3: Parse Each Idea File

For each idea file:
1. Read the file using Read tool
2. Extract from frontmatter (between `---`):
   - title
   - status
   - created date
3. Extract from scores section:
   - Work Required score (look for "**Score:** X/10")
   - Coolness Factor score
   - Commercial Opportunity score
   - Composite Score (or calculate it if missing)
4. If scores are missing:
   - Use placeholders: "-" for each score
   - Note: "Not scored yet"

## Step 4: Apply Filters

Based on the filter argument:
- `--inbox`: Include only ideas with status = "inbox"
- `--backlog`: Include only ideas with status = "backlog" or "scored"
- `--active`: Include only ideas with status = "active"
- `--archive`: Include only ideas with status = "archive" or "completed" or "abandoned"
- No filter: Include all ideas

## Step 5: Sort Ideas

Based on the sort argument:
- `--sort-work`: Sort by work score, **ascending** (lowest work first)
- `--sort-coolness`: Sort by coolness score, **descending** (highest first)
- `--sort-commercial`: Sort by commercial score, **descending** (highest first)
- `--sort-composite` or default: Sort by composite score, **descending** (highest first)

For ideas without scores, place them at the bottom of the list.

## Step 6: Identify Quick Wins

Mark ideas as quick wins (🌟) if:
- Composite score > 20
- Work score < 5
- Idea has been scored (not missing scores)

## Step 7: Format and Display

Create a formatted table with these columns:
- 🌟 (if quick win)
- **Title** (truncate if > 40 chars)
- **Work** (score/10)
- **Cool** (score/10)
- **Comm** (score/10)
- **Total** (composite/30)
- **Status** (inbox/backlog/active/archive)

**Table format**:
```
📋 [Filter description] ([X] ideas, sorted by [sort-field])

| Title                          | Work | Cool | Comm | Total | Status  |
|--------------------------------|------|------|------|-------|---------|
| 🌟 [Title 1]                   |  3   |  8   |  9   |  24   | backlog |
| 🌟 [Title 2]                   |  2   |  7   |  8   |  23   | backlog |
| [Title 3]                      |  7   |  8   |  7   |  15   | inbox   |

🌟 = Quick win (composite > 20, work < 5)
```

## Step 8: Add Summary Insights

After the table, provide useful insights:

```
Summary:
- Total ideas: [X]
- Quick wins: [X] 🌟
- Average composite score: [X]/30
- Highest scored: [Title] ([Score]/30)
[If quick wins > 0: - Next recommended: [Highest quick win title]]
```

## Important Guidelines

- **Handle missing scores gracefully**: Use "-" and note it in summary
- **Truncate long titles**: If > 40 chars, truncate with "..."
- **Be helpful in summaries**: Provide actionable insights
- **Quick win highlighting**: Make these stand out visually

Ready to list ideas! By default, I'll show all ideas sorted by composite score (highest first).
