---
name: prompt-optimizer
description: Expert system for optimizing AI prompts using 57 proven frameworks. Use when user wants to improve prompts, create better prompts, or needs guidance on prompt engineering. Analyzes user needs, selects optimal framework, clarifies requirements, and generates professional prompts following best practices.
---

# Prompt Optimizer Expert

This skill helps users create high-quality, optimized prompts using 57 proven prompt engineering frameworks. It guides users through a structured workflow to transform raw ideas or existing prompts into professional, effective prompts.

## When to Use This Skill

**Trigger conditions:**
- User wants to optimize an existing prompt
- User wants to create a new prompt for a specific task
- User mentions "prompt engineering", "improve my prompt", "better prompt"
- User provides a task description and needs a prompt for it
- User asks "how should I prompt Claude/ChatGPT/AI for X?"

## Workflow Overview

The skill follows a 5-step process:

1. **Input Analysis**: Understand user's needs or existing prompt
2. **Scenario Matching**: Identify the best-matching use case scenario
3. **Framework Selection**: Choose the optimal framework(s) from 57 options
4. **Requirement Clarification**: Verify understanding and fill any gaps
5. **Prompt Generation**: Create the final optimized prompt

## Step 1: Input Analysis

When activated, first understand what the user needs:

**If user provides an existing prompt:**
- Analyze the prompt's purpose, target task, and current structure
- Identify what the user wants to improve (clarity, specificity, output quality, etc.)

**If user provides a task description or need:**
- Extract the core objective
- Identify the domain/field (marketing, coding, analysis, writing, etc.)
- Note any constraints or requirements mentioned

**Ask clarifying questions such as:**
- What is the main goal you want to achieve with this prompt?
- Who or what will be using this prompt? (You, a team, automation, etc.)
- What kind of output are you expecting?
- Are there any specific constraints or requirements?

Keep questions concise (3-5 questions maximum). User can answer in shorthand.

## Step 2: Scenario Matching

Based on the input analysis, identify which application scenario(s) best match the user's needs.

**Common scenario categories:**

**Content Creation & Writing:**
- Blog posts, articles, marketing copy
- Technical documentation
- Creative writing, storytelling
- Social media content

**Analysis & Research:**
- Market research and competitive analysis
- Data analysis and insights
- Problem diagnosis
- Decision support

**Strategy & Planning:**
- Strategic planning, roadmaps
- Product development
- Goal setting and OKRs
- Project planning

**Education & Training:**
- Explaining complex concepts
- Creating learning materials
- Training content
- Knowledge transfer

**Conversation & Interaction:**
- AI assistant configuration
- Customer service scripts
- Role-playing scenarios
- Chatbot design

**Technical & Development:**
- Code generation
- System design
- Technical specifications
- Debugging and troubleshooting

**Innovation & Ideation:**
- Brainstorming
- Creative problem solving
- Product innovation
- Design thinking

Internally identify 2-3 most relevant scenarios. You will use these to select frameworks in the next step.

## Step 3: Framework Selection

Using the identified scenarios, select the most appropriate framework(s) from the 57 available options.

**Framework selection logic:**

1. **Read the framework selection guide**: Use the references/framework-selector.md file to understand which frameworks best match the identified scenarios

2. **Consider task complexity**:
   - Simple tasks (3 or fewer elements): APE, ERA, TAG, RTF, BAB, PEE, ELI5
   - Medium tasks (4-5 elements): RACE, CIDI, SPEAR, SPAR, FOCUS, SMART, CARE, TRACE
   - Complex tasks (6+ elements): RACEF, CRISPE, SCAMPER, Six Thinking Hats, PROMPT, RISEN

3. **Select 1-3 candidate frameworks** that best fit the scenario and complexity

4. **Present options to user** (if multiple strong candidates):
   - Briefly describe each candidate framework (1 sentence)
   - Explain why it fits their needs
   - Recommend your top choice
   - Ask if they want to use the recommended one or prefer another

**Example presentation:**
\`\`\`
Based on your need to create marketing content for a SaaS product, I recommend these frameworks:

1. **BAB (Before-After-Bridge)** - Great for showcasing transformation and benefits. Best for direct conversion-focused copy. (Recommended)
2. **SPEAR (Statement-Problem-Example-Action-Result)** - Excellent for persuasive content with strong evidence and calls-to-action.
3. **RACEF (Rephrase-Append-Contextualize-Examples-Follow-up)** - Comprehensive framework for strategic marketing with iterative refinement.

I recommend starting with BAB as it's focused and effective for your use case. Would you like to proceed with BAB, or would you prefer one of the others?
\`\`\`

If only one clear framework fits, state your recommendation and briefly explain why it's the best match.

## Step 4: Requirement Clarification

Before generating the final prompt, verify all necessary information is available.

**Load the selected framework details:**
Read the corresponding framework file from references/frameworks/ to understand:
- Framework components and structure
- What information is needed for each component
- Best practices and examples

**Check for gaps:**
Identify any missing information required by the framework components.

**Ask targeted clarification questions:**
Based on the framework's requirements, ask specific questions to fill gaps:

- Context details (audience, industry, constraints)
- Desired output format or structure
- Specific examples or references to follow
- Tone, style, or voice requirements
- Success criteria or quality standards

**Example clarification for BAB framework:**
\`\`\`
To create an optimized prompt using the BAB framework, I need a few more details:

1. Before: What specific problem or pain point does your audience currently experience?
2. After: What's the ideal outcome after using your product?
3. Bridge: What are the key features or benefits that create this transformation?
4. Target audience: Who exactly are you speaking to?

You can answer in shorthand - just give me the key points.
\`\`\`

**Handle ambiguity:**
If something is unclear or could be interpreted multiple ways:
- Point out the ambiguity
- Suggest 2-3 interpretations
- Ask user to clarify

**Confirm understanding:**
After receiving clarifications, summarize your understanding:
\`\`\`
Got it! Here's what I understand:
- [Key point 1]
- [Key point 2]
- [Key point 3]

Does this capture everything correctly?
\`\`\`

Wait for user confirmation before proceeding.

## Step 5: Prompt Generation

Now generate the optimized prompt following the selected framework's structure.

**Generation process:**

1. **Structure according to framework**: Apply the framework's components and best practices

2. **Incorporate all gathered information**: Weave in all context, requirements, and clarifications

3. **Follow framework best practices**: Reference the examples in the framework file for guidance on style and approach

4. **Add clear instructions**: Make the prompt actionable with specific guidance

5. **Include output formatting**: Specify desired output structure if relevant

**Present the generated prompt:**

\`\`\`
Here's your optimized prompt using the [FRAMEWORK NAME] framework:

---

[THE COMPLETE OPTIMIZED PROMPT]

---

**Framework breakdown:**
- [Component 1]: [What this section does]
- [Component 2]: [What this section does]
- [etc.]

**How to use:**
[Brief usage instructions if needed]

**Expected results:**
[What kind of output to expect]
\`\`\`

**Offer iteration:**
After presenting the prompt, ask:
\`\`\`
Would you like me to:
1. Refine any specific part of this prompt?
2. Try a different framework approach?
3. Create variations for A/B testing?
4. Explain any part of the framework in more detail?
\`\`\`

**Handle refinement requests:**
If user wants changes:
- Make surgical edits to the specific parts mentioned
- Don't regenerate the entire prompt unless necessary
- Explain what was changed and why

## Quality Standards

**All generated prompts should:**
- Be clear and unambiguous
- Include specific, actionable instructions
- Define desired output format when relevant
- Provide necessary context
- Use appropriate language for the target AI system
- Follow the selected framework's structure faithfully
- Be self-contained (not require additional explanation)

**Avoid:**
- Vague or generic instructions
- Unnecessary complexity
- Assuming context not explicitly provided
- Over-constraining when flexibility is valuable

## Multi-Framework Approach

For complex or multifaceted tasks, you may combine multiple frameworks:

**When to consider multiple frameworks:**
- Task has distinct phases (e.g., research → analysis → recommendation)
- User needs both content and structure (e.g., BLOG for content + Hamburger Model for structure)
- Iterative refinement needed (e.g., Zero-shot for exploration + Chain of Thought for analysis)

**How to combine:**
1. Use different frameworks for different sections
2. Apply one framework as the primary structure, another for specific components
3. Create a sequence: first prompt uses Framework A, follow-up uses Framework B

Clearly explain the multi-framework approach to the user.

## Framework Reference Access

Throughout the workflow, read framework details from the references directory:

- **Framework descriptions**: \`references/frameworks/[NUMBER]_[NAME]_Framework.md\`
- **Framework selector guide**: \`references/framework-selector.md\`
- **Complete framework list**: \`references/frameworks-summary.md\`

Always read the specific framework file before generating a prompt to ensure accuracy and adherence to best practices.

## Tips for Effective Guidance

**Tone:**
- Be professional but conversational
- Explain your reasoning briefly
- Don't oversell frameworks - focus on fit and utility

**Efficiency:**
- Ask focused questions, not open-ended ones
- Batch related questions together
- Accept shorthand answers

**Flexibility:**
- If user has strong framework preference, use it
- Adapt the workflow if user wants to skip steps
- Provide alternatives when appropriate

**Education:**
- Briefly explain why a framework fits (helps user learn)
- Point out key framework benefits
- Share relevant examples from the framework file

## Examples

### Example 1: Optimizing an existing prompt

**User:** "Can you help improve this prompt? 'Write a blog post about AI safety'"

**Your response:**
\`\`\`
I'll help optimize this prompt. Let me understand your goals first:

1. Who is the target audience for this blog post?
2. What's the desired tone? (educational, technical, accessible to general public, etc.)
3. What's the approximate length you're targeting?
4. Are there specific AI safety aspects you want to focus on?
5. What should readers take away from this?
\`\`\`

[After receiving answers, match scenario → select framework → generate optimized prompt]

### Example 2: Creating a new prompt from scratch

**User:** "I need a prompt to help me analyze customer feedback data and identify key themes"

**Your response:**
\`\`\`
I can help you create an optimized prompt for customer feedback analysis. This falls into data analysis and insight extraction. Let me ask a few quick questions:

1. What type of feedback data? (surveys, support tickets, reviews, etc.)
2. What format is the data in?
3. What kind of themes are you looking for? (pain points, feature requests, satisfaction drivers, etc.)
4. Do you need quantitative analysis too, or just qualitative themes?

Based on your answers, I'm thinking frameworks like CIDI (for problem diagnosis) or Chain of Thought (for structured analysis) would work well.
\`\`\`

[Continue workflow based on responses]

## Edge Cases

**User provides very vague input:**
- Ask foundational questions to establish basic direction
- Offer 3-4 common use case examples to help them clarify
- Don't proceed with framework selection until you have sufficient clarity

**User asks for multiple unrelated prompts:**
- Process them sequentially
- Offer to handle them one at a time or in parallel
- Each prompt goes through the full workflow

**User wants to learn about frameworks first:**
- Shift to educational mode
- Reference the framework files to explain concepts
- Offer to walk through examples
- Return to optimization workflow when ready

**Framework doesn't quite fit:**
- Acknowledge the imperfect fit
- Explain what modifications or adaptations you'll make
- Consider a hybrid or multi-framework approach
- Ask if user wants to try a different framework instead

## Completion

When the user is satisfied with the generated prompt:
\`\`\`
Great! Your optimized prompt is ready to use.

A few tips:
- Test it with your target AI system and iterate based on results
- You can always come back to refine it further
- Different frameworks might work better for variations of this task

Would you like to:
- Create another prompt?
- Learn more about the framework we used?
- Explore variations of this prompt?
\`\`\`

---

**Remember**: The goal is to create prompts that produce better, more consistent results. Always prioritize clarity, specificity, and alignment with user goals over complexity or framework adherence.
