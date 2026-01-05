---
description: Migrate all ideas to enhanced frontmatter format with nested scores and metadata
---

# Migrate Ideas to Enhanced Format

You are helping migrate all existing idea files from the basic format to the enhanced format with nested scores and rich metadata. Follow this workflow carefully:

## Step 1: Prepare for Migration

1. Display friendly introduction message
2. Explain what will be updated (priority, effort_estimate_days, next_step, last_reviewed, nested scores)
3. Mention that git history preserves old format if needed to revert
4. Ask user to confirm they want to proceed

## Step 2: Find All Idea Files

1. Use Glob tool to find all markdown files in `ideas/` subdirectories
2. Pattern: `ideas/**/*.md`
3. Exclude `.gitkeep` files
4. If no ideas found:
   - Say: "No ideas found! Nothing to migrate."
   - End workflow

## Step 3: Process Each Idea File

For each idea file found, follow this process:

### 3a. Read the File

Read the file using the Read tool. This gives you the current frontmatter and body content.

### 3b. Extract Current Data

Parse the frontmatter to get:
- `id`, `title`, `created`, `updated`, `status`, `tags`

Parse the body to find scores:
- Look for "### Work Required" section → find "**Score:** X/10"
- Look for "### Coolness Factor" section → find "**Score:** X/10"
- Look for "### Commercial Opportunity" section → find "**Score:** X/10"
- Look for "### Composite Score" section → find "**Total:** X/30"

Extract these exactly as integers (e.g., "**Score:** 6/10" → 6).

### 3c. Intelligently Extract New Fields

**Priority (high/medium/low):**
```
IF composite score >= 21: priority = "high"
ELSE IF composite score >= 15: priority = "medium"
ELSE: priority = "low"

ALSO check assessment text for keywords like "quick win", "critical", "significant opportunity"
If found, may upgrade priority one level.
```

**Effort Estimate Days:**
```
Parse the "### Work Required" reasoning text.

Look for time mentions:
- If contains "days": extract number (e.g., "3-5 days" → 4)
- If contains "weeks": work_score * 7 (e.g., work=5 → 35 days)
- If contains "months": work_score * 21 (e.g., work=8 → 168 days)

Fallback if no time mentions:
- work score 1-2: 1 day
- work score 3-4: 5 days
- work score 5-6: 21 days
- work score 7-8: 45 days
- work score 9-10: 120 days
```

**Next Step:**
```
Look for "## Next Steps" section in the markdown body.
Extract the FIRST bullet point or numbered item.
Remove bullet/number prefix (-, *, 1., etc.)
Truncate to ~100 characters if longer.
If no "## Next Steps" section: set to null.
```

**Last Reviewed:**
```
Set to today's date: 2026-01-05
```

### 3d. Create Enhanced Frontmatter

Build new frontmatter in this exact order and format:

```yaml
---
id: [id from original]
title: [title from original]
created: [created from original]
updated: [updated from original]
status: [status from original]
tags: [tags from original]

priority: [extracted priority]
effort_estimate_days: [extracted effort or null]
next_step: "[extracted next step or null]"
last_reviewed: 2026-01-05

scores:
  work: [extracted work score or null]
  coolness: [extracted coolness score or null]
  commercial: [extracted commercial score or null]
  composite: [extracted composite score or null]
---
```

**Important:** Keep the exact formatting:
- No quotes around priority, effort_estimate_days, last_reviewed (except in next_step)
- Nested scores object with proper indentation (2 spaces)
- Empty line after tags before new fields
- Empty line after last_reviewed before scores object

### 3e. Update the File

Use the Edit tool to replace the old frontmatter with the new frontmatter:
- Find the old frontmatter (from first `---` to second `---`)
- Replace it with the new frontmatter
- Keep ALL body content exactly the same

## Step 4: Migration Execution

Execute the migration for each file:
- Read file
- Extract and transform data
- Update file with new frontmatter
- Track success/errors

If a file fails:
- Log the error (e.g., "ai-fridge-to-menu.md: Failed to parse scores")
- Continue with next file
- Report failure in summary

## Step 5: Display Migration Summary

After all files processed, display a summary like this:

```
✅ Migrated [X] ideas to enhanced format

📊 Migration Details:

| File                              | Priority | Effort (days) | Next Step                  |
|-----------------------------------|----------|---------------|----------------------------|
| ai-fridge-to-menu                 | medium   | 42            | Market research            |
| idea-manager                       | high     | 21            | Build autonomous agent MVP |
| idea-collector-website            | medium   | 4             | Set up Astro project       |
| cloud-independent-data-platform   | high     | 168           | Build MVP security model   |

✨ Migration Complete!

🎯 New Features Available:
   - Filter by priority: /list-ideas --priority=high
   - Filter by effort: /list-ideas --effort<10
   - Track stale ideas: /list-ideas --stale=30

Next Steps:
- Run /list-ideas to see enhanced metadata
- Try new filtering options
- All future /new-idea captures will use enhanced format automatically
```

## Important Guidelines

- **Parse carefully:** Missing scores should result in `null`, not errors
- **Preserve body:** Never modify the markdown body content, only the frontmatter
- **Idempotent:** Safe to run multiple times (detects if already migrated)
- **Git safety:** User can always `git checkout` to revert if needed
- **Be specific:** Show extracted values so user can verify accuracy

## Edge Cases

**Missing Scores:**
- If an idea has no scores yet, set all score values to `null`

**Already Migrated:**
- If frontmatter already has `scores:` object, skip that file
- Report: "[filename] already migrated, skipping"

**Malformed Content:**
- If can't find Next Steps section: set to `null`
- If can't parse work score: set to `null` for that field
- Continue processing with what you can extract

**Different Status Directories:**
- Handle ideas in `ideas/inbox/`, `ideas/backlog/`, `ideas/active/`, `ideas/archive/`
- Migrate all regardless of status

## Example Transformation

**Before:**
```yaml
---
id: ai-fridge-to-menu
title: AI Fridge to Menu
created: 2026-01-04
updated: 2026-01-04
status: inbox
tags: [software, lifestyle]
---

# AI Fridge to Menu

[... body content ...]

### Work Required (1-10)
**Score:** 6/10
**Reasoning:** Building a mobile app with computer vision...

### Coolness Factor (1-10)
**Score:** 7/10

### Commercial Opportunity (1-10)
**Score:** 6/10

### Composite Score
**Total:** 18/30

## Next Steps

1. **Market research** - Run `/market-research ai-fridge-to-menu`
2. **Validate MVP scope** - Define minimum set...
```

**After:**
```yaml
---
id: ai-fridge-to-menu
title: AI Fridge to Menu
created: 2026-01-04
updated: 2026-01-04
status: inbox
tags: [software, lifestyle]

priority: medium
effort_estimate_days: 42
next_step: "Market research - Run `/market-research ai-fridge-to-menu`"
last_reviewed: 2026-01-05

scores:
  work: 6
  coolness: 7
  commercial: 6
  composite: 18
---

# AI Fridge to Menu

[... EXACT SAME body content ...]

### Work Required (1-10)
**Score:** 6/10
[etc...]
```

Ready to migrate! When you're set, I'll start the process.
