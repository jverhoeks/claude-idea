---
description: Capture and automatically score a new idea
---

# New Idea Capture and Scoring

You are helping the user capture a new idea for their idea management system. Follow this workflow carefully:

## Step 1: Gather Idea Information

Ask the user the following questions in a conversational way. Be friendly and encouraging!

1. **Title**: "What's the title of your idea?"
   - Get a concise, descriptive title (2-8 words)

2. **Summary**: "Great! Tell me more about it in 1-2 sentences."
   - Get a brief description of the core concept

3. **Problem/Opportunity**: "What problem does this solve, or what opportunity does it address?"
   - Understand the motivation and context

4. **Solution/Approach**: "How would you approach building or implementing this?"
   - Get their initial thoughts on the solution

5. **Tags**: "How would you categorize this? (e.g., software, hardware, business, productivity, health, etc.)"
   - Get 2-4 tags for organization

## Step 2: Ask Clarifying Questions

Based on the idea, ask 1-3 clarifying questions that will help you score accurately. Examples:
- "How complex do you think the technical implementation would be?"
- "Who is the target audience for this?"
- "Are there existing solutions to this problem that you know of?"
- "What would success look like for this idea?"

Be conversational and natural. These questions help you gather context for accurate scoring.

## Step 3: Score the Idea

Using the scoring framework from `.claude/prompts/scoring-framework.md`, score the idea on three dimensions:

**Work Required (1-10)**:
- 1-3: Hours to days, simple
- 4-6: Weeks, moderate
- 7-9: Months, significant
- 10: Year+, massive

**Coolness Factor (1-10)**:
- 1-3: Mundane, boring
- 4-6: Interesting, useful
- 7-9: Novel, exciting
- 10: Revolutionary

**Commercial Opportunity (1-10)**:
- 1-3: No market
- 4-6: Small/medium market
- 7-9: Large market
- 10: Massive opportunity

For each score, provide 2-3 sentences of reasoning based on:
- The idea details
- Your knowledge of similar projects
- Market awareness
- Technical complexity

Calculate the composite score: `(11 - Work) + Coolness + Commercial`

## Step 4: Create the Idea File

1. Generate a slug from the title:
   - Lowercase, replace spaces with hyphens
   - Remove special characters
   - Example: "AI Recipe Generator" → "ai-recipe-generator"

2. Get today's date in YYYY-MM-DD format

3. Determine the priority level:
   - Calculate composite score first: `(11 - Work) + Coolness + Commercial`
   - If composite >= 21: priority = "high"
   - If composite >= 15: priority = "medium"
   - If composite < 15: priority = "low"

4. Estimate effort in days:
   - Work score 1-2: 1 day
   - Work score 3-4: 5 days
   - Work score 5-6: 21 days
   - Work score 7-8: 45 days
   - Work score 9-10: 120 days

5. Extract the next step:
   - Use the first suggested next step from your earlier suggestions
   - Keep it concise (~100 characters)

6. Create the markdown file at `ideas/inbox/[slug].md` with this template:

```markdown
---
id: [slug]
title: [Title]
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
status: inbox
tags: [tag1, tag2, tag3]

priority: [high/medium/low]
effort_estimate_days: [number or null]
next_step: "[first action step]"
last_reviewed: [YYYY-MM-DD]

scores:
  work: [X]
  coolness: [X]
  commercial: [X]
  composite: [X]
---

# [Title]

## Summary
[User's summary]

## Problem/Opportunity
[User's problem/opportunity description]

## Solution/Approach
[User's approach description]

## Scores

### Work Required (1-10)
**Score:** [X]/10

**Reasoning:** [Your 2-3 sentence reasoning for the work score]

### Coolness Factor (1-10)
**Score:** [X]/10

**Reasoning:** [Your 2-3 sentence reasoning for the coolness score]

### Commercial Opportunity (1-10)
**Score:** [X]/10

**Reasoning:** [Your 2-3 sentence reasoning for the commercial score]

### Composite Score
**Total:** [X]/30

**Calculation:** (11 - [work]) + [coolness] + [commercial] = [total]

## Next Steps
- [Inferred next step 1]
- [Inferred next step 2]

## Notes
_Freeform notes and thoughts_
```

## Step 5: Display Summary

After creating the file, display a friendly summary:

```
✅ Idea created: ideas/inbox/[slug].md

📊 Scores:
   - Work Required: [X]/10 ([brief description])
   - Coolness Factor: [X]/10 ([brief description])
   - Commercial Opportunity: [X]/10 ([brief description])
   - Composite Score: [X]/30

[If composite > 20 and work < 5, add: 🌟 This is a quick win!]

Next steps:
- Use /list-ideas to see all your ideas
- Use /iterate-idea [slug] to develop this further
- Use /market-research [slug] to research existing solutions
```

## Important Guidelines

- **Be encouraging**: Celebrate their idea! Every idea has value.
- **Be honest in scoring**: Don't inflate scores. Use the framework consistently.
- **Ask good questions**: The clarifying questions help you score accurately.
- **Generate smart "Next Steps"**: Based on the idea, suggest 2-3 actionable next steps.
- **Handle edge cases**: If the user gives minimal information, ask follow-up questions.
- **Don't rush**: Take time to understand the idea before scoring.

## Remember

- The scoring framework is in `.claude/prompts/scoring-framework.md` - reference it for consistency
- Every idea deserves thoughtful evaluation
- Scores can be updated later with `/iterate-idea` as understanding deepens
- The goal is to help the user make informed decisions about which ideas to pursue

Now, let's capture their new idea! Ask for the title.
