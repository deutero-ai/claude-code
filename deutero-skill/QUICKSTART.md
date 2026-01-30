# Deutero Plugin - Quick Start Guide

Get up and running with user research in Claude Code in under 5 minutes.

## Prerequisites Checklist

- [ ] Claude Code 1.0.33+ installed (`claude --version`)
- [ ] Deutero API key (get at [deutero.ai](https://www.deutero.ai))
- [ ] 5 minutes to set up

## 3-Step Setup

### Step 1: Install the Plugin (1 minute)

```bash
# If using a marketplace
/plugin install deutero

# Or load locally
claude --plugin-dir ./deutero-plugin
```

### Step 2: Configure API Key (1 minute)

```bash
# Set your API key
export DEUTERO_API_KEY="your-api-key-here"

# Add to your shell profile for persistence
echo 'export DEUTERO_API_KEY="your-api-key-here"' >> ~/.zshrc
source ~/.zshrc
```

### Step 3: Verify Installation (1 minute)

```bash
# Start Claude Code
claude

# Check the plugin loaded
/plugin list
# You should see: ✓ deutero (v1.0.0)

# Test MCP connection
"What MCP tools are available?"
# You should see 8 Deutero tools

# Verify skill and agent
"What skills are available?"  # Should include user-research
/agents  # Should include user-researcher
```

## Your First Study (2 minutes)

### Option 1: Automatic (Easiest)

Just describe what you need:

```
"I need to understand why users abandon our checkout process"
```

Claude will automatically:
1. Use the user-research skill
2. Guide you through study creation
3. Generate questions and personas
4. Run simulations and analysis
5. Create requirements document

### Option 2: Explicit

Invoke the skill directly:

```
/deutero:user-research checkout abandonment issues
```

### Option 3: Subagent (For Background Work)

```
"Use the user-researcher subagent to investigate mobile app onboarding 
with 8 personas and generate a requirements document"
```

## What Happens Next?

The plugin will guide you through 4 phases:

### Phase 1: Study Design (~2 minutes)
- Gathers context about your research need
- Creates research questions and objectives
- Saves study specification to XML file
- **You review and approve**

### Phase 2: Question Generation (~2 minutes)
- Generates targeted interview questions
- Provides URL to test interview
- Provides URL to edit questions
- **You review and approve**

### Phase 3: Data Collection (~5 minutes)
- Creates diverse user personas
- Runs interview simulations
- Monitors completion progress
- **Automatic (you monitor)**

### Phase 4: Analysis (~10 minutes)
- Runs multi-model thematic analysis
- Identifies patterns and themes
- Generates requirements document
- **Automatic (you review results)**

**Total time**: ~20 minutes for a complete study

## Example: Complete Study

Here's what a real session looks like:

```
You: /deutero:user-research why aren't users using our new dashboard feature

Plugin: I'll create a study to investigate dashboard feature adoption barriers.

Let me gather some context:
- What's the business context?
> Enterprise SaaS, dashboard launched 3 months ago, 20% adoption vs 60% target

- Who are the target users?
> IT managers, data analysts, business intelligence teams

- Any constraints?
> Need insights in 2 weeks for Q2 planning

Plugin: Creating study...

✓ Study created: dashboard-adoption-study.xml

Research Questions:
1. How do users currently handle analytics in their role?
2. What prevents them from trying the dashboard?
3. For those who tried, what was the experience?
4. What would increase usage?

Ready to generate interview questions?

You: Yes, create 8 questions

Plugin: Generating 8 targeted questions...

✓ Questions added to study

You can:
- Edit questions: http://0.0.0.0:8000/edit-survey/?survey_id=abc-123
- Test interview: http://localhost:8000/?survey_id=abc-123

Ready to generate personas?

You: Generate 6 diverse personas

Plugin: Creating 6 personas...

✓ Personas created:
1. Senior IT Manager (large enterprise)
2. Data Analyst (mid-size company)
3. BI Lead (startup)
4. Dept Manager (non-technical)
5. Junior Analyst (new to role)
6. Technical Architect (evaluating tools)

Running 6 interview simulations...

✓ All interviews completed (took 4 minutes)

Running thematic analysis with 3 runs...

✓ Analysis complete!

Key Findings:
1. **Awareness Gap** (4/6 personas)
   - Didn't know feature existed
   - No in-app promotion

2. **Onboarding Friction** (5/6 who tried)
   - Steep learning curve
   - No tutorial or guidance

3. **Value Unclear** (6/6 personas)
   - Benefits not obvious
   - No clear ROI shown

Recommendations:
1. Launch awareness campaign
2. Create 5-min quick start guide
3. Add interactive tutorial
4. Develop ROI calculator
5. Build Slack integration

✓ Created: dashboard-adoption-requirements.md

The requirements document is ready for your development team!
```

## Files You'll Get

After running a study, you'll have:

1. **`{study-name}-study.xml`**
   - Complete study specification
   - Editable between phases
   - Use for replication or reference

2. **`{study-name}-requirements.md`**
   - LLM-optimized requirements
   - Ready for development team
   - Evidence-based recommendations

## Quick Tips

### 🎯 Study Scope
- Keep focused on single problem
- 3-5 research questions ideal
- Be specific about users

### 📝 Questions
- 5-7 questions: Quick studies
- 8-10 questions: Standard studies
- Test interview flow before simulations

### 👥 Personas
- 3-5: Quick validation
- 6-8: Standard research
- 10+: Comprehensive studies

### 🔍 Analysis
- 2 runs: Quick insights
- 3-4 runs: Robust findings (recommended)
- 4-5 runs: Critical decisions

### ⚡ Speed
- Quick study: 1-2 hours total
- Standard study: Half day
- Comprehensive: Full day

## Common First-Time Questions

### "How do I resume a study later?"

Save the survey_id (UUID) from the study creation. Then:

```
/deutero:user-research abc-123-def-456-789
```

### "Can I edit questions after generation?"

Yes! Two ways:
1. Use the `edit_questions_url` provided
2. Edit the XML file directly, then continue

### "How do I know when analysis is complete?"

The plugin monitors automatically and notifies you. Or check:

```
"Check analysis status for this study"
```

### "What if I want to run multiple studies?"

You can run them sequentially or in parallel:

```
"Run three studies: mobile users, desktop users, and API customers"
```

Each gets its own survey_id and files.

### "Can I customize the workflow?"

Yes! Edit the files in `skills/user-research/` or `agents/` to customize behavior.

## Next Steps

Now that you're set up:

1. **Run your first study** (use the example above)
2. **Review the files created** (XML and requirements.md)
3. **Check out full examples** in `skills/user-research/examples.md`
4. **Read the tool reference** in `skills/user-research/reference.md`
5. **Explore advanced features** in the main README

## Need Help?

### Quick Answers
- **Skill not working?** Try `/deutero:user-research [topic]` explicitly
- **MCP errors?** Check `curl http://127.0.0.1:8000/health`
- **Files not created?** Check working directory with `pwd`
- **Analysis stuck?** Wait 10 mins or check status

### Documentation
- Main README: Complete feature documentation
- Examples: `skills/user-research/examples.md`
- Tool Reference: `skills/user-research/reference.md`
- Deutero Docs: https://www.deutero.ai/docs

### Support
- Email: support@deutero.ai
- GitHub: https://github.com/deutero-ai/claude-code-plugin/issues

## Video Tutorial

[Coming soon: 5-minute setup and first study video]

---

**Ready?** Start Claude Code and run your first study:

```bash
claude
```

```
"I need to understand why users [your problem here]"
```

Happy researching! 🎉
