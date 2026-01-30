---
name: user-research
description: Conduct user research studies using Deutero. Use when gathering user requirements, running UX studies, conducting interviews, analyzing user feedback, or generating product requirements from user insights.
argument-hint: [study-topic or survey-id]
allowed-tools: MCP, Read, Write, Edit, Bash
model: sonnet
context: fork
agent: Plan
---

# User Research with Deutero

You are conducting a user research study using the Deutero platform. This skill guides you through the complete research workflow: study creation, question design, persona generation, interview simulation, thematic analysis, and requirements documentation.

## Study Topic

$ARGUMENTS

## Research Workflow

Follow this structured approach to conduct comprehensive user research:

### Phase 1: Study Design & Creation

**Step 1: Define the study**
- If a survey_id is provided in arguments, skip to Phase 2
- Otherwise, use `create_study` MCP tool with:
  - business_context: What is the business situation?
  - research_need: What specific problem needs investigation?
  - target_users: Who are we researching?
  - constraints: Timeline, budget, or access limitations

**Step 2: Review and save study details**
- Create `{study-name}-study.xml` file with the returned XML content
- Use the study name from the API response for the filename (sanitize for filesystem)
- Present the structured study details to the user:
  - Study name and description
  - Research questions (formatted as numbered list)
  - Research objectives (formatted as numbered list)
  - Study URL for reference

**Step 3: Get user approval**
- Inform user to review the XML file and make any changes needed
- Wait for explicit confirmation before proceeding to question generation

### Phase 2: Interview Question Design

**Step 1: Generate questions**
- Use `create_study_questions` MCP tool with:
  - survey_id: From Phase 1 or provided in arguments
  - number_of_questions: 5-10 for most studies (ask user preference)
  - additional_instructions: Any specific focus areas

**Step 2: Update documentation**
- Check if `{study-name}-study.xml` exists (search for survey_id UUID in filenames)
- If exists: Edit the file to add the question list
- If not exists: Create new XML file with complete study + questions
- Present questions to user as a numbered list

**Step 3: Provide review resources**
- Share edit_questions_url for manual editing
- Share interview_url for testing the interview flow
- Encourage user to test before running simulations

**Step 4: Get approval**
- Wait for user confirmation that questions are finalized

### Phase 3: Persona Generation & Interview Simulation

**Step 1: Generate personas**
- Use `create_simulation_persona` MCP tool with:
  - survey_id: From previous phases
  - number_of_personas: 
    - 3-5 for quick studies
    - 6-8 for comprehensive research
    - 10+ for large-scale studies (ask user)
  - additional_instructions: Specify diversity requirements

**Step 2: Present personas**
- Show the persona descriptions clearly
- Note the persona_id for each (needed for simulations)

**Step 3: Run interview simulations**
- Use `simulate_interviews` MCP tool for each persona:
  - survey_id: Current study
  - persona_id: From persona generation
- Can run multiple in sequence or suggest running in background
- Provide transcript_url for each completed interview
- Inform user that simulations take a few minutes to complete

**Step 4: Monitor progress**
- Use `get_survey_participation` MCP tool to check:
  - Total interviews
  - Completed vs incomplete
  - Completion rate
  - Quota status (if applicable)
- Update user on progress periodically

**Step 5: Confirm completion**
- Verify all interviews are complete before proceeding to analysis
- If any are incomplete, wait or investigate issues

### Phase 4: Thematic Analysis

**Step 1: Run analysis**
- Use `run_thematic_analysis` MCP tool with:
  - survey_id: Analyze all interviews for this study
  - model_tier: 
    - 'open_weights' (default, cost-effective)
    - 'premium' (better quality)
    - 'frontier' (highest quality for critical studies)
  - num_runs: 
    - 1-2 for quick insights
    - 3-4 for robust findings (recommended)
    - 5 for critical business decisions

**Step 2: Monitor analysis**
- Inform user that analysis runs in background
- Use `get_analysis_status` MCP tool to check progress:
  - Shows phase completion for each interview
  - Shows run metadata
- Update user when analysis completes

**Step 3: Generate requirements document**
- Use `get_agent_requirements` MCP tool with survey_id
- Save the returned markdown to `{study-name}-requirements.md`
- This document is optimized for LLM coding agents

**Step 4: Present findings**
- Summarize key insights from the analysis
- Highlight critical user needs and pain points
- Provide actionable recommendations
- Direct user to the requirements document for full details

## File Management

Create and maintain these files throughout the workflow:

1. **`{study-name}-study.xml`**
   - Created after study creation
   - Updated after question generation
   - Contains complete study specification
   - User can edit manually between phases

2. **`{study-name}-requirements.md`**
   - Created after analysis completes
   - LLM-optimized requirements document
   - Ready for development team use

3. **Optional: `{study-name}-analysis-summary.md`**
   - Create if user requests a summary
   - Include key findings, quotes, recommendations

## Best Practices

### Study Scope
- Keep studies focused on a single problem area
- Define 3-5 clear research questions
- Be specific about target user characteristics
- Include realistic constraints (time, budget, access)

### Question Design
- Use 5-10 questions for most studies
- Mix behavioral ("Tell me about a time...") and attitudinal ("What do you think about...") questions
- Avoid leading questions
- Use open-ended format for rich qualitative data
- Test interview flow before running simulations

### Persona Generation
- 3-5 personas: Quick studies or focused user segments
- 6-8 personas: Comprehensive research with diverse users
- 10+ personas: Large-scale studies or when representing many segments
- Use additional_instructions to ensure:
  - Demographic diversity
  - Behavioral diversity
  - Edge cases and underrepresented groups
  - Relevant domain expertise levels

### Interview Simulation
- Allow 3-5 minutes per interview for completion
- Check participation stats before running analysis
- Save transcript URLs for reference and validation

### Analysis
- Use multiple runs (3-5) for important studies
- Start with 'open_weights' tier for cost efficiency
- Escalate to 'premium' or 'frontier' if needed for complex analysis
- Analyze entire survey (survey_id) rather than individual interviews

### Communication
- Explain what you're doing at each phase
- Provide progress updates during long operations
- Present structured data clearly (use tables or lists)
- Always include URLs and file locations
- Summarize findings and suggest next steps

## Error Handling

- If MCP tool returns an error, explain to user and suggest solutions
- If missing required parameters, tools will elicit them interactively
- Validate UUIDs before passing to tools (survey_id, interview_id, persona_id)
- Check for existing XML files before creating new ones
- Confirm user approval before starting simulations or analysis

## String Substitutions

- `$ARGUMENTS`: Study topic, survey_id, or specific instructions
- `$ARGUMENTS[0]` or `$0`: First argument (e.g., survey_id)
- `$ARGUMENTS[1]` or `$1`: Second argument (e.g., number of personas)
- `${CLAUDE_SESSION_ID}`: Current session ID for logging/tracking

## Example Invocations

### By user (explicit)
```
/user-research checkout abandonment issues
/user-research abc-123-def (resume existing study)
/user-research mobile app redesign with 8 personas
```

### By Claude (automatic)
When user says things like:
- "I need to understand why users are leaving during checkout"
- "Let's run a UX study on our onboarding flow"
- "Can you help me gather requirements from user interviews?"
- "I want to research feature adoption barriers"

## Output Format

Present findings in this structure:

### Study Overview
- Study name and description
- Research questions
- Target users
- Constraints

### Interview Results
- Number of personas/interviews
- Completion statistics
- Key themes identified

### Key Findings
1. **[Theme 1]**: Description and evidence
2. **[Theme 2]**: Description and evidence
3. **[Theme 3]**: Description and evidence

### Recommendations
1. [Actionable recommendation with rationale]
2. [Actionable recommendation with rationale]
3. [Actionable recommendation with rationale]

### Files Created
- `{study-name}-study.xml` - Full study specification
- `{study-name}-requirements.md` - Development requirements

### Next Steps
- Suggested follow-up actions
- Additional research needs (if any)
- Implementation priorities

## Quality Checklist

Before completing the research study, verify:

- [ ] Study has clear, specific research questions
- [ ] Questions are open-ended and unbiased
- [ ] Personas represent diverse user segments
- [ ] All interviews completed successfully
- [ ] Analysis used appropriate model tier and runs
- [ ] Requirements document generated and saved
- [ ] Key findings clearly communicated
- [ ] Recommendations are actionable and prioritized
- [ ] All files saved with appropriate naming
- [ ] User has URLs for manual review/editing

## When to Use This Skill

**Use this skill when:**
- Gathering user requirements for new features
- Understanding user pain points or barriers
- Validating design decisions with user feedback
- Conducting UX research on existing products
- Generating product requirements from user insights
- Exploring user needs for market opportunities
- Investigating adoption or engagement issues

**Don't use this skill when:**
- User wants quantitative analysis (use analytics tools)
- Need is for competitive research without user involvement
- Request is for technical documentation (use code analysis)
- User wants market research or financial analysis

## Integration with Development

The requirements document produced by this skill is optimized for:
- LLM coding agents (clear, structured, actionable)
- Product managers (user-centric, prioritized)
- Development teams (technical requirements with user context)
- Design teams (UX improvements with user evidence)

Use the requirements document to:
1. Create feature specifications
2. Write user stories
3. Prioritize backlog items
4. Design user interfaces
5. Plan product roadmap
6. Validate assumptions

## Workflow Variations

### Quick Study (1-2 hours)
- 3-5 personas
- 5 questions
- 2 analysis runs
- 'open_weights' tier

### Standard Study (half day)
- 6-8 personas  
- 8-10 questions
- 3-4 analysis runs
- 'premium' tier for complex topics

### Comprehensive Study (full day)
- 10+ personas
- 10-12 questions
- 4-5 analysis runs
- 'frontier' tier for critical decisions
- Additional analysis summaries

## Remember

- Always save XML files for user review
- Provide URLs at every phase
- Get user approval before proceeding to next phase
- Present findings clearly and actionably
- Focus on insights that drive decisions
- Keep the user informed of progress throughout
