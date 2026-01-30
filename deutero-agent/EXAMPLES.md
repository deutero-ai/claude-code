# User Researcher Subagent - Usage Examples

This guide provides practical examples of using the User Researcher subagent for various UX research scenarios.

---

## Example 1: Feature Adoption Study

**Scenario**: Your team launched a new dashboard feature 3 months ago, but adoption is lower than expected. You need to understand why.

### User Request
```
"I need to understand why enterprise customers aren't adopting our new 
dashboard analytics feature. It launched 3 months ago and we're seeing 
only 20% adoption among eligible accounts."
```

### Subagent Workflow

**Phase 1: Study Creation**
```
User Researcher: "I'll create a research study to investigate dashboard 
adoption barriers. Let me gather the study parameters..."

[Elicits information]
- Business context: Enterprise SaaS, analytics dashboard feature
- Research need: Understand low adoption (20% vs. 60% target)
- Target users: IT managers, data analysts, business intelligence teams
- Constraints: Need insights in 2 weeks, budget for 8 interviews

[Creates study]

User Researcher: "Study created! Saved to 'dashboard-adoption-study.xml'

Research Questions:
1. What are the primary barriers to dashboard feature adoption?
2. How do current non-users perceive the feature's value proposition?
3. What would motivate users to start using the dashboard?
4. Are there technical or organizational obstacles?
5. How does this compare to competitors' analytics tools?

Research Objectives:
1. Identify top 3 adoption barriers
2. Understand user perception vs. product team's intent
3. Generate actionable recommendations for improving adoption

Please review the XML file. Ready to generate interview questions?"
```

**Phase 2: Question Design**
```
You: "Yes, create 8 questions focusing on barriers and motivations"

User Researcher: "Generating 8 targeted questions..."

[Creates questions]

Questions added to study:
1. Can you walk me through how you currently handle analytics and reporting 
   in your role?
2. How did you first learn about our dashboard analytics feature?
3. What was your initial reaction when you saw/heard about this feature?
4. Have you tried to use the dashboard feature? If not, what has stopped you?
5. If you have tried it, what was that experience like?
6. How would you compare this to other analytics tools you use?
7. What would need to change for you to use this feature regularly?
8. Is there anything else about your analytics needs we should know?

Edit questions: http://0.0.0.0:8000/edit-survey/?survey_id=abc123
Test interview: http://localhost:8000/?survey_id=abc123

Review and test the flow, then let me know when you're ready to run simulations.
```

**Phase 3: Data Collection**
```
You: "Generate 6 diverse personas and run all interviews"

User Researcher: "Generating 6 personas representing different user segments..."

[Creates personas]

Personas created:
1. Senior IT Manager (large enterprise, 500+ employees)
2. Data Analyst (mid-size company, established analytics practice)
3. Business Intelligence Lead (startup, building analytics from scratch)
4. Department Manager (non-technical, needs insights for decisions)
5. Junior Analyst (new to role, learning tools)
6. Technical Architect (evaluating tools for organization)

[Simulates interviews]

Running interviews for all 6 personas...
- Persona 1: Interview started (transcript: https://...)
- Persona 2: Interview started (transcript: https://...)
- Persona 3: Interview started (transcript: https://...)
- Persona 4: Interview started (transcript: https://...)
- Persona 5: Interview started (transcript: https://...)
- Persona 6: Interview started (transcript: https://...)

Simulations will complete in 3-5 minutes. I'll monitor progress...

[Checks participation]

All 6 interviews completed! 
- Total: 6
- Completed: 6
- Completion rate: 100%

Ready to run thematic analysis?
```

**Phase 4: Analysis & Synthesis**
```
You: "Yes, run analysis with 4 runs for robust findings"

User Researcher: "Running thematic analysis with 4 runs..."

[Runs analysis]

Analysis queued for 6 interviews (4 runs each)
This will take several minutes...

[Monitors status]

Analysis progress:
- Interview 1: 4/4 runs complete
- Interview 2: 4/4 runs complete
- Interview 3: 4/4 runs complete
- Interview 4: 4/4 runs complete
- Interview 5: 4/4 runs complete
- Interview 6: 4/4 runs complete

[Generates requirements]

Analysis complete! Generating requirements document...

Created: dashboard-adoption-requirements.md

Key Findings:
1. **Awareness Gap**: 4/6 personas didn't know feature existed
2. **Onboarding Friction**: Those who tried faced steep learning curve
3. **Integration Issues**: Doesn't fit existing workflows
4. **Value Unclear**: Benefits not obvious for time investment
5. **Training Gap**: No self-serve resources or guidance

Recommendations:
1. Launch awareness campaign targeting existing users
2. Create interactive onboarding flow (5-min quick start)
3. Build integrations with existing analytics tools
4. Develop case study showing ROI for typical use cases
5. Create video tutorials and documentation

The requirements document has been optimized for your development team 
to implement these improvements.
```

---

## Example 2: Mobile App Redesign

**Scenario**: Planning to redesign your mobile app and need user input on priorities.

### User Request
```
"We're redesigning our mobile app from scratch. I need to understand what 
users love, hate, and what features are most important to them."
```

### Abbreviated Workflow

```
User Researcher: "I'll create a comprehensive mobile app redesign study..."

[Study Creation]
Study: mobile-app-redesign-study.xml
Focus: Current experience evaluation, feature priorities, pain points

[Question Generation - 10 questions]
1. How often do you use our mobile app and for what purposes?
2. What are your favorite features and why?
3. What frustrates you most about the current app?
4. Can you describe a recent time when the app didn't meet your needs?
5. If you could change one thing about the app, what would it be?
6. How does our app compare to similar apps you use?
7. What features do you wish existed?
8. How important is [specific feature] to your usage?
9. Would you recommend the app to others? Why or why not?
10. What would make this app indispensable for you?

[Persona Generation - 8 personas]
1. Power User (daily, uses advanced features)
2. Casual User (weekly, basic features only)
3. New User (just started, still learning)
4. Former User (stopped using, switched to competitor)
5. Mobile-First User (primary device is phone)
6. Reluctant User (forced to use for work)
7. Feature Requester (active in feedback channels)
8. Silent Majority (typical usage, never contacts support)

[Simulation & Analysis]
8 interviews completed
Analysis: 3 runs with 'premium' tier (complex synthesis needed)

[Requirements Generated]
mobile-app-redesign-requirements.md

Priority 1 Features:
- Offline mode (requested by 7/8 users)
- Simplified navigation (pain point for 6/8)
- Dark mode (requested by 5/8)

Priority 2 Features:
- Custom dashboard
- Push notification controls
- Quick actions/shortcuts

Features to Deprecate:
- Social sharing (used by 0/8)
- In-app messaging (0/8 used, prefer email)

UX Improvements:
- Reduce steps for common tasks
- Add onboarding for new users
- Improve search functionality
```

---

## Example 3: E-commerce Checkout Optimization

**Scenario**: High cart abandonment rate during checkout.

### User Request
```
"Our checkout abandonment rate is 68%. I need to find out why users are 
leaving before completing purchases."
```

### Key Steps

```
[Study Creation]
Study: checkout-abandonment-study.xml
Focus: Checkout flow pain points, abandonment triggers, competitor comparison

[Questions - 7 focused questions]
1. Walk me through your last attempt to make a purchase
2. At what point did you consider abandoning your cart?
3. What information or features were you looking for during checkout?
4. How did the checkout process compare to your expectations?
5. What would have made you more likely to complete the purchase?
6. How does our checkout compare to other sites you shop on?
7. What's the ideal checkout experience for you?

[Personas - 5 targeted segments]
1. Price Sensitive Shopper (abandons if shipping too high)
2. Security Conscious (needs trust signals)
3. Mobile Shopper (struggles with mobile UX)
4. Impatient User (wants fastest possible checkout)
5. Research Shopper (saves carts, compares options)

[Analysis Results]
checkout-abandonment-requirements.md

Critical Issues:
1. Shipping costs hidden until final step (5/5 mentioned)
2. Account creation required (4/5 abandoned here)
3. Mobile form fields difficult to fill (3/5 on mobile)
4. No guest checkout option (4/5 wanted this)
5. Too many form fields (5/5 mentioned friction)

Quick Wins:
- Add guest checkout
- Show shipping costs earlier
- Reduce required fields
- Improve mobile form UX
- Add trust badges

Estimated Impact: 15-20% reduction in abandonment
```

---

## Example 4: SaaS Onboarding Improvement

**Scenario**: New users aren't activating key features during onboarding.

### User Request
```
"Only 30% of new signups complete our onboarding flow and activate 
core features. Need to fix this."
```

### Workflow Highlights

```
[Study Setup]
Study: saas-onboarding-improvement-study.xml
Target: New users (signed up in last 30 days)
Questions: 9 questions covering onboarding experience, feature discovery, 
           activation barriers

[Personas - 6 user types]
1. Technical User (wants to dive in immediately)
2. Non-Technical User (needs hand-holding)
3. Team Admin (setting up for whole team)
4. Trial User (evaluating for purchase)
5. Migrator (switching from competitor)
6. Returner (tried before, came back)

[Simulation: 6 interviews]
[Analysis: 4 runs with 'open_weights' tier]

[Key Findings]
saas-onboarding-requirements.md

Onboarding Failures:
1. Too many setup steps before value (avg 15 steps, users quit at step 7)
2. Unclear value proposition for each feature
3. No contextual help when stuck
4. Sample data not realistic enough
5. Can't skip steps to explore freely

Successful Patterns:
1. Users who saw quick win in first 5 minutes stayed
2. Video tutorials helped non-technical users
3. Progressive disclosure worked better than all-at-once

Recommendations:
1. Reduce to 3 critical setup steps
2. Add "quick start" path (skip to value)
3. Implement contextual tooltips
4. Improve sample data/templates
5. Add progress indicator with time estimates
6. Create role-based onboarding paths

Expected Outcome: 30% → 55% activation rate
```

---

## Example 5: API Developer Experience

**Scenario**: Developers are struggling with your API documentation and integration.

### User Request
```
"Our API has great functionality but developers say it's hard to use. 
Need to understand their pain points."
```

### Execution

```
[Study Creation]
Study: api-developer-experience-study.xml
Focus: Documentation quality, integration challenges, developer journey

[Questions - 8 technical questions]
1. Describe your experience integrating our API
2. What resources did you use (docs, examples, support)?
3. What was the most confusing or frustrating part?
4. How long did it take vs. your expectation?
5. What would have made integration easier?
6. How does our API compare to others you've used?
7. What's missing from our documentation?
8. Would you recommend our API to other developers?

[Personas - 5 developer profiles]
1. Senior Developer (experienced, high expectations)
2. Junior Developer (learning, needs more guidance)
3. Full-Stack Developer (wants quick integration)
4. Backend Specialist (deep technical requirements)
5. Freelancer (needs to deliver fast for client)

[Analysis Results]
api-developer-experience-requirements.md

Critical Pain Points:
1. Authentication flow unclear (5/5 struggled)
2. Error messages unhelpful (4/5 mentioned)
3. Code examples outdated (4/5 found errors)
4. No Postman collection available
5. Rate limiting not well documented

Documentation Issues:
- Examples only in one language (need more)
- No troubleshooting section
- Concepts explained before examples (backwards)
- Missing common use case guides
- No changelog for version differences

Required Improvements:
1. Rewrite authentication guide with step-by-step
2. Create comprehensive error message reference
3. Update all code examples (Python, JS, Ruby, Go)
4. Publish Postman collection
5. Add "Common Scenarios" section
6. Implement interactive API explorer
7. Create troubleshooting flowchart
8. Add video walkthrough for getting started

Priority Order: Auth docs → Error messages → Code examples → Postman
```

---

## Example 6: Background Research for Product Decision

**Scenario**: Deciding between two feature directions, need user input.

### User Request
```
"We're deciding between building an advanced search feature or an 
AI-powered recommendation engine. Which do users actually want?"
```

### Compact Example

```
[Study: feature-priority-study.xml]
Questions: 6 comparative questions about search vs recommendations

[4 Personas representing user segments]
[4 interviews completed]
[Analysis: 2 runs, 'open_weights' tier]

[Results: feature-priority-requirements.md]

Winner: AI Recommendations (3/4 preferred)
- But: users want basic search improvements first
- Recommendation: Phase 1 (search improvements), Phase 2 (AI recommendations)
- Timeline: Search (4 weeks), Recommendations (8 weeks after)

User Quotes Supporting Decision:
- "Search is broken, fix that first"
- "Recommendations sound cool but I need to find specific things"
- "Both would be great, but search is daily pain point"

Recommendation: Build improved search immediately, then add AI 
recommendations as Phase 2 using search infrastructure.
```

---

## Tips for Different Study Types

### Exploratory Research
```
- Use 8-10 open-ended questions
- Generate 6-8 diverse personas
- Run 3-4 analysis runs for depth
- Focus on "why" and "how" questions
```

### Validation Studies
```
- Use 5-7 targeted questions
- Generate 4-6 representative personas
- Run 2 analysis runs (faster)
- Focus on specific hypotheses
```

### Competitive Analysis
```
- Include comparison questions
- Generate personas familiar with competitors
- Ask about switching motivations
- Include questions about feature gaps
```

### Usability Testing
```
- Focus on task-based questions
- Include "walk me through" prompts
- Ask about pain points and confusion
- Generate personas with varying skill levels
```

### Requirements Gathering
```
- Mix current-state and future-state questions
- Include priority/ranking questions
- Ask about constraints and requirements
- Generate personas across user roles
```

---

## Common Patterns

### Quick Study (1-2 hours)
```
1. Create study → 10 minutes
2. Generate 5 questions → 5 minutes
3. Create 3 personas → 5 minutes
4. Run simulations → 10 minutes
5. Analyze (2 runs) → 20 minutes
6. Generate requirements → 10 minutes
Total: ~1 hour
```

### Comprehensive Study (half day)
```
1. Create study → 20 minutes (with stakeholder input)
2. Generate 10 questions → 10 minutes
3. Create 8 personas → 10 minutes
4. Run simulations → 20 minutes
5. Analyze (4 runs, premium tier) → 60 minutes
6. Generate requirements → 15 minutes
7. Create presentation → 30 minutes
Total: ~3 hours
```

### Ongoing Research Program
```
Weekly:
- Run 1-2 quick studies on current questions
- 3-4 personas each
- Fast analysis (1-2 runs)

Monthly:
- 1 comprehensive study
- 8-10 personas
- Deep analysis (4-5 runs)
- Full requirements doc

Quarterly:
- Synthesis of all studies
- Trend analysis
- Strategic recommendations
```

---

## Integration with Development Workflow

### Before Development
```
1. Research Study → Requirements Doc → Technical Spec → Development
   "Should we build feature X?" → Yes/No with requirements
```

### During Development
```
1. Prototype → Validation Study → Refinements → Ship
   "Does this design meet user needs?" → Iteration
```

### After Launch
```
1. Launch → Post-Launch Study → Improvements → Next Version
   "How's the feature performing?" → Optimization
```

---

## Collaborative Workflows

### With Product Team
```
Product Manager: Defines research questions
User Researcher Agent: Runs study, generates findings
Product Manager: Reviews requirements doc
Development Team: Implements based on requirements
```

### With Design Team
```
Designer: Creates mockups/prototypes
User Researcher Agent: Tests concepts with personas
Designer: Iterates based on feedback
Developer: Builds validated designs
```

### With Customer Success
```
CS Team: Identifies common support issues
User Researcher Agent: Investigates root causes
Product Team: Prioritizes fixes
CS Team: Validates solutions
```

---

## Next Steps

After completing a study:

1. **Share findings** with stakeholders
2. **Prioritize** recommendations (impact vs effort)
3. **Create tickets** for development work
4. **Schedule follow-up** research to validate changes
5. **Archive** study files for future reference

Files to keep:
- `{study-name}-study.xml` (for replication)
- `{study-name}-requirements.md` (for development)
- Interview transcripts (for quotes/evidence)
- Analysis results (for trend tracking)
