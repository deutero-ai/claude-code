# Deutero Plugin for Claude Code

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/deutero-ai/claude-code-plugin)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

Comprehensive user research toolkit for Claude Code. Conduct UX studies, gather requirements, run qualitative interviews at scale, and generate actionable product insights—all powered by Deutero's AI research platform.

## Features

🎯 **Complete Research Workflow**
- Study design and planning
- Interview question generation
- User persona creation
- Automated interview simulation
- Thematic analysis with multiple AI models
- LLM-optimized requirements generation

🤖 **Two Ways to Work**
- **Skill** (`/deutero:user-research`): Interactive, step-by-step workflow with approval gates
- **Subagent** (automatic delegation): Isolated context for complex research operations

📊 **8 Research Operations**
- Create studies with research objectives
- Generate targeted interview questions
- Create diverse user personas
- Simulate interviews at scale
- Run multi-model thematic analysis
- Track analysis progress
- Generate development requirements
- Monitor participation metrics

🔧 **Production-Ready**
- XML file management for study specifications
- Markdown requirements optimized for AI coding agents
- Progress monitoring and status tracking
- Error handling and validation
- Background task support

## Quick Start

### 1. Install the Plugin

```bash
# From a marketplace (recommended)
/plugin install deutero

# Or load locally for development
claude --plugin-dir ./deutero-plugin
```

### 2. Configure Deutero API

Set your API key as an environment variable:

```bash
export DEUTERO_API_KEY="your-api-key-here"
```

Or add to your shell profile (`~/.bashrc`, `~/.zshrc`):

```bash
echo 'export DEUTERO_API_KEY="your-api-key-here"' >> ~/.zshrc
source ~/.zshrc
```

### 3. Start Researching

```bash
# Launch Claude Code
claude

# Run a study (automatic - skill activates when needed)
"I need to understand why users abandon our checkout process"

# Or invoke explicitly
/deutero:user-research checkout abandonment issues

# Or use the subagent
"Use the user-researcher subagent to investigate mobile app onboarding"
```

## Installation

### Prerequisites

- Claude Code 1.0.33 or later
- Deutero API account and key (get one at [deutero.ai](https://www.deutero.ai))
- Deutero MCP server running (see [Server Setup](#server-setup))

### From Plugin Marketplace

1. Open Claude Code
2. Run `/plugin install deutero`
3. Follow the configuration prompts
4. Restart Claude Code

### From Source

```bash
# Clone or download the plugin
git clone https://github.com/deutero-ai/claude-code-plugin.git deutero-plugin

# Load the plugin
claude --plugin-dir ./deutero-plugin

# Or install permanently
cp -r deutero-plugin ~/.claude/plugins/deutero
```

### Server Setup

The plugin requires the Deutero MCP server to be running and accessible. You have two options:

#### Option 1: Cloud Service (Recommended)

Use Deutero's hosted service:

```bash
export DEUTERO_BASE_URL="https://api.deutero.ai"
export DEUTERO_API_KEY="your-api-key"
```

#### Option 2: Local Server

Run the Deutero MCP server locally:

```bash
# Install dependencies
pip install fastmcp httpx --break-system-packages

# Start the server
python deutero_mcp_server.py
```

The server will be available at `http://127.0.0.1:8000` (default).

### Verify Installation

After installation, verify the plugin is loaded:

```bash
# Check available plugins
/plugin list

# Check available skills
What skills are available?

# Check available agents
/agents

# Test the MCP connection
"Test the Deutero connection"
```

You should see:
- ✅ Deutero plugin in the plugin list
- ✅ `user-research` skill available
- ✅ `user-researcher` agent available
- ✅ 8 Deutero MCP tools accessible

## Usage

### Interactive Research Workflow (Skill)

The skill provides a guided, interactive workflow with approval gates at each phase:

```bash
# Automatic activation
"Research why users aren't adopting our dashboard feature"

# Or explicit invocation
/deutero:user-research dashboard feature adoption
```

**Workflow phases:**
1. **Study Creation** - Define research objectives → Review XML file → Approve
2. **Question Design** - Generate questions → Test interview → Approve
3. **Data Collection** - Create personas → Run simulations → Monitor progress
4. **Analysis** - Run thematic analysis → Generate requirements → Review findings

**Example session:**
```
You: /deutero:user-research mobile app onboarding problems

Plugin: Creating study to investigate onboarding issues...

[Gathers context, creates study, saves XML file]

Study created: mobile-app-onboarding-study.xml

Research Questions:
1. How do users first interact with the app?
2. What confuses them during onboarding?
3. What would make onboarding easier?

Review the XML file. Ready to generate questions?

You: Yes, create 7 questions

[Generates questions, provides URLs]

Questions added. Test the interview at: http://localhost:8000/?survey_id=...

Ready to generate personas?

You: Generate 6 diverse personas

[Creates personas, runs simulations, analyzes results]

Analysis complete! Key findings:
- 5/6 personas struggled with navigation
- Onboarding takes 2x longer than expected
- Users skip critical setup steps

Created: mobile-app-onboarding-requirements.md
```

### Background Research (Subagent)

For complex research that shouldn't interrupt your main work:

```
"Use the user-researcher subagent to conduct a comprehensive study 
on API developer experience with 10 personas"
```

The subagent:
- Runs in isolated context
- Handles the complete workflow autonomously
- Returns summarized findings
- Preserves your main conversation context

### Resume Existing Studies

Continue previous research by providing the survey ID:

```bash
/deutero:user-research abc-123-def-456-789
```

The plugin detects where you left off and continues from that phase.

## Components

### 1. User Research Skill

**Name:** `/deutero:user-research`  
**Type:** Interactive workflow skill  
**Invocation:** Automatic or manual

Provides step-by-step guidance through the complete research workflow with approval gates at each phase.

**Features:**
- Interactive context gathering
- XML file management for study specs
- URL provisioning for manual editing/testing
- Progress monitoring and status updates
- File creation and management
- Error handling and validation

**When to use:**
- Interactive research with iteration
- Need approval gates between phases
- Want to test and refine before proceeding
- Prefer conversational guidance

### 2. User Researcher Subagent

**Name:** `user-researcher`  
**Type:** Specialized research agent  
**Invocation:** Automatic delegation by Claude

Handles complex research operations in isolated context with full autonomy.

**Features:**
- Autonomous workflow execution
- Isolated context (preserves main conversation)
- Full MCP tool access
- XML and markdown file generation
- Background task support

**When to use:**
- Complex multi-phase research
- Want isolation from main conversation
- Running multiple studies in parallel
- Need autonomous execution

### 3. MCP Server Integration

**Server:** Deutero MCP  
**Tools:** 8 research operations

Provides the backend functionality for all research operations:

| Tool | Operation |
|------|-----------|
| `create_study` | Initialize new research study |
| `create_study_questions` | Generate interview questions |
| `create_simulation_persona` | Create user personas |
| `simulate_interviews` | Run interview simulations |
| `run_thematic_analysis` | Analyze interview data |
| `get_analysis_status` | Monitor analysis progress |
| `get_agent_requirements` | Generate requirements document |
| `get_survey_participation` | Track interview statistics |

## Configuration

### Environment Variables

Configure the plugin using environment variables:

```bash
# Required: Your Deutero API key
export DEUTERO_API_KEY="your-api-key-here"

# Optional: API base URL (defaults to localhost)
export DEUTERO_BASE_URL="http://127.0.0.1:8000"

# Optional: Timeout for long-running operations (milliseconds)
export DEUTERO_TIMEOUT="60000"
```

### MCP Server Settings

The plugin automatically configures the MCP server connection. To customize, edit your Claude Code settings (`~/.claude/settings.json`):

```json
{
  "mcpServers": {
    "deutero": {
      "url": "http://127.0.0.1:8000/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_API_KEY}"
      },
      "timeout": 60000
    }
  }
}
```

### Skill Customization

To customize the skill behavior, edit `skills/user-research/SKILL.md` frontmatter:

```yaml
---
name: user-research
description: Conduct user research studies...
allowed-tools: MCP, Read, Write, Edit, Bash
model: sonnet  # Change to 'opus' or 'haiku'
---
```

### Subagent Customization

To customize the subagent, edit `agents/user-researcher.md` frontmatter:

```yaml
---
name: user-researcher
description: User research specialist...
model: sonnet  # Change to 'opus' or 'haiku'
permissionMode: default  # Or 'acceptEdits', 'dontAsk', etc.
---
```

## Workflows

### Quick Study (1-2 hours)

For fast directional insights:

```
/deutero:user-research [topic]
→ 3-5 personas
→ 5 questions
→ 2 analysis runs (open_weights tier)
→ Quick requirements doc
```

### Standard Study (half day)

For reliable, actionable insights:

```
/deutero:user-research [topic]
→ 6-8 personas
→ 8-10 questions
→ 3-4 analysis runs (premium tier)
→ Comprehensive requirements
```

### Comprehensive Study (full day)

For critical decisions requiring deep analysis:

```
/deutero:user-research [topic]
→ 10+ personas
→ 10-12 questions
→ 4-5 analysis runs (frontier tier)
→ Full analysis report + requirements
```

## File Outputs

The plugin creates these files in your working directory:

### Study XML File
**Format:** `{study-name}-study.xml`  
**Created:** After study creation and question generation  
**Purpose:** Complete study specification, editable by user

```xml
<?xml version="1.0" encoding="UTF-8"?>
<study>
  <study_id>uuid</study_id>
  <study_name>Checkout Abandonment Research</study_name>
  <research_questions>...</research_questions>
  <interview_questions>...</interview_questions>
</study>
```

### Requirements Document
**Format:** `{study-name}-requirements.md`  
**Created:** After thematic analysis  
**Purpose:** LLM-optimized development requirements

```markdown
# Development Requirements: Feature Name

## Executive Summary
[Key findings and recommendations]

## User Needs
[Evidence-based user requirements]

## Technical Requirements
[Specific implementation requirements]

## Implementation Priorities
[Phased rollout plan]
```

## Examples

### E-commerce Checkout Study

```bash
You: /deutero:user-research checkout abandonment on mobile

Plugin: [Creates study with 7 questions, 6 personas]
Plugin: [Runs simulations and analysis]

Results:
- 5/6 personas cited hidden shipping costs
- 4/6 wanted guest checkout
- Mobile form UX major friction point

Recommendations:
1. Show shipping costs on cart page (25% impact)
2. Add guest checkout (20% impact)
3. Improve mobile forms (30% mobile impact)

Files created:
- checkout-abandonment-study.xml
- checkout-abandonment-requirements.md
```

### Feature Adoption Investigation

```bash
You: Research why users aren't adopting the new dashboard

Plugin: [8 personas, 8 questions, premium analysis]

Key Findings:
- 60% weren't aware feature existed
- Onboarding too complex for those who tried
- Value proposition unclear
- No integration with existing workflows

Quick Wins:
1. Launch awareness campaign
2. Add 5-min quick start guide
3. Create demo video
4. Build Slack integration

Expected Impact: 20% → 55% adoption rate
```

### API Developer Experience

```bash
You: Study API integration challenges for developers

Plugin: [5 technical personas, 8 questions, frontier analysis]

Critical Issues:
- Authentication flow unclear (5/5 struggled)
- Error messages unhelpful
- Code examples outdated
- No Postman collection

Priority Fixes:
1. Rewrite auth documentation
2. Improve error messages
3. Update all code examples
4. Publish Postman collection
```

## Best Practices

### Study Design
✅ Focus on single problem area  
✅ Define 3-5 clear research questions  
✅ Be specific about target users  
✅ Include realistic constraints  

❌ Avoid combining unrelated topics  
❌ Don't make assumptions about users  
❌ Don't skip the review/approval steps  

### Question Generation
✅ Use 5-10 questions for most studies  
✅ Mix behavioral and attitudinal questions  
✅ Test interview flow before simulations  
✅ Avoid leading questions  

### Persona Creation
✅ 3-5 personas for focused studies  
✅ 6-8 personas for comprehensive research  
✅ Ensure demographic and behavioral diversity  
✅ Consider edge cases and underrepresented groups  

### Analysis Configuration
✅ Use 3-4 runs for robust findings  
✅ Start with 'open_weights' tier  
✅ Escalate to 'premium' or 'frontier' as needed  
✅ Analyze entire surveys (not individual interviews)  

## Troubleshooting

### Plugin Not Loading

**Problem:** Plugin doesn't appear after installation

**Solutions:**
```bash
# Check plugin installation
/plugin list

# Reload plugins
# Exit and restart Claude Code

# Check for conflicts
/plugin list --all

# Verify plugin structure
ls -la ~/.claude/plugins/deutero/
```

### MCP Connection Failures

**Problem:** "MCP server not available" errors

**Solutions:**
```bash
# 1. Check server is running
curl http://127.0.0.1:8000/health

# 2. Verify API key is set
echo $DEUTERO_API_KEY

# 3. Test MCP endpoint
curl -H "X-API-Key: $DEUTERO_API_KEY" \
  http://127.0.0.1:8000/mcp/list-tools

# 4. Check Claude Code MCP logs
tail -f ~/.claude/logs/mcp-*.log

# 5. Restart Claude Code
# Exit and run: claude
```

### Skill Not Triggering

**Problem:** Claude doesn't use the skill automatically

**Solutions:**
- Be explicit: `/deutero:user-research [topic]`
- Check skill is loaded: `What skills are available?`
- Use keywords: "research", "study", "interview", "UX"
- Verify MCP tools are accessible

### Analysis Not Completing

**Problem:** Thematic analysis seems stuck

**Solutions:**
```bash
# Check analysis status
"Check analysis status for survey [survey-id]"

# Verify interviews completed
"Show participation stats for survey [survey-id]"

# Check for errors in server logs
# Analysis typically takes 5-10 minutes for 6-8 interviews

# If truly stuck, restart analysis
# Note the survey_id and contact support
```

### File Creation Issues

**Problem:** XML or requirements files not being created

**Solutions:**
- Check working directory: `pwd`
- Verify write permissions
- Look for files with UUID: `ls -la | grep [survey-id]`
- Ask Claude to recreate: "Recreate the study XML file"

### Authentication Errors

**Problem:** 401 Unauthorized errors

**Solutions:**
```bash
# Verify API key is correct
echo $DEUTERO_API_KEY

# Check key has required permissions
# Log in to Deutero dashboard to verify

# Try setting key directly in settings
# Edit ~/.claude/settings.json:
{
  "mcpServers": {
    "deutero": {
      "headers": {
        "X-API-Key": "your-actual-key-here"
      }
    }
  }
}
```

## Support

### Documentation
- **Plugin Guide**: This README
- **Skill Documentation**: `skills/user-research/SKILL.md`
- **Tool Reference**: `skills/user-research/reference.md`
- **Examples**: `skills/user-research/examples.md`
- **Deutero Docs**: https://www.deutero.ai/docs

### Getting Help

1. **Check the examples**: See `skills/user-research/examples.md`
2. **Review tool reference**: See `skills/user-research/reference.md`
3. **Search issues**: https://github.com/deutero-ai/claude-code-plugin/issues
4. **Contact support**: support@deutero.ai
5. **Community**: https://discord.gg/deutero (if available)

### Reporting Issues

When reporting issues, include:
- Claude Code version: `claude --version`
- Plugin version: Check `plugin.json`
- Error messages (full text)
- Steps to reproduce
- Expected vs actual behavior

[Create an issue](https://github.com/deutero-ai/claude-code-plugin/issues/new)

## Development

### Building from Source

```bash
# Clone the repository
git clone https://github.com/deutero-ai/claude-code-plugin.git
cd claude-code-plugin

# Test locally
claude --plugin-dir .

# Make changes to skills, agents, or manifest
# Test changes
# Commit and push
```

### Testing

```bash
# Load plugin in development mode
claude --plugin-dir ./deutero-plugin

# Test each component
/deutero:user-research test study
"Use user-researcher subagent for test"
"What MCP tools are available?"

# Check for errors
tail -f ~/.claude/logs/*.log
```

### Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Changelog

### v1.0.0 (2024-01-29)

**Initial Release**

Features:
- User research skill with complete workflow
- User researcher subagent for autonomous operation
- MCP server integration (8 tools)
- XML file management
- Requirements document generation
- Progress monitoring and status tracking
- Comprehensive documentation and examples

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Credits

- **Developed by**: Deutero (https://www.deutero.ai)
- **MCP Integration**: FastMCP
- **Built for**: Claude Code by Anthropic

## Links

- **Website**: https://www.deutero.ai
- **Documentation**: https://www.deutero.ai/docs
- **GitHub**: https://github.com/deutero-ai/claude-code-plugin
- **Support**: support@deutero.ai
- **Claude Code**: https://code.claude.com

---

Made with ❤️ by the Deutero team

For questions, issues, or feedback: support@deutero.ai
