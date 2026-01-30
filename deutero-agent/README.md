# User Researcher Subagent for Claude Code

A specialized Claude Code subagent for conducting comprehensive user research and UX studies using the Deutero platform.

## Overview

The User Researcher subagent handles the complete user research workflow:

1. **Study Design** - Create research frameworks with clear objectives
2. **Question Development** - Generate targeted interview questions
3. **Data Collection** - Generate personas and simulate interviews at scale
4. **Analysis** - Run thematic analysis on interview transcripts
5. **Documentation** - Generate LLM-optimized requirement documents

## Installation

### Prerequisites

- Claude Code installed and configured
- Deutero MCP server set up and accessible
- API key for Deutero (configured in your MCP settings)

### Install the Subagent

**Option 1: User-level (available in all projects)**
```bash
# Copy to your global Claude agents directory
cp user-researcher.md ~/.claude/agents/
```

**Option 2: Project-level (specific to current project)**
```bash
# Copy to project's .claude directory
mkdir -p .claude/agents
cp user-researcher.md .claude/agents/
```

**Option 3: Use the interactive command**
```bash
# In Claude Code
/agents
# Select "Create new agent" → "Import from file" → select user-researcher.md
```

### Verify Installation

After installation (no restart needed), verify the subagent is available:

```bash
# In Claude Code
/agents
# Look for "user-researcher" in the list
```

## Configuration

### Deutero MCP Server Setup

Ensure your Deutero MCP server is configured in Claude Code settings. You'll need:

1. **Server endpoint** (default: `http://127.0.0.1:8000`)
2. **API key** (passed as X-API-Key header)
3. **MCP tools enabled** in Claude Code

Example MCP configuration (in your Claude Code settings):

```json
{
  "mcpServers": {
    "deutero": {
      "command": "python",
      "args": ["/path/to/deutero_mcp_server.py"],
      "env": {
        "BASE_URL": "http://127.0.0.1:8000"
      }
    }
  }
}
```

### Subagent Customization

You can customize the subagent by editing `user-researcher.md`:

- **Model**: Change from `sonnet` to `opus` or `haiku`
- **Tools**: Restrict or expand available tools
- **Permission mode**: Change from `default` to `acceptEdits` or `dontAsk`
- **System prompt**: Modify the prompt to adjust behavior

## Usage

### Quick Start

The User Researcher subagent activates automatically when you mention user research tasks:

```
# Claude will automatically delegate to user-researcher
"I need to understand why users are struggling with our onboarding flow"
"Create a UX study to gather requirements for our mobile app redesign"
"Run user interviews about our checkout process"
```

### Explicit Invocation

You can also explicitly request the subagent:

```
"Use the user-researcher subagent to create a study about feature adoption"
"Have the user-researcher analyze our interview transcripts"
```

### Complete Workflow Example

```
You: "I need to understand why enterprise customers aren't adopting our new dashboard feature"

Claude: [Delegates to user-researcher subagent]

User Researcher: "I'll create a research study to investigate dashboard adoption challenges.

Let me gather some details:
- Business context: Enterprise SaaS, new dashboard feature launched 3 months ago
- Research need: Understand adoption barriers and feature perception
- Target users: Enterprise customers (IT managers, data analysts)
- Constraints: Need results within 2 weeks, budget for 6-8 interviews

Creating study..."

[Subagent creates study, generates XML file, presents structure]

User Researcher: "Study created! I've saved the details to 
'dashboard-adoption-study.xml'. Please review the research questions 
and objectives. Ready to generate interview questions?"

You: "Yes, create 7 questions"

[Subagent generates questions, updates XML, provides URLs]

User Researcher: "Added 7 questions to the study. You can:
- Edit questions: http://0.0.0.0:8000/edit-survey/?survey_id=<UUID>
- Test interview: http://localhost:8000/?survey_id=<UUID>

Ready to generate personas and run simulations?"

You: "Generate 6 personas and run all interviews"

[Subagent generates personas, simulates interviews, monitors progress]

User Researcher: "All 6 interviews completed! Running thematic analysis 
with 3 runs for robust findings..."

[Subagent runs analysis, monitors status, generates requirements]

User Researcher: "Analysis complete! I've created:
1. dashboard-adoption-study.xml - Full study specification
2. dashboard-adoption-requirements.md - Development requirements

Key findings: [summary of insights]

The requirements document is optimized for your development team."
```

### Common Commands

**Start a study**
```
"Create a user research study about [topic]"
"I need to understand [user problem]"
```

**Generate questions**
```
"Add 8 interview questions to the study"
"Create questions focusing on [specific aspect]"
```

**Run simulations**
```
"Generate 5 personas and simulate interviews"
"Run interviews for study [study_id]"
```

**Analyze results**
```
"Run thematic analysis on the completed interviews"
"Check analysis status for survey [survey_id]"
```

**Get deliverables**
```
"Generate the requirements document"
"Show me the participation statistics"
```

## Workflow Phases

### Phase 1: Study Creation
- Define business context and research need
- Identify target user population
- Set constraints and scope
- **Output**: Study XML file for review

### Phase 2: Question Design
- Generate interview questions
- Review and refine question set
- Test interview flow
- **Output**: Updated XML with questions, URLs for editing/testing

### Phase 3: Data Collection
- Generate diverse user personas
- Simulate interviews at scale
- Monitor completion progress
- **Output**: Interview transcripts, participation stats

### Phase 4: Analysis & Synthesis
- Run multi-run thematic analysis
- Track analysis progress
- Generate findings and insights
- **Output**: Requirements document (markdown)

## Files Created

The subagent creates these files in your working directory:

| File | Description | When Created |
|------|-------------|--------------|
| `{study-name}-study.xml` | Study specification with questions | After study creation and question generation |
| `{study-name}-requirements.md` | LLM-optimized requirements document | After running `get_agent_requirements` |
| `{study-name}-analysis-summary.md` | Optional analysis summary | If requested by user |

All files are saved to your current working directory. The subagent will inform you of file locations.

## Tool Reference

The subagent uses these Deutero MCP tools:

| Tool | Purpose | Required Params |
|------|---------|-----------------|
| `create_study` | Initialize new research study | business_context, research_need, target_users, constraints |
| `create_study_questions` | Generate interview questions | survey_id, number_of_questions |
| `create_simulation_persona` | Generate user personas | survey_id, number_of_personas |
| `simulate_interviews` | Run simulated interviews | survey_id, persona_id |
| `run_thematic_analysis` | Analyze interview transcripts | survey_id OR interview_id, model_tier, num_runs |
| `get_analysis_status` | Check analysis progress | survey_id OR interview_id |
| `get_agent_requirements` | Generate requirements doc | survey_id |
| `get_survey_participation` | Get participation stats | survey_id |

## Best Practices

### Study Design
- Keep studies focused (single problem space)
- Define 3-5 clear research questions
- Be specific about target users
- Include realistic constraints

### Question Creation
- Use 5-10 questions for most studies
- Mix behavioral and attitudinal questions
- Avoid leading questions
- Test the interview flow before simulation

### Persona Generation
- Generate 3-8 personas for balanced coverage
- Ensure demographic and behavioral diversity
- Consider edge cases and underrepresented segments
- Use additional_instructions for specificity

### Analysis
- Run 3-5 analysis runs for important studies
- Start with 'open_weights' tier (cost-effective)
- Use 'premium' or 'frontier' for complex analysis needs
- Analyze entire surveys (not individual interviews) for comprehensive insights

### Collaboration
- Share XML files with team for review
- Use provided URLs for manual editing/testing
- Version control the XML and requirements files
- Keep stakeholders informed at each phase

## Troubleshooting

### Subagent Not Activating

If Claude doesn't delegate to the subagent:
1. Verify installation: `/agents` and check for "user-researcher"
2. Be explicit: "Use the user-researcher subagent to..."
3. Check that MCP tools are enabled in Claude Code
4. Restart Claude Code if you just installed the subagent

### MCP Connection Issues

If tools fail with connection errors:
1. Verify Deutero server is running: `curl http://127.0.0.1:8000/health`
2. Check API key is configured in MCP settings
3. Confirm MCP server configuration in Claude Code settings
4. Check server logs for authentication errors

### Missing XML Files

If the subagent can't find XML files:
1. Check your working directory
2. Search for files containing the survey_id UUID
3. The subagent creates files with sanitized study names
4. Ask the subagent to recreate the file if lost

### Analysis Not Completing

If thematic analysis seems stuck:
1. Use `get_analysis_status` to check progress
2. Confirm interviews are actually completed: `get_survey_participation`
3. Check server logs for processing errors
4. Analysis can take several minutes for multiple interviews

## Advanced Usage

### Background Execution

Run simulations in the background while working:
```
"Run all interview simulations in the background"
# Or press Ctrl+B when the subagent is running simulations
```

### Custom Model Tiers

For complex studies, use premium analysis:
```
"Run thematic analysis using the frontier tier with 5 runs"
```

### Parallel Research

Run multiple studies simultaneously:
```
"Create three separate studies: one for mobile users, one for desktop users, 
and one for API customers"
```

### Resume Previous Work

Resume a subagent session to continue work:
```
"Resume the user-researcher work and generate the requirements document 
for study [survey_id]"
```

## Integration with Development Workflow

### 1. Requirements Gathering
```
Research Study → Interview Simulation → Thematic Analysis → Requirements.md
```

The `requirements.md` file is optimized for LLM coding agents and can be used directly in development tasks.

### 2. Feature Validation
```
Prototype → User Testing Study → Analysis → Refinement Requirements
```

Run studies to validate feature designs before full development.

### 3. Continuous Discovery
```
Regular Studies → Trend Analysis → Roadmap Updates
```

Maintain a cadence of research studies to inform product direction.

## Support & Resources

- **Deutero Documentation**: [https://www.deutero.ai/docs](https://www.deutero.ai/docs)
- **Claude Code Docs**: [https://code.claude.com/docs](https://code.claude.com/docs)
- **Subagent Guide**: [https://code.claude.com/docs/en/create-custom-subagents](https://code.claude.com/docs/en/create-custom-subagents)

## License

This subagent configuration is provided as-is for use with Claude Code and Deutero.

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────────┐
│                  USER RESEARCHER SUBAGENT                   │
├─────────────────────────────────────────────────────────────┤
│ INSTALLATION                                                │
│   cp user-researcher.md ~/.claude/agents/                   │
│                                                             │
│ ACTIVATION                                                  │
│   "Create a UX study about [topic]"                        │
│   "Use user-researcher to analyze interviews"              │
│                                                             │
│ WORKFLOW                                                    │
│   1. Create Study       → XML file                         │
│   2. Generate Questions → Updated XML + URLs               │
│   3. Run Simulations    → Interview transcripts            │
│   4. Analyze Results    → Requirements.md                  │
│                                                             │
│ KEY FILES                                                   │
│   {study-name}-study.xml        - Study specification      │
│   {study-name}-requirements.md  - Dev requirements         │
│                                                             │
│ COMMON TASKS                                                │
│   Check status:  "Show participation stats"                │
│   Edit study:    Use edit_questions_url from output        │
│   Test flow:     Use interview_url from output             │
│   Resume work:   "Continue the previous study analysis"    │
└─────────────────────────────────────────────────────────────┘
```
