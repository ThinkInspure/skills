---
name: prompt-optimizer
description: Expert system for optimizing AI prompts using 57 proven frameworks. Use when users want to improve, structure, or create effective prompts for AI interactions. Triggers include requests like "optimize this prompt", "help me write a better prompt", "improve my AI instruction", or when users share a prompt/requirement that needs refinement using established frameworks (RICE, CRISPE, BAB, Tree of Thought, SCAMPER, Chain of Thought, etc.).
---

# Prompt Optimizer

Optimize AI prompts using 57 proven frameworks tailored to specific use cases and scenarios.

## Workflow

Follow this sequential process for every prompt optimization request:

### 1. Understand User Input

Analyze what the user provides:
- **Raw requirement**: User describes what they want the AI to do
- **Existing prompt**: User shares a prompt they want to improve
- **Scenario description**: User describes their use case

Extract the core intent, target audience, desired outcome, and any constraints.

### 2. Select Framework

Read `references/frameworks_summary.md` to identify the best-matching framework(s) based on:
- Application scenario alignment
- Complexity level (simple/medium/complex)
- Domain fit (marketing, education, decision-making, etc.)

**Framework categories:**
- **Quick tasks** (3 elements): APE, ERA, TAG, RTF, BAB, PEE, ELI5
- **Standard workflows** (4-5 elements): RACE, CIDI, SPEAR, SPAR, FOCUS, SMART, CARE
- **Complex processes** (6+ elements): RACEF, CRISPE, SCAMPER, Six Thinking Hats, PROMPT

If multiple frameworks could work, present 2-3 options with brief rationale.

### 3. Clarify Requirements

Before generating the optimized prompt, verify understanding with the user:

**Check for ambiguities:**
- Missing context about target audience
- Unclear desired output format
- Ambiguous success criteria
- Unstated constraints or preferences

**Use targeted questions:**
- "Should the output be [X] or [Y]?"
- "What format do you prefer: [options]?"
- "Any specific constraints I should know about?"

Do NOT proceed to Step 4 until all ambiguities are resolved.

### 4. Load Framework Details

Read the specific framework file from `references/frameworks/<framework_name>.md` to understand:
- Framework components and structure
- Best practices and examples
- Component definitions and scoring (if applicable)

### 5. Generate Optimized Prompt

Create the final prompt following the framework structure:

**Output format:**
```
## Framework Used: [Framework Name]

## Optimized Prompt:
[Generated prompt following framework structure]

## Framework Breakdown:
[Explain how each component was applied]
```

**Quality standards:**
- Clear, specific, actionable instructions
- Structured according to framework elements
- Includes relevant context and constraints
- Specifies expected output format
- Matches user's clarified requirements

## Framework Reference

This skill includes 57 frameworks organized by application scenario:

**Access frameworks:**
- `references/frameworks_summary.md` - Quick reference table of all 57 frameworks with scenarios
- `references/frameworks/<number>_<name>_Framework.md` - Detailed framework documentation

**When to read which file:**
1. Always read `frameworks_summary.md` first for framework selection
2. Read specific framework file only after selecting the best match
3. For complex cases requiring multiple frameworks, read 2-3 relevant files

**Framework file structure:**
Each framework file contains:
- Application scenarios
- Framework overview
- Component definitions
- Best practices
- Practical examples

## Examples

### Example 1: Optimizing a vague request

**User input:** "Help me write a prompt for analyzing sales data"

**Process:**
1. Identify scenario: Data analysis, decision support
2. From `frameworks_summary.md`, match to **RICE Framework** (marketing, data analysis) or **GRADE Framework** (data analysis, strategy)
3. Ask: "What decisions will this analysis inform? Do you need prioritization scoring?"
4. User clarifies: "I need to prioritize which product features to develop based on sales impact"
5. Select RICE (better for prioritization)
6. Read `references/frameworks/05_RICE_Framework.md`
7. Generate optimized prompt with Reach, Impact, Confidence, Effort scoring

### Example 2: Improving an existing prompt

**User input:** "Make this better: 'Write a blog post about AI'"

**Process:**
1. Identify scenario: Content creation, blogging
2. From `frameworks_summary.md`, match to **BLOG Framework** or **4S Method**
3. Ask: "Who's the target audience? What's the key message you want to convey?"
4. User clarifies: "Tech professionals, focus on AI practical applications"
5. Select BLOG Framework
6. Read `references/frameworks/08_BLOG_Framework.md`
7. Generate structured prompt with Background, Learning objective, Objectives, Guidance

### Example 3: Multiple framework options

**User input:** "I need a prompt for brainstorming new product ideas"

**Process:**
1. Identify scenario: Creative thinking, innovation, product development
2. From `frameworks_summary.md`, identify multiple matches:
   - **SCAMPER Framework** (product innovation, creative exploration)
   - **HMW Framework** (design thinking, problem reframing)
   - **RACEF Framework** (brainstorming, creative generation)
3. Present options: "I found three excellent frameworks for this. SCAMPER systematically explores modifications, HMW reframes problems as opportunities, and RACEF generates diverse ideas through roles. Which approach resonates with you?"
4. User selects or asks for recommendation
5. Proceed with selected framework

## Best Practices

**Framework selection:**
- Match scenario first, complexity second
- When uncertain between 2-3 frameworks, present options to user
- Consider user's familiarity level (beginners → simpler frameworks)
- Domain-specific frameworks often outperform generic ones

**Requirement clarification:**
- Ask 2-4 focused questions maximum
- Offer specific choices rather than open-ended questions
- Build on user's language and terminology
- Confirm understanding before generating

**Prompt generation:**
- Follow framework structure strictly
- Make implicit requirements explicit
- Include concrete examples when helpful
- Specify output format clearly
- Add constraints and success criteria

**Quality checks:**
- Does the prompt match the framework structure?
- Are all framework components addressed?
- Is the prompt actionable and specific?
- Does it align with user's clarified requirements?
