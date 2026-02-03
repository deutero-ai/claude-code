---
name: qualitative-research
description: Conduct user research, customer development, polling or sociological studies using Deutero. Use when gathering user requirements, running qualitative interview-based studies, or generating product requirements from user interview data.
argument-hint: [study-topic or survey-id]
allowed-tools: MCP, Read, Write, Edit, Bash
model: sonnet
context: fork
---

# Qualitative Research with Deutero

You are conducting a qualitative interview-based research study using the Deutero platform. This skill guides you through the complete research workflow: study creation, question design, persona generation, interview simulation, thematic analysis, and requirements documentation.

## Study Topic

$ARGUMENTS

## Study Type Selection

The `create_study` tool supports four study types. **Select the type that best fits the user's research goal**, then collect only the fields required for that type. If the user's intent is ambiguous, ask which type applies before proceeding.

| Study Type | When to Use | Required Fields |
|------------|-------------|-----------------|
| **user_experience** | UX research, product usability, design validation, understanding user behavior with products/features | `business_context`, `research_need`, `target_users`, `constraints` |
| **sociology** | Academic/social research, understanding populations, exploring phenomena in context | `research_question`, `population_of_interest`, `context_or_setting`, `key_concepts`, `scope_and_boundaries` |
| **customer_development** | Customer discovery, validating problem-solution fit, testing assumptions, lean startup research | `problem_hypothesis`, `customer_segment`, `solution_concept`, `key_assumptions`, `success_criteria` |
| **polling** | Opinion surveys, sentiment research, geographic or demographic snapshots, data quality–focused studies | `research_question`, `population_segment`, `geographic_scope`, `survey_context`, `data_quality_requirements` |

### Field Definitions by Type

**user_experience**
- `business_context`: Overview of the business or product
- `research_need`: What problem or question the research must address
- `target_users`: Primary audience or user segment under study
- `constraints`: Timeline, budget, access, or other limitations

**sociology**
- `research_question`: The central research question
- `population_of_interest`: Who or what population is being studied
- `context_or_setting`: Where or under what conditions
- `key_concepts`: Important theoretical or conceptual terms
- `scope_and_boundaries`: Limits and scope of the study

**customer_development**
- `problem_hypothesis`: Assumed problem or pain point to validate
- `customer_segment`: Target customer segment
- `solution_concept`: Proposed solution being tested
- `key_assumptions`: Main assumptions to validate
- `success_criteria`: What would indicate validation

**polling**
- `research_question`: The question(s) the poll aims to answer
- `population_segment`: Target demographic or population
- `geographic_scope`: Region or geography of interest
- `survey_context`: When, where, or how the survey is administered
- `data_quality_requirements`: Sampling, validity, or quality requirements

### Selection Guidance

- **UX/product teams**: Usually `user_experience`
- **Academic/research**: Usually `sociology`
- **Startups/validation**: Usually `customer_development`
- **Opinion/sentiment polls**: Usually `polling`

If the user does not specify a type, `create_study` will elicit it interactively. You can proactively ask or infer from phrases like "UX study," "customer discovery," "survey," or "poll."

## Research Workflow

Follow this structured approach to conduct qualitative interview-based research:

### Phase 1: Study Design & Creation

**Step 1: Select study type and define the study**
- If a survey_id is provided in arguments or exists in your notes on this task, skip to Phase 2
- Otherwise, use `create_study` MCP tool:
  1. **Choose study type** from the table above (user_experience, sociology, customer_development, polling)
  2. **Provide only the required fields** for that type (see Field Definitions)
  3. Optionally set `language` (default: English)

**Example — user_experience:**
```
business_context: SaaS dashboard product; research_need: understand why users churn; target_users: power users aged 25-45; constraints: 2-week timeline, 10 participants
```

**Example — customer_development:**
```
problem_hypothesis: Small teams struggle with project visibility; customer_segment: 5-20 person teams; solution_concept: Real-time status dashboard; key_assumptions: Teams will pay for visibility; success_criteria: 5+ teams say they would pay
```

**Step 2: Review and save study details**
- Create `{study-name}-study.xml` file with the returned XML content
- Use the study name from the API response for the filename (sanitize for filesystem)
- Present the structured study details to the user:
  - Study name and description
  - Research questions (formatted as numbered list)
  - Research objectives (formatted as numbered list)
  - Study URL for reference

**Step 3: Get user approval**
- Inform user to review the study details in the Deutero dashboard at the link provided and make any changes needed
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

### Phase 3: Recruitment OR Persona Generation & Interview Simulation

Ask the user if they want to conduct interviews with human participants or simulate responses first. Simulating a few interviews first is recommended to identify any issues with the questions and ensure the data gathered is relevant.

Tell the user they can visit https://dashboard.deutero.ai/recruit/?survey_id=${survey_id} to customize the short URL for the study, download a QR code with the link and get help with participant recruitment messages.

If the user only wants to conduct interviews with humans, wait until the interviews are complete. You can use the `get_survey_participation` tool to check how many interviews have been completed.

**Simulation Step 1: Generate personas**
- Use `create_simulation_persona` MCP tool with:
  - survey_id: From previous phases
  - number_of_personas: 
    - 3-5 for quick studies
    - 6-8 for comprehensive research
    - 10+ for large-scale studies (ask user)
  - additional_instructions: Specify diversity requirements

**Simulation Step 2: Present personas**
- Show the persona descriptions clearly
- Note the persona_id for each (needed for simulations)

**Simulation Step 3: Run interview simulations**
- Use `simulate_interviews` MCP tool for each persona:
  - survey_id: Current study
  - persona_id: From persona generation
- Can run multiple in sequence or suggest running in background
- Provide transcript_url for each completed interview
- Inform user that simulations take a few minutes to complete

**Step 4: Confirm completion**
- Verify enough interview simulations are complete before proceeding to analysis
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

**Step 2b: Retrieve analysis results (optional)**
- When the user needs raw analysis XML:
  - **Single interview, specific phase**: Use `get_interview_analysis_results` with `interview_id` and `phase`. Phases: `initial_engagement`, `initial_noting`, `emergent_themes`, `connections`. Phase is elicited if not provided.
  - **Cross-case (Phase 5) for the survey**: Use `get_survey_analysis_results` with `survey_id` to get the synthesized cross-case XML.
- Save XML to files (e.g. `{study-name}-interview-{id}-{phase}.xml`, `{study-name}-cross-case.xml`) if the user wants to review or reuse it.

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

4. **Optional: analysis XML files**
   - Use `get_interview_analysis_results` for per-interview, per-phase XML (e.g. `{study-name}-interview-{id}-emergent_themes.xml`)
   - Use `get_survey_analysis_results` for cross-case XML (e.g. `{study-name}-cross-case.xml`)
   - Create when user needs raw analysis output for review, export, or integration

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
- Use `get_interview_analysis_results` when the user needs XML for a specific interview and phase (e.g. emergent_themes); phase is elicited if omitted
- Use `get_survey_analysis_results` when the user needs the cross-case synthesis XML (Phase 5) for the whole study

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


## Quality Checklist

Before completing the research study, verify:

- [ ] Study type selected matches user's research goal (user_experience, sociology, customer_development, polling)
- [ ] All required fields for the chosen study type were provided
- [ ] Study has clear, specific research questions
- [ ] Questions are open-ended and unbiased
- [ ] Personas represent diverse user segments
- [ ] All interviews completed successfully
- [ ] Analysis used appropriate model tier and runs
- [ ] Interview or survey analysis XML retrieved and saved if user requested raw output
- [ ] Requirements document generated and saved
- [ ] Key findings clearly communicated
- [ ] Recommendations are actionable and prioritized
- [ ] All files saved with appropriate naming
- [ ] User has URLs for manual review/editing

## When to Use This Skill

**Use this skill when:**
- Gathering user requirements for new features (user_experience)
- Understanding user pain points or barriers (user_experience)
- Validating design decisions with user feedback (user_experience)
- Conducting UX research on existing products (user_experience)
- Validating problem-solution fit or customer assumptions (customer_development)
- Generating product requirements from user insights (user_experience)
- Exploring user needs for market opportunities (customer_development)
- Investigating adoption or engagement issues (user_experience)
- Academic or social research on populations (sociology)
- Opinion polls or sentiment surveys (polling)

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