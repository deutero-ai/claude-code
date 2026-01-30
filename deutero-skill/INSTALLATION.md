# Deutero Plugin - Installation & Testing Guide

Complete guide for installing, configuring, and testing the Deutero plugin.

## Table of Contents

1. [Installation Methods](#installation-methods)
2. [Configuration](#configuration)
3. [Testing](#testing)
4. [Verification Checklist](#verification-checklist)
5. [Troubleshooting](#troubleshooting)
6. [Uninstallation](#uninstallation)

---

## Installation Methods

### Method 1: Load from Directory (Development/Testing)

Best for: Testing, development, or temporary use

```bash
# Navigate to the plugin directory
cd /path/to/deutero-plugin

# Start Claude Code with the plugin
claude --plugin-dir .
```

**Pros:**
- No permanent installation
- Easy to update/modify
- Great for testing

**Cons:**
- Must use `--plugin-dir` flag every time
- Not available in other projects

### Method 2: Install to User Plugins Directory

Best for: Personal use across all projects

```bash
# Copy plugin to user plugins directory
mkdir -p ~/.claude/plugins
cp -r deutero-plugin ~/.claude/plugins/deutero

# Start Claude Code normally
claude
```

**Pros:**
- Available in all projects
- No special flags needed
- Persists across sessions

**Cons:**
- Requires manual updates
- User-specific only

### Method 3: Install to Project

Best for: Project-specific use, team collaboration

```bash
# In your project directory
mkdir -p .claude/plugins
cp -r /path/to/deutero-plugin .claude/plugins/deutero

# Commit to version control
git add .claude/plugins/deutero
git commit -m "Add Deutero plugin"

# Start Claude Code normally
claude
```

**Pros:**
- Team members get the plugin automatically
- Version controlled
- Project-specific

**Cons:**
- Need to update in each project
- Takes repository space

### Method 4: From Marketplace (Future)

Best for: Production use, automatic updates

```bash
# When plugin is published to marketplace
claude
/plugin install deutero
```

**Pros:**
- Easy installation
- Automatic updates
- Verified and tested

**Cons:**
- Requires marketplace setup (coming soon)

---

## Configuration

### Step 1: API Key Setup

The plugin requires a Deutero API key. Get one at [deutero.ai](https://www.deutero.ai).

#### Temporary (Current Session)
```bash
export DEUTERO_API_KEY="your-api-key-here"
claude --plugin-dir ./deutero-plugin
```

#### Persistent (Recommended)
```bash
# Add to shell profile
echo 'export DEUTERO_API_KEY="your-api-key-here"' >> ~/.zshrc
source ~/.zshrc

# Or for bash
echo 'export DEUTERO_API_KEY="your-api-key-here"' >> ~/.bashrc
source ~/.bashrc
```

#### Project-Specific (.env file)
```bash
# Create .env file in project root
echo 'DEUTERO_API_KEY=your-api-key-here' > .env

# Load before starting Claude Code
set -a; source .env; set +a
claude
```

### Step 2: MCP Server Configuration

The plugin automatically configures the MCP server. To customize:

#### Option A: Use Environment Variables (Recommended)
```bash
# Default (localhost)
export DEUTERO_BASE_URL="http://127.0.0.1:8000"

# Or cloud service
export DEUTERO_BASE_URL="https://agents.deutero.ai"

# Custom timeout (milliseconds)
export DEUTERO_TIMEOUT="60000"
```

#### Option B: Modify Plugin Configuration

Edit `deutero-plugin/.mcp.json`:

```json
{
  "mcpServers": {
    "deutero": {
      "url": "https://agents.deutero.ai/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_API_KEY}"
      },
      "timeout": 60000
    }
  }
}
```

#### Option C: Override in Claude Settings

Edit `~/.claude/settings.json`:

```json
{
  "mcpServers": {
    "deutero": {
      "url": "http://127.0.0.1:8000/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "your-actual-key-here"
      },
      "timeout": 60000
    }
  }
}
```

### Step 3: Verify MCP Server

Ensure the Deutero MCP server is running:

```bash
# Check health endpoint
curl http://127.0.0.1:8000/health

# Expected response:
# {"status": "healthy"}

# Test MCP endpoint with API key
curl -H "X-API-Key: $DEUTERO_API_KEY" \
  http://127.0.0.1:8000/mcp/list-tools

# Expected: List of 8 Deutero tools
```

---

## Testing

### Phase 1: Basic Verification

#### Test 1: Plugin Loads
```bash
claude --plugin-dir ./deutero-plugin

# In Claude Code:
/plugin list

# Expected output:
# ✓ deutero (v1.0.0)
#   Comprehensive user research toolkit...
```

#### Test 2: Skill Available
```
What skills are available?

# Expected: List includes "user-research"
```

#### Test 3: Agent Available
```
/agents

# Expected: List includes "user-researcher"
```

#### Test 4: MCP Tools Accessible
```
What MCP tools are available?

# Expected: List includes 8 Deutero tools:
# - create_study
# - create_study_questions
# - create_simulation_persona
# - simulate_interviews
# - run_thematic_analysis
# - get_analysis_status
# - get_agent_requirements
# - get_survey_participation
```

### Phase 2: Skill Testing

#### Test 5: Skill Invocation
```
/deutero:user-research test study

# Expected: Skill activates and starts gathering context
```

#### Test 6: Automatic Activation
```
I need to understand why users abandon checkout

# Expected: Skill activates automatically
```

#### Test 7: Help Text
```
/help deutero:user-research

# Expected: Displays skill description and usage
```

### Phase 3: Subagent Testing

#### Test 8: Subagent Delegation
```
Use the user-researcher subagent to create a quick test study

# Expected: Subagent starts in isolated context
```

#### Test 9: Subagent Listing
```
/agents

# Expected: Shows user-researcher in list
```

### Phase 4: Integration Testing

#### Test 10: Complete Workflow

Run a simple end-to-end test:

```bash
# Start Claude Code
claude --plugin-dir ./deutero-plugin

# In Claude Code:
/deutero:user-research mobile app onboarding test
```

**Expected workflow:**
1. ✅ Study creation prompt
2. ✅ XML file created
3. ✅ Question generation
4. ✅ Persona creation
5. ✅ Interview simulations
6. ✅ Analysis completion
7. ✅ Requirements document

**Expected files created:**
- `mobile-app-onboarding-test-study.xml`
- `mobile-app-onboarding-test-requirements.md`

#### Test 11: MCP Tool Calls

Verify MCP tools work:

```
# Test study creation
"Create a test study about user onboarding"

# Expected: create_study tool called successfully

# Test participation stats
"Show participation stats for the study"

# Expected: get_survey_participation tool called
```

#### Test 12: Error Handling

Test error scenarios:

```
# Invalid survey_id
"Get analysis status for survey invalid-id"

# Expected: Clear error message, not crash

# Missing API key (temporarily unset)
unset DEUTERO_API_KEY
claude --plugin-dir ./deutero-plugin
"Create a study"

# Expected: 401 Unauthorized error with clear message
```

### Phase 5: File Management Testing

#### Test 13: XML File Creation
```
/deutero:user-research test study

# After study creation:
ls -la *.xml

# Expected: test-study.xml exists
```

#### Test 14: Requirements Generation
```
# After completing analysis:
ls -la *requirements.md

# Expected: requirements.md file exists
```

#### Test 15: File Content Validation
```
# Check XML is valid
cat test-study.xml | head -20

# Expected: Valid XML structure with study_id, questions, etc.

# Check requirements are readable
cat test-requirements.md | head -20

# Expected: Markdown with structured requirements
```

---

## Verification Checklist

Use this checklist to verify installation:

### Installation
- [ ] Plugin directory structure is correct
- [ ] `.claude-plugin/plugin.json` exists
- [ ] Skills directory has `user-research/SKILL.md`
- [ ] Agents directory has `user-researcher.md`
- [ ] `.mcp.json` is present

### Configuration
- [ ] `DEUTERO_API_KEY` environment variable is set
- [ ] MCP server is running and accessible
- [ ] Health endpoint responds: `curl http://127.0.0.1:8000/health`
- [ ] MCP endpoint responds with tools list

### Claude Code Integration
- [ ] Plugin appears in `/plugin list`
- [ ] Skill appears in available skills
- [ ] Agent appears in `/agents`
- [ ] MCP tools are accessible

### Functionality
- [ ] Skill activates with `/deutero:user-research`
- [ ] Skill activates automatically with appropriate prompts
- [ ] Subagent delegates when requested
- [ ] MCP tools execute successfully
- [ ] Files are created in working directory

### Error Handling
- [ ] Clear error messages on API failures
- [ ] Graceful handling of invalid inputs
- [ ] No crashes on missing data
- [ ] Helpful suggestions for fixing issues

---

## Troubleshooting

### Issue: Plugin Not Loading

**Symptoms:**
- Plugin doesn't appear in `/plugin list`
- Skills not available

**Solutions:**
```bash
# 1. Check plugin structure
ls -la deutero-plugin/.claude-plugin/plugin.json
# Must exist at this exact path

# 2. Verify JSON is valid
cat deutero-plugin/.claude-plugin/plugin.json | jq .
# Should parse without errors

# 3. Check directory name
# If installed to ~/.claude/plugins/, directory must be named "deutero"
ls -la ~/.claude/plugins/deutero/.claude-plugin/

# 4. Restart Claude Code
# Exit and restart
```

### Issue: MCP Connection Failures

**Symptoms:**
- "MCP server not available"
- Tools don't execute
- 401 or 404 errors

**Solutions:**
```bash
# 1. Check server is running
curl http://127.0.0.1:8000/health
# Should return: {"status": "healthy"}

# 2. Verify API key
echo $DEUTERO_API_KEY
# Should output your key

# 3. Test MCP endpoint
curl -H "X-API-Key: $DEUTERO_API_KEY" \
  http://127.0.0.1:8000/mcp/list-tools
# Should return list of tools

# 4. Check firewall/network
# Ensure port 8000 is accessible

# 5. Try alternate URL
export DEUTERO_BASE_URL="http://127.0.0.1:8000"
# Or use IP: http://0.0.0.0:8000
```

### Issue: Skill Not Activating

**Symptoms:**
- Skill doesn't respond to prompts
- Manual invocation doesn't work

**Solutions:**
```bash
# 1. Check skill is loaded
# In Claude Code:
What skills are available?
# Should list "user-research"

# 2. Try explicit invocation
/deutero:user-research test

# 3. Check skill file exists
ls -la deutero-plugin/skills/user-research/SKILL.md

# 4. Verify frontmatter
head -20 deutero-plugin/skills/user-research/SKILL.md
# Should have valid YAML between --- markers

# 5. Check for typos in name field
grep "^name:" deutero-plugin/skills/user-research/SKILL.md
# Should be: name: user-research
```

### Issue: Files Not Being Created

**Symptoms:**
- XML or requirements files don't appear
- Working directory seems empty

**Solutions:**
```bash
# 1. Check current directory
pwd
# Note the path

# 2. Search for files with UUID
ls -la | grep -E '[0-9a-f]{8}-[0-9a-f]{4}'

# 3. Check permissions
# Ensure Claude Code can write to current directory

# 4. Try a different directory
cd ~/Desktop
claude --plugin-dir /path/to/deutero-plugin

# 5. Ask Claude to recreate
"Recreate the study XML file"
```

### Issue: Analysis Not Completing

**Symptoms:**
- Analysis seems stuck
- No progress updates

**Solutions:**
```bash
# 1. Check status explicitly
"Check analysis status for this study"

# 2. Verify interviews completed
"Show participation statistics"

# 3. Wait longer
# Analysis can take 10-15 minutes for 8 interviews with 4 runs

# 4. Check server logs
# If running local server, check console output

# 5. Restart analysis
# Note survey_id and try again with explicit ID
```

### Issue: Permission Errors

**Symptoms:**
- "Permission denied" errors
- Files can't be written

**Solutions:**
```bash
# 1. Check directory permissions
ls -la

# 2. Use a directory you own
cd ~
mkdir research-test
cd research-test
claude --plugin-dir /path/to/deutero-plugin

# 3. Check file system isn't read-only

# 4. On shared systems, use your home directory
```

---

## Uninstallation

### Remove Plugin

```bash
# If installed to user plugins
rm -rf ~/.claude/plugins/deutero

# If installed to project
rm -rf .claude/plugins/deutero

# Remove configuration (optional)
# Edit ~/.claude/settings.json and remove deutero section
```

### Remove Environment Variables

```bash
# Edit shell profile
nano ~/.zshrc  # or ~/.bashrc

# Remove lines:
# export DEUTERO_API_KEY="..."
# export DEUTERO_BASE_URL="..."

# Reload
source ~/.zshrc
```

### Clean Up Study Files

```bash
# Remove generated files (be careful!)
rm -f *-study.xml
rm -f *-requirements.md

# Or move to archive
mkdir research-archive
mv *-study.xml *-requirements.md research-archive/
```

---

## Advanced Testing

### Load Testing

Test with multiple concurrent studies:

```bash
# Start Claude Code
claude --plugin-dir ./deutero-plugin

# Create multiple studies
"Create study 1 about checkout"
"Create study 2 about onboarding"
"Create study 3 about navigation"

# Monitor resource usage
# Check all studies complete successfully
```

### Integration Testing

Test with other plugins:

```bash
# Load multiple plugins
claude \
  --plugin-dir ./deutero-plugin \
  --plugin-dir ./another-plugin

# Verify no conflicts
/plugin list
```

### Stress Testing

Test with maximum parameters:

```bash
# Large study
/deutero:user-research large scale test

# When prompted:
- 25 personas (maximum)
- 12 questions
- 5 analysis runs
- Frontier tier

# Verify handles large workload
# Check all files created correctly
# Monitor memory usage
```

---

## Support

If issues persist after troubleshooting:

1. **Check documentation**:
   - README.md - Main docs
   - QUICKSTART.md - Setup guide
   - Skills reference.md - Tool details

2. **Search issues**:
   - GitHub issues for similar problems

3. **Create issue**:
   - Include all relevant information:
     - Claude Code version
     - Plugin version
     - Error messages
     - Steps to reproduce

4. **Contact support**:
   - Email: support@deutero.ai
   - Include debug information

---

## Quick Reference

### Essential Commands

```bash
# Install
cp -r deutero-plugin ~/.claude/plugins/deutero

# Load (dev)
claude --plugin-dir ./deutero-plugin

# Check plugin
/plugin list

# Check skill
What skills are available?

# Check agent
/agents

# Test MCP
What MCP tools are available?

# Use skill
/deutero:user-research [topic]

# Check logs
tail -f ~/.claude/logs/*.log
```

### Essential Environment Variables

```bash
export DEUTERO_API_KEY="your-key"
export DEUTERO_BASE_URL="http://127.0.0.1:8000"
```

### Quick Health Check

```bash
# Server health
curl http://127.0.0.1:8000/health

# MCP tools
curl -H "X-API-Key: $DEUTERO_API_KEY" \
  http://127.0.0.1:8000/mcp/list-tools

# Plugin loaded
claude --plugin-dir . -c "/plugin list"
```

---

**Installation complete?** Head to [QUICKSTART.md](QUICKSTART.md) to run your first study!
