# Idea Scoring Framework

This document defines the scoring criteria for evaluating ideas. Use this as a reference when scoring ideas to ensure consistency.

## Scoring Dimensions

Each idea is scored on three dimensions using a 1-10 scale:

### 1. Work Required (1-10)

**What it measures**: Time, effort, resources, and complexity needed to implement the idea.

**Scale**:
- **1-2**: **Minimal** - A few hours of work, very simple
  - Example: Add a feature flag, simple script, config change
  - No dependencies, straightforward implementation

- **3-4**: **Light** - A day or two of work, low complexity
  - Example: Small utility tool, simple CLI command, basic webpage
  - Few dependencies, well-known tech, clear path forward

- **5-6**: **Moderate** - Weeks of work, moderate complexity
  - Example: Mobile app MVP, moderate web app, integration project
  - Multiple components, some research needed, standard tech stack

- **7-8**: **Significant** - Months of work, high complexity
  - Example: Full-featured product, complex integration, ML project
  - Many components, significant research, challenging tech

- **9-10**: **Massive** - Year+ of work, very high complexity
  - Example: Platform, operating system, major infrastructure
  - Large team needed, deep research required, novel technology

**Consider**:
- Development time (hours/days/weeks/months)
- Technical complexity
- Required expertise level
- Number of components/systems involved
- Research and learning needed
- Dependencies on external factors
- Testing and iteration requirements

**Scoring tip**: Be realistic. Most ideas are 4-7. Reserve 1-3 for truly trivial tasks and 8-10 for massive undertakings.

---

### 2. Coolness Factor (1-10)

**What it measures**: Innovation, excitement, wow factor, and personal interest.

**Scale**:
- **1-2**: **Boring** - Mundane, routine, uninteresting
  - Example: Yet another CRUD app, standard business software
  - No novel aspects, purely functional

- **3-4**: **Incremental** - Slight improvement over existing
  - Example: Minor optimization, small UX improvement
  - Useful but not exciting

- **5-6**: **Interesting** - Notably useful or clever
  - Example: Smart automation, helpful tool, good UX innovation
  - People would find it interesting and useful

- **7-8**: **Novel** - Innovative approach, exciting to build/use
  - Example: Creative use of technology, unique problem-solving
  - Would make people say "that's really cool!"

- **9-10**: **Revolutionary** - Groundbreaking, paradigm-shifting
  - Example: New interaction paradigm, breakthrough innovation
  - Could change how people think about a problem space

**Consider**:
- How novel is the approach?
- Would this excite other people?
- Is it fun/interesting to you personally?
- Does it use technology in creative ways?
- Is there a "wow factor"?
- Would you be proud to show this to others?
- Does it solve a problem in an unexpected way?

**Scoring tip**: Don't be cynical. If an idea genuinely excites you, give it credit! Personal excitement matters.

---

### 3. Commercial Opportunity (1-10)

**What it measures**: Market potential, monetization possibility, and revenue opportunity.

**Scale**:
- **1-2**: **No market** - No clear way to monetize, very niche
  - Example: Personal hobby project, academic exercise
  - No one would pay for this

- **3-4**: **Tiny niche** - Very small market, limited monetization
  - Example: Tool for specific job/hobby, micro-niche SaaS
  - Hundreds of potential users, small revenue potential

- **5-6**: **Small/Medium market** - Clear but limited market
  - Example: Industry-specific tool, specialized service
  - Thousands of potential users, modest revenue ($10K-$100K/year)

- **7-8**: **Large market** - Significant market opportunity
  - Example: Productivity tool, consumer app, B2B SaaS
  - Millions of potential users, strong revenue ($100K-$1M+/year)

- **9-10**: **Massive opportunity** - Huge addressable market
  - Example: Platform, major consumer product, enterprise solution
  - Billions in potential market size, unicorn potential

**Consider**:
- How many people have this problem?
- How painful is the problem?
- Would people/companies pay for a solution?
- What's the market size? (users × willingness to pay)
- How much would they pay? ($/user/month)
- Is there clear monetization? (subscription, ads, marketplace, etc.)
- What's the competition like?
- Is the market growing or shrinking?

**Scoring tip**: Be objective about market reality, not just your enthusiasm. A cool idea might have no commercial potential - that's okay!

---

## Composite Score Calculation

**Formula**: `(11 - Work) + Coolness + Commercial`

**Range**: 2 to 30

**Why this formula?**:
- Inverts work score (lower work = higher value)
- Rewards "quick wins" - low effort, high payoff
- Balances effort against potential value
- Creates a single prioritization metric

**Interpreting Composite Scores**:
- **25-30**: Exceptional - High priority, likely a quick win
- **20-24**: Strong - Definitely worth pursuing
- **15-19**: Moderate - Consider based on other factors
- **10-14**: Weak - Probably not worth the effort
- **2-9**: Poor - Avoid unless other compelling reasons

**Quick Win Threshold**: Composite > 20 AND Work < 5
- These are the "sweet spot" ideas
- Low effort, high value
- Should be top priority

---

## Scoring Process

When scoring an idea:

1. **Read the idea thoroughly** - Understand the full context
2. **Ask clarifying questions** if needed - Get details that affect scoring
3. **Score each dimension independently** - Don't let one influence others
4. **Provide reasoning** - 2-3 sentences explaining each score
5. **Calculate composite** - Use the formula
6. **Be consistent** - Use the same criteria across all ideas
7. **Be honest** - Don't inflate scores, be realistic

**Example Reasoning**:

> **Work Required: 6/10**
> This would require building a mobile app with ML integration for image recognition, cloud backend for recipe storage, and user authentication. Estimate 4-6 weeks for a solo developer to build an MVP. Moderate complexity with known technologies.
>
> **Coolness Factor: 8/10**
> Novel application of computer vision to a common household problem. The "scan your fridge, get recipes" UX is delightful and would generate strong word-of-mouth. Exciting to build and use.
>
> **Commercial Opportunity: 7/10**
> Large addressable market (anyone who cooks), clear subscription model ($5/month), existing competitors prove demand. Crowded space but room for differentiation with photo scanning feature.
>
> **Composite Score: 16/30**
> Calculation: (11 - 6) + 8 + 7 = 16

---

## Common Scoring Mistakes

**Mistake**: Scoring based on current skill level
- ❌ "I don't know React Native, so Work = 9"
- ✅ Score based on objective complexity, not your current skills

**Mistake**: Letting coolness influence commercial score
- ❌ "This is so cool, people will definitely pay!"
- ✅ Score commercial based on market evidence, not enthusiasm

**Mistake**: Being too harsh or too generous
- ❌ Everything is 5/10 or everything is 9/10
- ✅ Use the full scale, most ideas are 4-7 on each dimension

**Mistake**: Overthinking
- ❌ Spending 30 minutes deciding between 6 or 7
- ✅ Make a reasonable judgment and move on, you can re-score later

**Mistake**: Ignoring context
- ❌ Scoring without understanding the full idea
- ✅ Ask clarifying questions first

---

## Re-scoring

Scores can and should change when:
- You learn more about the idea (after `/iterate-idea`)
- Market research reveals new information (after `/market-research`)
- You gain expertise that reduces work estimate
- You discover the market is larger/smaller than expected
- The scope changes significantly

**When re-scoring**:
- Keep old scores in "History" section
- Note what changed and why
- Update composite score
- Don't be afraid to significantly revise scores

---

## Examples

### Example 1: Browser Tab Manager
- **Work**: 3/10 (Browser extension, ~2-3 days)
- **Coolness**: 8/10 (Solves annoying problem elegantly)
- **Commercial**: 9/10 (Millions of users, proven market)
- **Composite**: 24/30 - **Quick Win! 🌟**

### Example 2: Blockchain-Based Social Network
- **Work**: 9/10 (Complex protocol, scaling challenges, months of work)
- **Coolness**: 7/10 (Innovative but blockchain fatigue)
- **Commercial**: 3/10 (Unclear business model, declining interest)
- **Composite**: 12/30 - **Poor fit**

### Example 3: Weekend Task Logger
- **Work**: 2/10 (Simple script or spreadsheet, few hours)
- **Coolness**: 6/10 (Personally useful, clean design)
- **Commercial**: 2/10 (Personal tool, no market)
- **Composite**: 17/30 - **Moderate, good side project**

---

## Calibration

Over time, calibrate your scoring by:
- Reviewing completed ideas: Were the scores accurate?
- Comparing scores across ideas: Are they relatively consistent?
- Tracking outcomes: Do high-scoring ideas actually succeed?
- Adjusting criteria based on your context and goals

**The scoring system is a tool, not a law.** Use it to inform decisions, but trust your intuition too.
