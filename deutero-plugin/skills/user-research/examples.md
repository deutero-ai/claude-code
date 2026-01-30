# User Research Skill - Examples

This file contains example outputs and common usage patterns for the user-research skill.

## Example 1: E-commerce Checkout Study

### Invocation
```
/user-research checkout abandonment in our e-commerce platform
```

### Expected Output

```
# User Research Study: Checkout Abandonment

## Study Overview

**Study Name:** E-commerce Checkout Abandonment Research
**Study ID:** abc-123-def-456-789

**Research Questions:**
1. What are the primary barriers preventing users from completing checkout?
2. At what specific steps do users abandon their carts?
3. How does our checkout experience compare to competitors?
4. What features or information are users looking for during checkout?

**Research Objectives:**
1. Identify top 3 abandonment triggers
2. Map the critical drop-off points in the checkout flow
3. Generate actionable UX improvements to reduce abandonment by 20%

**Target Users:** Online shoppers who added items to cart but didn't complete purchase in last 30 days

**Files Created:**
- checkout-abandonment-study.xml (saved)

Review the XML file and let me know when you're ready to generate interview questions.

---

[After user approval]

## Interview Questions Generated

I've created 7 targeted questions for the checkout study:

1. Can you walk me through the last time you added items to your cart on our site?
2. At what point in the checkout process did you consider abandoning your purchase?
3. What information or features were you looking for during checkout that you couldn't find?
4. How did our checkout experience compare to your expectations?
5. What would have made you more likely to complete the purchase?
6. Have you used other e-commerce sites recently? How did their checkout compare?
7. What would be your ideal checkout experience?

**Edit questions:** http://0.0.0.0:8000/edit-survey/?survey_id=abc-123-def-456-789
**Test interview:** http://localhost:8000/?survey_id=abc-123-def-456-789

Updated: checkout-abandonment-study.xml

Test the interview flow and let me know when you're ready to generate personas.

---

[After user approval]

## Personas Generated

Created 6 diverse personas for the study:

1. **Price-Sensitive Shopper** (ID: persona-001)
   - Frequently compares prices across sites
   - Abandons if shipping costs seem high
   - Budget-conscious, looks for deals

2. **Mobile-First User** (ID: persona-002)
   - Primarily shops on smartphone
   - Expects seamless mobile experience
   - Frustrated by complex forms on mobile

3. **Security-Conscious Buyer** (ID: persona-003)
   - Concerned about payment security
   - Looks for trust signals and SSL indicators
   - Abandons if site seems untrustworthy

4. **Impatient Professional** (ID: persona-004)
   - Wants fastest possible checkout
   - Values guest checkout option
   - Abandons if too many steps required

5. **Research-Oriented Shopper** (ID: persona-005)
   - Saves items to compare later
   - Rarely completes purchase on first visit
   - Uses cart as wishlist/comparison tool

6. **First-Time Buyer** (ID: persona-006)
   - New to the platform
   - Needs clear guidance and help
   - Uncertain about policies and processes

Running interviews for all 6 personas...

Simulations started. Interviews will complete in approximately 5 minutes.

---

[After monitoring completion]

## Interview Progress

All interviews completed successfully!

**Participation Statistics:**
- Total interviews: 6
- Completed: 6
- Incomplete: 0
- Completion rate: 100%

Ready to run thematic analysis. Recommended: 3 runs with 'premium' tier for reliable insights.

Proceed with analysis?

---

[After user approval]

## Thematic Analysis

Running thematic analysis...
- Model tier: premium
- Number of runs: 3
- Interviews being analyzed: 6

Analysis queued. This will take several minutes...

[Progress updates]

Analysis complete! Generating requirements document...

## Key Findings

### Critical Issues Identified

1. **Hidden Shipping Costs (5/6 personas mentioned)**
   - Shipping costs not shown until final checkout step
   - Users feel "tricked" when costs appear late
   - Major trigger for abandonment

2. **Forced Account Creation (4/6 personas mentioned)**
   - No guest checkout option
   - Users don't want to create account for one purchase
   - Mobile users especially frustrated by registration forms

3. **Mobile Form Complexity (3/6 mobile users)**
   - Form fields difficult to fill on mobile devices
   - Auto-fill doesn't work reliably
   - Keyboard covers important UI elements

4. **Lack of Trust Signals (4/6 personas noted)**
   - Security indicators not prominent
   - Return policy unclear during checkout
   - No visible customer reviews or testimonials

5. **Too Many Required Fields (5/6 personas)**
   - Excessive information requested
   - Unclear why certain fields are necessary
   - Process feels lengthy and invasive

### Quick Win Recommendations

1. **Show shipping costs earlier** (Estimated impact: 25% reduction in abandonment)
   - Display on cart page before checkout
   - Provide shipping calculator
   - Clear "free shipping" thresholds

2. **Add guest checkout** (Estimated impact: 20% reduction in abandonment)
   - One-click guest option
   - Optional account creation after purchase
   - Streamlined form (email + shipping only)

3. **Reduce required fields** (Estimated impact: 15% reduction in abandonment)
   - Mark optional fields clearly
   - Remove unnecessary data collection
   - Use smart defaults where possible

4. **Improve mobile UX** (Estimated impact: 30% reduction in mobile abandonment)
   - Larger touch targets
   - Better keyboard handling
   - Mobile-optimized field layouts

5. **Add trust signals** (Estimated impact: 10% reduction in abandonment)
   - Prominent SSL indicator
   - Return policy summary at checkout
   - Security badges from payment providers

### Implementation Priority

**Phase 1 (Week 1-2):**
- Add guest checkout option
- Show shipping costs on cart page
- Reduce required fields to minimum

**Phase 2 (Week 3-4):**
- Implement mobile form improvements
- Add trust signals and security badges
- Improve field auto-fill

**Phase 3 (Week 5-6):**
- Add shipping calculator
- Implement progress indicator
- A/B test variations

### Expected Outcomes

- **Overall abandonment reduction:** 15-20%
- **Mobile abandonment reduction:** 25-30%
- **Completion time improvement:** 30-40% faster
- **User satisfaction increase:** Significant (based on persona feedback)

## Files Created

1. **checkout-abandonment-study.xml** - Complete study specification
2. **checkout-abandonment-requirements.md** - Development requirements (optimized for LLM agents)

## Next Steps

1. Review the requirements document for full technical details
2. Prioritize implementation based on development capacity
3. Create tickets for Phase 1 quick wins
4. Schedule follow-up study after implementation to validate improvements
5. Set up analytics to track abandonment metrics

Would you like me to:
- Create more detailed implementation specifications?
- Generate user stories for the development team?
- Run additional research on specific findings?
```

## Example 2: Feature Adoption Study

### Invocation
```
/user-research new dashboard feature adoption
```

### Expected Flow

```
# User Research Study: Dashboard Feature Adoption

## Study Setup

I'll create a study to investigate low adoption of the new dashboard feature.

Business context: Enterprise SaaS product, new analytics dashboard launched 3 months ago
Research need: Understand why adoption is only 20% vs 60% target
Target users: IT managers, data analysts, business intelligence teams
Constraints: Need insights within 2 weeks for Q2 planning

[Creates study, saves XML file]

Study created: dashboard-adoption-study.xml

Generating 8 questions focused on awareness, trial barriers, and value perception...

[Generates questions, provides URLs for review]

Creating 8 diverse personas representing different user segments and adoption states...

[Creates personas: non-adopters, early adopters, churned users, etc.]

Running 8 interview simulations...

[Monitors progress, runs analysis with 4 runs]

## Analysis Results

### Major Adoption Barriers

1. **Awareness Gap (5/8 personas)**
   - Feature not prominently announced
   - No in-app notifications
   - Users didn't know it existed

2. **Unclear Value Proposition (6/8 personas)**
   - Benefits not obvious
   - Didn't understand how it helps their role
   - No clear ROI or time savings shown

3. **Steep Learning Curve (4/5 who tried)**
   - No onboarding or tutorial
   - Interface not intuitive
   - Takes too long to learn vs perceived value

4. **Integration Gaps (3/8 personas)**
   - Doesn't fit existing workflows
   - Can't export to preferred tools
   - Missing key data sources

[Provides detailed recommendations and requirements document]
```

## Example 3: Quick Validation Study

### Invocation
```
/user-research validate new search feature design with 4 personas
```

### Output Pattern

```
# Quick Validation Study: Search Feature Design

## Study Parameters

Based on your request:
- Topic: New search feature design validation
- Number of personas: 4 (as specified)
- Study type: Quick validation

Creating focused study...

[Generates study with 5 targeted questions]
[Creates 4 representative personas]
[Runs 2 analysis runs for faster turnaround]

## Validation Results (1-hour turnaround)

### User Sentiment: Positive (3/4 personas)

**What users liked:**
- Faster than current search
- Better filtering options
- Clean, uncluttered interface

**Concerns raised:**
- Advanced search needs more visibility (2/4)
- Results sorting could be clearer (1/4)
- Mobile layout needs work (1/4)

### Recommendations

**Ship with:**
- Current design for basic search
- Add tooltip for advanced search link

**Before next release:**
- Improve mobile responsive design
- Add sort options to results header

Decision: Validated for release with minor adjustments.
```

## Example 4: Resume Existing Study

### Invocation
```
/user-research abc-123-def-456-789
```

### Output
```
# Resuming Study: Mobile App Redesign

Detected existing survey_id: abc-123-def-456-789

Loading study details...

## Current Status

**Study:** Mobile App Redesign Research
**Questions:** 10 questions created ✓
**Personas:** 8 personas generated ✓
**Interviews:** 8/8 completed ✓
**Analysis:** Not yet run

You're ready for Phase 4: Thematic Analysis

Proceeding with analysis...

[Runs analysis and generates requirements]
```

## Common Usage Patterns

### Pattern 1: Full Research Study
```
/user-research [topic] → Review study → Approve questions → 
Generate personas → Run interviews → Analyze results → Review requirements
```

### Pattern 2: Quick Insights
```
/user-research [topic] with 3 personas and 5 questions → 
Fast turnaround for directional insights
```

### Pattern 3: Resume Workflow
```
/user-research [survey-id] → Continue from where you left off
```

### Pattern 4: Targeted Analysis
```
/user-research analyze results for [survey-id] → 
Skip to analysis phase with existing interviews
```

## Output File Examples

### Example XML File Structure
```xml
<?xml version="1.0" encoding="UTF-8"?>
<study>
  <study_id>abc-123-def-456-789</study_id>
  <study_name>Checkout Abandonment Research</study_name>
  <study_description>Investigate why users abandon shopping carts during checkout</study_description>
  <research_questions>
    <question id="1">What are the primary barriers preventing checkout completion?</question>
    <question id="2">At what steps do users abandon most frequently?</question>
  </research_questions>
  <interview_questions>
    <question id="1">
      <question_content>Can you walk me through your last checkout experience?</question_content>
    </question>
    <!-- Additional questions -->
  </interview_questions>
</study>
```

### Example Requirements Document Structure
```markdown
# Development Requirements: Checkout Abandonment Improvements

## Executive Summary
User research identified 5 critical barriers to checkout completion...

## User Needs
Based on interviews with 6 diverse user personas:

### Need 1: Transparent Pricing
**User Evidence:** "I hate when shipping costs surprise me at the end"
**Technical Requirement:** Display shipping costs on cart page...

## Implementation Requirements

### Quick Win 1: Guest Checkout
**Priority:** High
**Effort:** Medium
**Impact:** 20% reduction in abandonment

Technical specifications:
- Add "Continue as Guest" button on checkout page
- Minimal form: email, shipping address only
- Optional account creation post-purchase

[Additional detailed requirements...]
```

## Tips for Best Results

1. **Be specific in your research topic**
   - Good: "checkout abandonment on mobile devices"
   - Less good: "improve website"

2. **Specify persona count based on scope**
   - 3-5: Quick validation
   - 6-8: Standard research
   - 10+: Comprehensive study

3. **Review and edit between phases**
   - Test interview flow before simulations
   - Refine questions based on initial results
   - Adjust persona diversity if needed

4. **Choose analysis settings appropriately**
   - Quick insights: 2 runs, open_weights
   - Standard: 3 runs, premium
   - Critical decisions: 4-5 runs, frontier
