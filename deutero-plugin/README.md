# User Research Skill for Claude Code

A comprehensive Claude Code skill for conducting user research studies using the Deutero platform. This skill provides structured workflows for UX research, requirements gathering, and qualitative user studies.

## Overview

The user-research skill guides you through the complete research workflow:

1. **Study Design** - Create research frameworks with clear objectives
2. **Question Development** - Generate targeted interview questions
3. **Persona Generation** - Create diverse, realistic user personas
4. **Data Collection** - Simulate interviews at scale
5. **Thematic Analysis** - Identify patterns and themes
6. **Requirements Documentation** - Generate LLM-optimized requirements

## Installation

### Prerequisites

- Claude Code installed and configured
- Deutero MCP server set up and accessible
- API key for Deutero (configured in MCP settings)

### Install the Skill

**Option 1: Personal (available in all your projects)**
```bash
# Create the skill directory
mkdir -p ~/.claude/skills/user-research

# Copy all files
cp SKILL.md ~/.claude/skills/user-research/
cp examples.md ~/.claude/skills/user-research/
cp reference.md ~/.claude/skills/user-research/
```

**Option 2: Project-specific**
```bash
# Create the skill directory in your project
mkdir -p .claude/skills/user-research

# Copy all files
cp SKILL.md .claude/skills/user-research/
cp examples.md .claude/skills/user-research/
cp reference.md .claude/skills/user-research/
```

**Option 3: Via Claude Code**
```bash
# In Claude Code, copy the directory, then:
Ask Claude: "Install the user-research skill from the user-research-skill directory"
```

### Verify Installation

The skill is available immediately (no restart needed):

```bash
# In Claude Code, check available skills:
What skills are available?

# Or invoke directly:
/user-research
```

You should see "user-research" in the available skills list.

## Quick Start

### Automatic Invocation (Recommended)

Claude automatically uses the skill when you ask about user research:

```
"I need to understand why users are abandoning our checkout process"
"Let's run a UX study on the mobile app onboarding"
"Help me gather requirements for the new dashboard feature"
```

### Manual Invocation

You can also invoke the skill directly:

```
/user-research checkout abandonment issues
/user-research mobile app redesign with 8 personas
/user-research validate search feature design
```

### With Existing Study

Resume work on an existing study by providing the survey_id:

```
/user-research abc-123-def-456-789
```

## Usage

### Basic Workflow

1. **Start a study**
   ```
   /user-research [topic or problem statement]
   ```

2. **Follow the prompts**
   - The skill will guide you through each phase
   - Review and approve at each checkpoint
   - Test interview flow before simulations

3. **Get results**
   - Analysis runs automatically after interviews
   - Requirements document generated for development team
   - All files saved in working directory

### Example Session

```
You: /user-research why users aren't using our new feature

Skill: I'll create a study to investigate feature adoption barriers.

[Gathers context about business, users, constraints]
[Creates study and saves to XML file]

Study created! Please review new-feature-adoption-study.xml

Research Questions:
1. How did users first discover the new feature?
2. What prevented them from trying it?
3. For those who tried it, what was the experience?
4. What would increase feature usage?
5. How does it compare to existing workflows?

Ready to generate interview questions?

You: Yes, create 8 questions

[Generates questions, provides URLs for editing/testing]
[Continues through persona generation, simulations, analysis]

Analysis complete! Created:
- new-feature-adoption-study.xml
- new-feature-adoption-requirements.md

Key findings:
1. 60% weren't aware feature existed
2. Those who tried found onboarding confusing
3. Value proposition unclear

[Provides detailed recommendations]
```

## Skill Structure

### Main File (SKILL.md)

The main skill instructions that Claude follows when conducting research. Contains:
- Complete workflow phases
- Best practices for each step
- Error handling and validation
- Output formatting guidelines

### Supporting Files

**examples.md** - Real-world usage examples
- Full study walkthroughs
- Common usage patterns
- Expected outputs
- File structure examples

**reference.md** - Deutero MCP tool documentation
- Detailed tool parameters
- Return value structures
- Best practices for each tool
- Common workflows and error handling

Claude loads these files when needed for additional context.

## Configuration

### Customize the Skill

Edit `SKILL.md` frontmatter to adjust behavior:

```yaml
---
name: user-research
description: Conduct user research studies...
argument-hint: [study-topic or survey-id]
allowed-tools: MCP, Read, Write, Edit, Bash
model: sonnet
---
```

**Available customizations:**
- `model`: Change to `opus` for more sophisticated analysis or `haiku` for faster execution
- `allowed-tools`: Restrict which tools the skill can use
- `disable-model-invocation: true`: Prevent automatic activation (manual only)
- `user-invocable: false`: Hide from `/` menu (Claude can still use it)

### Restrict Skill Access

Prevent Claude from using the skill automatically:

**In skill frontmatter:**
```yaml
disable-model-invocation: true  # Only manual invocation
```

**In permissions (`.claude/settings.json`):**
```json
{
  "permissions": {
    "deny": ["Skill(user-research)"]
  }
}
```

## Features

### Workflow Phases

**Phase 1: Study Design**
- Interactive context gathering
- Research question generation
- Study specification in XML format
- User review and approval gates

**Phase 2: Question Development**
- Targeted interview question generation
- Question editing interface URLs
- Interview flow testing
- Iterative refinement support

**Phase 3: Data Collection**
- Diverse persona generation
- Automated interview simulations
- Progress monitoring
- Completion verification

**Phase 4: Analysis & Requirements**
- Multi-run thematic analysis
- Theme identification and synthesis
- LLM-optimized requirements generation
- Actionable recommendations

### File Management

The skill creates and manages these files:

| File | Created When | Purpose |
|------|--------------|---------|
| `{study-name}-study.xml` | After study creation | Complete study specification, editable by user |
| `{study-name}-requirements.md` | After analysis | Development requirements, optimized for LLMs |

All files are saved to your working directory with appropriate naming.

### URLs Provided

The skill provides URLs for manual interaction:

- **edit_questions_url**: Edit questions in browser interface
- **interview_url**: Test the interview experience yourself
- **transcript_url**: View completed interview transcripts

### Progress Monitoring

The skill keeps you informed throughout:
- Progress updates during long operations
- Participation statistics tracking
- Analysis status monitoring
- Clear next-step guidance

## Best Practices

### Study Scope
- Focus on single problem area
- Define 3-5 clear research questions
- Be specific about target users
- Include realistic constraints

### Question Design
- Use 5-10 questions for most studies
- Mix behavioral and attitudinal questions
- Test interview flow before simulations
- Avoid leading questions

### Persona Generation
- 3-5 personas: Quick validation
- 6-8 personas: Standard research
- 10+ personas: Comprehensive studies
- Ensure demographic and behavioral diversity

### Analysis Configuration
- 2 runs: Quick directional insights
- 3-4 runs: Standard robust findings (recommended)
- 4-5 runs: Critical business decisions
- Model tiers: open_weights → premium → frontier

## Common Use Cases

### Feature Development
```
"Research user needs for our new collaboration feature"
→ Understand requirements before building
```

### UX Improvement
```
"Study why users struggle with our onboarding flow"
→ Identify friction points and solutions
```

### Adoption Investigation
```
"Find out why customers aren't using our API"
→ Uncover barriers and opportunities
```

### Validation Research
```
"Validate our new checkout design with user feedback"
→ Test before full implementation
```

### Requirements Gathering
```
"Gather requirements for mobile app redesign"
→ User-driven feature prioritization
```

## Troubleshooting

### Skill Not Activating

If the skill doesn't trigger automatically:

1. **Check installation:**
   ```
   What skills are available?
   ```
   
2. **Invoke manually:**
   ```
   /user-research [your topic]
   ```

3. **Be more explicit:**
   ```
   "Use the user-research skill to investigate checkout abandonment"
   ```

### MCP Tools Not Working

If you see MCP connection errors:

1. **Verify Deutero server is running:**
   ```bash
   curl http://127.0.0.1:8000/health
   ```

2. **Check MCP configuration:**
   - Review `~/.claude/settings.json`
   - Verify API key is set
   - Confirm server URL is correct

3. **Test MCP tools:**
   ```
   What MCP tools are available?
   ```

### Files Not Being Created

If XML or requirements files aren't appearing:

1. **Check working directory:**
   ```
   Where are we working?
   ```

2. **Verify file was created:**
   ```
   List files in current directory
   ```

3. **Ask Claude to recreate:**
   ```
   "Recreate the study XML file"
   ```

### Analysis Not Completing

If thematic analysis seems stuck:

1. **Check status:**
   ```
   "Check analysis status for this study"
   ```

2. **Verify interviews completed:**
   ```
   "Show participation statistics"
   ```

3. **Wait longer:**
   - Analysis can take 5-10 minutes
   - Multiple runs and interviews take longer

## Integration

### With Development Workflow

```
Research → Requirements → Development → Validation
```

The requirements document is optimized for:
- LLM coding agents (Claude Code, Cursor, etc.)
- Product managers (prioritized, evidence-based)
- Development teams (technical requirements with user context)

### With Design Process

```
Concept → User Research → Design Iteration → Validation Research
```

Use the skill for:
- Pre-design user needs research
- Concept validation
- Post-design usability feedback

### With Product Planning

```
Idea → Research Study → Requirements → Roadmap Prioritization
```

Use findings to:
- Validate product ideas
- Prioritize features
- Inform roadmap decisions

## Advanced Usage

### Background Execution

Run time-consuming operations in background:

```
"Run the interview simulations in the background"
```

Press **Ctrl+B** to background a running operation.

### Multiple Studies

Run several studies in parallel:

```
"Create three studies: one for mobile users, one for desktop users, 
and one for API customers"
```

### Custom Analysis

Specify analysis parameters:

```
"Run analysis with frontier tier and 5 runs for maximum quality"
```

### Resume Previous Work

Continue from where you left off:

```
/user-research [survey-id from previous session]
```

## Examples

See `examples.md` for detailed walkthroughs of:
- E-commerce checkout abandonment study
- Feature adoption investigation
- Mobile app redesign research
- API developer experience study
- Quick validation studies

## API Reference

See `reference.md` for complete documentation of:
- All 8 Deutero MCP tools
- Parameter specifications
- Return value structures
- Common workflows
- Error handling

## Support

### Resources
- **Deutero Documentation**: https://www.deutero.ai/docs
- **Claude Code Docs**: https://code.claude.com/docs
- **Skills Guide**: https://code.claude.com/docs/en/extend-claude-with-skills

### Getting Help

1. **Check examples.md** for similar use cases
2. **Review reference.md** for tool details
3. **Ask Claude** for help with specific issues
4. **Check MCP configuration** if tools aren't working

## Related Skills

Consider combining with:
- **commit-skill**: Commit research files to version control
- **document-skill**: Generate additional documentation
- **slack-skill**: Share findings with team

## Quick Reference

```
┌─────────────────────────────────────────────────────────┐
│              USER RESEARCH SKILL                        │
├─────────────────────────────────────────────────────────┤
│ INSTALLATION                                            │
│   mkdir -p ~/.claude/skills/user-research               │
│   cp SKILL.md examples.md reference.md [that directory] │
│                                                         │
│ INVOCATION                                              │
│   Automatic: "Research why users abandon checkout"     │
│   Manual: /user-research [topic]                       │
│                                                         │
│ WORKFLOW                                                │
│   1. Create study → XML file                           │
│   2. Generate questions → Updated XML                  │
│   3. Create personas → Persona list                    │
│   4. Run simulations → Transcripts                     │
│   5. Analyze → Requirements.md                         │
│                                                         │
│ FILES CREATED                                           │
│   {study-name}-study.xml                               │
│   {study-name}-requirements.md                         │
│                                                         │
│ KEY PARAMETERS                                          │
│   Personas: 3-5 (quick) | 6-8 (standard) | 10+ (comprehensive) │
│   Questions: 5-7 (quick) | 8-10 (standard)             │
│   Analysis: 2 runs (quick) | 3-4 runs (standard)       │
└─────────────────────────────────────────────────────────┘
```

## License

This skill configuration is provided as-is for use with Claude Code and Deutero.
