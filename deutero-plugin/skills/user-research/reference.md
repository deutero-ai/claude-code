# Deutero MCP Tools - Quick Reference

This reference documents all available Deutero MCP tools for user research.

## Available Tools

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `create_study` | Initialize research study | Start of any new research project |
| `create_study_questions` | Generate interview questions | After study approval |
| `create_simulation_persona` | Generate user personas | Before running interviews |
| `simulate_interviews` | Run simulated interviews | After personas created |
| `run_thematic_analysis` | Analyze interview transcripts | After interviews complete |
| `get_analysis_status` | Check analysis progress | Monitor long-running analysis |
| `get_agent_requirements` | Generate requirements doc | After analysis completes |
| `get_survey_participation` | Get interview statistics | Monitor interview completion |

---

## Tool Details

### create_study

**Purpose:** Create a new user research study framework

**Parameters:**
- `business_context` (string): Business situation and background
- `research_need` (string): Specific problem to investigate
- `target_users` (string): Description of target user population
- `constraints` (string): Timeline, budget, access limitations

**Returns:**
```json
{
  "study_id": "uuid",
  "study_name": "string",
  "study_description": "string",
  "research_questions": ["string"],
  "research_objectives": ["string"],
  "url": "string",
  "xml_file": "string"
}
```

**Example:**
```json
{
  "business_context": "E-commerce platform with 68% cart abandonment rate",
  "research_need": "Understand why users abandon during checkout",
  "target_users": "Online shoppers who added items but didn't complete purchase",
  "constraints": "Need results within 2 weeks for Q2 planning"
}
```

**Next Steps After Calling:**
1. Save `xml_file` content to `{study-name}-study.xml`
2. Present research questions and objectives to user
3. Wait for user approval before proceeding

---

### create_study_questions

**Purpose:** Generate interview questions for a study

**Parameters:**
- `survey_id` (string, required): UUID from create_study
- `number_of_questions` (int): 1-25, default 10
- `additional_instructions` (string, optional): Focus areas or special requirements

**Returns:**
```json
{
  "survey_id": "uuid",
  "question_list": ["string"],
  "edit_questions_url": "string",
  "interview_url": "string",
  "xml_file": "string"
}
```

**Best Practices:**
- 5-7 questions: Quick studies or focused topics
- 8-10 questions: Standard research
- 10-12 questions: Comprehensive studies
- Always test interview flow at `interview_url` before simulations

**Next Steps After Calling:**
1. Update or create XML file with question list
2. Present questions to user
3. Provide `edit_questions_url` and `interview_url`
4. Wait for user approval

---

### create_simulation_persona

**Purpose:** Generate user personas for interview simulation

**Parameters:**
- `survey_id` (string, required): UUID of the study
- `number_of_personas` (int): 1-25, default 1
- `additional_instructions` (string, optional): Diversity or characteristic requirements

**Returns:**
```json
{
  "survey_id": "uuid",
  "personas": [
    {
      "persona": "string (description)",
      "persona_id": "string"
    }
  ]
}
```

**Persona Count Guidelines:**
- 3-5: Quick validation studies
- 6-8: Standard comprehensive research
- 10-15: Large-scale or high-diversity needs
- 15-25: Market research or extensive segmentation

**Next Steps After Calling:**
1. Present persona descriptions to user
2. Note each persona_id (needed for simulations)
3. Proceed to simulate_interviews

---

### simulate_interviews

**Purpose:** Run a simulated interview for a specific persona

**Parameters:**
- `survey_id` (string, required): UUID of the study
- `persona_id` (string, required): ID from create_simulation_persona

**Returns:**
```json
{
  "survey_id": "uuid",
  "persona_id": "string",
  "transcript_url": "string"
}
```

**Important Notes:**
- Call once per persona (loop through all persona_ids)
- Each interview takes ~3-5 minutes to complete
- Can run multiple in sequence or parallel
- Save transcript_url for reference
- Check completion with get_survey_participation before analysis

**Next Steps After Calling:**
1. Note transcript_url for each interview
2. Wait for all interviews to complete
3. Verify completion with get_survey_participation
4. Proceed to run_thematic_analysis

---

### run_thematic_analysis

**Purpose:** Analyze interview transcripts and identify themes

**Parameters:**
- `survey_id` (string): Analyze all interviews for this study (recommended)
- `interview_id` (string): Analyze single specific interview
  - ⚠️ Provide exactly one: survey_id OR interview_id
- `model_tier` (string): Analysis quality level
  - `open_weights` (default): Cost-effective, good quality
  - `premium`: Better quality, more nuanced analysis
  - `frontier`: Highest quality, best for critical decisions
- `num_runs` (int): 1-5, default 1
  - More runs = more robust findings
  - Recommended: 3-4 for important studies

**Returns:**
```json
{
  "success": true,
  "interviews_queued": 6,
  "interviews": [
    {
      "interview_id": "uuid",
      "survey_id": "uuid"
    }
  ],
  "message": "string"
}
```

**Analysis Runs in Background:**
- Returns immediately
- Use get_analysis_status to monitor progress
- Can take several minutes depending on interview count and num_runs

**Model Tier Selection:**
- **open_weights**: Quick insights, directional findings, budget-conscious
- **premium**: Standard research, balanced quality/cost
- **frontier**: Critical business decisions, complex synthesis needed

**Next Steps After Calling:**
1. Inform user analysis is running in background
2. Monitor with get_analysis_status
3. When complete, call get_agent_requirements

---

### get_analysis_status

**Purpose:** Check progress and status of thematic analysis

**Parameters:**
- `survey_id` (string): Check status for all interviews in survey
- `interview_id` (string): Check status for specific interview
  - ⚠️ Provide exactly one: survey_id OR interview_id

**Returns:**
```json
{
  "survey_id": "uuid",
  "total_interviews": 6,
  "interviews": [
    {
      "interview_id": "uuid",
      "survey_id": "uuid",
      "phase_completion": {
        "phase_name": "completed"
      },
      "runs": [
        {
          "run_id": "uuid",
          "status": "completed",
          "metadata": {}
        }
      ]
    }
  ]
}
```

**Phase Completion States:**
- `not_started`: Analysis hasn't begun
- `in_progress`: Currently processing
- `completed`: Analysis finished
- `failed`: Error occurred

**Usage:**
- Call periodically while waiting for analysis
- Check all interviews show `completed` status
- Verify all runs completed successfully

---

### get_agent_requirements

**Purpose:** Generate LLM-optimized requirements document from analysis

**Parameters:**
- `survey_id` (string, required): UUID of the analyzed study

**Returns:**
```json
{
  "survey_id": "uuid",
  "markdown": "string (full requirements document)",
  "filename": "string"
}
```

**Document Contents:**
- Executive summary of findings
- User needs with evidence from interviews
- Technical requirements for development
- Implementation priorities
- Expected outcomes and metrics

**Next Steps After Calling:**
1. Save `markdown` content to `{filename}` or `{study-name}-requirements.md`
2. Present key findings to user
3. Provide file location for full details
4. Suggest next steps (implementation, follow-up research, etc.)

---

### get_survey_participation

**Purpose:** Get interview completion statistics for a study

**Parameters:**
- `survey_id` (string, required): UUID of the study

**Returns:**
```json
{
  "survey_id": "uuid",
  "total_interviews": 8,
  "completed_interviews": 6,
  "incomplete_interviews": 2,
  "max_responses": 10,
  "completion_rate": 0.75,
  "quota_fill_rate": 0.6,
  "quota_remaining": 4
}
```

**When to Use:**
- After running simulations to verify completion
- Before running analysis (ensure all complete)
- To monitor progress during simulations
- To check quota status if max_responses set

**Key Metrics:**
- `completion_rate`: Percentage of started interviews that finished
- `quota_fill_rate`: Progress toward max_responses (if set)
- Should see completion_rate = 1.0 before analysis

---

## Common Workflows

### Full Research Study
```
1. create_study
   ↓
2. [User reviews XML file]
   ↓
3. create_study_questions
   ↓
4. [User tests interview at interview_url]
   ↓
5. create_simulation_persona
   ↓
6. simulate_interviews (for each persona)
   ↓
7. get_survey_participation (verify completion)
   ↓
8. run_thematic_analysis
   ↓
9. get_analysis_status (monitor)
   ↓
10. get_agent_requirements
```

### Quick Validation
```
1. create_study (focused topic)
   ↓
2. create_study_questions (5-7 questions)
   ↓
3. create_simulation_persona (3-4 personas)
   ↓
4. simulate_interviews
   ↓
5. run_thematic_analysis (2 runs, open_weights)
   ↓
6. get_agent_requirements
```

### Resume Existing Study
```
1. Identify phase from files/status
   ↓
2. Call appropriate tool to continue
   (e.g., if questions exist but no personas,
    start with create_simulation_persona)
```

---

## Error Handling

### Missing Parameters
- Tools will elicit missing required parameters interactively
- Provide clear, specific values when prompted

### Invalid UUIDs
- Verify format: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
- Check survey_id/interview_id from previous tool responses

### API Errors
- 401 Unauthorized: Check API key configuration
- 404 Not Found: Verify survey_id/interview_id exists
- 400 Bad Request: Check parameter values and ranges

### Analysis Issues
- If analysis doesn't complete, check get_analysis_status
- Verify all interviews completed with get_survey_participation
- Check for error messages in status response

---

## Tips for Best Results

### Study Creation
- Be specific in business_context and research_need
- Clearly define target_users with demographics and behaviors
- Include realistic constraints (timeline, budget, access)

### Question Generation
- Start with 8-10 questions for most studies
- Use additional_instructions for focus areas
- Always test the interview flow before simulations

### Persona Generation
- Ensure diversity in demographics and behaviors
- Use additional_instructions to specify segments
- Consider edge cases and underrepresented groups

### Interview Simulation
- Allow adequate time for completion (3-5 min per interview)
- Verify completion before analysis
- Save transcript URLs for reference

### Thematic Analysis
- Use multiple runs (3-4) for robust findings
- Choose model_tier based on study importance
- Analyze entire survey (survey_id) for comprehensive insights
- Monitor status during long-running analysis

### Requirements Generation
- Only call after analysis completes
- Save markdown to appropriately named file
- Use as input for development, design, or product planning

---

## File Naming Conventions

| File Type | Naming Pattern | Example |
|-----------|----------------|---------|
| Study XML | `{study-name}-study.xml` | `checkout-abandonment-study.xml` |
| Requirements | `{study-name}-requirements.md` | `checkout-abandonment-requirements.md` |
| Analysis Summary | `{study-name}-analysis-summary.md` | `checkout-abandonment-analysis-summary.md` |

Sanitize study names for filesystem:
- Lowercase
- Replace spaces with hyphens
- Remove special characters
- Example: "Mobile App Redesign" → "mobile-app-redesign"

---

## URLs Provided by Tools

| URL Type | Tool | Purpose |
|----------|------|---------|
| `url` | create_study | Study overview page |
| `edit_questions_url` | create_study_questions | Manual question editing interface |
| `interview_url` | create_study_questions | Test interview experience |
| `transcript_url` | simulate_interviews | View interview transcript |

Always provide these URLs to users for manual review and testing.
