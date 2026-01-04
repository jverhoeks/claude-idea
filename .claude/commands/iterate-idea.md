---
description: Extend and improve an idea with different development modes
---

# Iterate and Extend Idea

You are helping the user extend and improve one of their ideas. Follow this workflow carefully:

## Step 1: Find the Idea

The user will provide either:
- A filename (e.g., "ai-recipe-generator")
- A partial title or keyword (e.g., "recipe")
- The full path (e.g., "ideas/inbox/ai-recipe-generator.md")

**Your task**:
1. Search for matching idea files using Glob tool: `ideas/**/*[search-term]*.md`
2. If multiple matches found: List them and ask user to select
3. If one clear match found: Confirm and proceed
4. If no matches found: Say "No idea found" and end

## Step 2: Read and Display the Idea

1. Read the idea file
2. Extract and display: Title, Summary, Current scores, Status
3. Give a brief assessment

## Step 3: Choose Extension Mode

Ask the user how they want to extend the idea:

```
How would you like to extend this idea?

1. **Build cool tool** 🛠️
   Focus on implementation: tech stack, MVP features, architecture, development plan

2. **Research/extend** 🔬
   Deep dive: problem space, alternatives, validation, research

3. **Commercialize** 💰
   Business strategy: market analysis, business model, go-to-market
```

## Step 4: Mode-Specific Iteration

### Mode 1: Build Cool Tool 🛠️

Ask targeted questions:
1. "What should the MVP include?"
2. "What tech stack are you considering?"
3. "How much time can you dedicate?"
4. "What's your skill level with required technologies?"

**Generate**:
- MVP Feature List
- Tech Stack Recommendation
- Architecture Overview
- Development Phases
- Risk Assessment
- Learning Plan

### Mode 2: Research/Extend 🔬

Ask targeted questions:
1. "What aspects are you most uncertain about?"
2. "Who would be your ideal first user?"
3. "What assumptions should be validated?"
4. "What alternatives have you considered?"

**Generate**:
- Problem Space Analysis
- Existing Solutions
- Unique Value Proposition
- Assumptions to Validate
- Validation Experiments
- Alternative Approaches

### Mode 3: Commercialize 💰

Ask targeted questions:
1. "Who is your target customer?"
2. "How much would they pay?"
3. "How would you reach first 100 customers?"
4. "What's your unfair advantage?"

**Generate**:
- Target Customer Profile
- Market Sizing (TAM/SAM/SOM)
- Business Model Options
- Pricing Strategy
- Go-to-Market Plan
- Competitive Analysis
- Unit Economics
- Traction Milestones

## Step 5: Update the Idea File

1. Add the extension to the "## Extensions" section
2. Keep all previous extensions

## Step 6: Re-score the Idea

Based on new insights, re-evaluate:
- Work Required
- Coolness Factor
- Commercial Opportunity

Provide new scores with reasoning that references the extension.
Preserve old scores in history.

## Step 7: Display Summary

```
✅ Extension added to ideas/[dir]/[filename].md

📝 Added: [Extension type] plan
📊 Updated Scores:
   - Work Required: [OLD] → [NEW]/10
   - Coolness Factor: [OLD] → [NEW]/10
   - Commercial Opportunity: [OLD] → [NEW]/10
   - Composite Score: [OLD] → [NEW]/30

Key insights:
- [Insight 1]
- [Insight 2]

Next steps:
- [Action 1]
- [Action 2]
```

## Important Guidelines

- Be thorough and specific
- Ask good questions
- Update scores honestly (may go up or down)
- Keep history - append, don't overwrite
- Multiple iterations are encouraged

Ready to extend an idea! Which idea would you like to work on?
