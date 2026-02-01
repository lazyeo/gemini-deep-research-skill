---
name: gemini-deep-research
description: Conduct deep research using Gemini's Deep Research feature via browser automation. Use when user requests comprehensive research, company analysis, market research, competitive analysis, or any task requiring multi-source investigation. Requires Gemini Advanced subscription. Includes completion monitoring to ensure results are captured.
---

# Gemini Deep Research

Automate Gemini's Deep Research feature for comprehensive multi-source investigations.

## Prerequisites
- Gemini Advanced subscription (logged in via browser)
- Browser profile `openclaw` with Google account authenticated

## Workflow

### Phase 1: Initiate Research

```
1. Open Gemini
   browser action=open profile=openclaw targetUrl="https://gemini.google.com/app"
   
2. Wait for page load (5s)
   
3. Dismiss any dialogs (press Escape)
   browser action=act request={kind:"press", key:"Escape"}

4. Click "Tools" button
   snapshot → find button "Tools" → click

5. Click "Deep Research" in the tools menu
   snapshot → find button "Deep Research" → click

6. Verify Deep Research mode active
   snapshot → confirm textbox shows "What do you want to research?"

7. Type research query
   browser action=act request={kind:"type", ref:"<textbox_ref>", text:"<RESEARCH_QUERY>"}

8. Submit query
   snapshot → find "Send message" button → click
```

### Phase 2: Approve Research Plan

```
1. Wait for research plan (10-15s)
   
2. Snapshot and verify plan appears
   Look for: "Here's the plan I've put together"
   
3. Click "Start research" button
   snapshot → find button "Start research" → click

4. Confirm research started
   Look for: "Starting research..." or "Researching X websites..."
```

### Phase 3: Monitor Completion (CRITICAL)

**Do NOT skip this phase.** Research typically takes 5-15 minutes.

**Timing strategy:**
- **First 5 minutes**: Silent wait (research never completes this fast)
- **After 5 minutes**: Poll every 30 seconds until complete or timeout (15 min max)

```
# Option A: Spawn a monitor sub-agent (RECOMMENDED)
sessions_spawn({
  task: "Monitor Gemini Deep Research completion. 
    1. Wait 5 minutes silently (research never completes faster)
    2. Then check browser every 30s for completion
    3. When complete, extract report and notify main session
    Browser targetId: <TARGET_ID>",
  label: "deep-research-monitor-<timestamp>",
  runTimeoutSeconds: 900  # 15 min max
})

# Option B: Polling loop (if spawn unavailable)
1. Sleep 5 minutes (research never finishes faster)
2. LOOP every 30 seconds for remaining 10 minutes:
   a. browser action=snapshot targetId=<TARGET_ID>
   b. Check for completion indicators:
      - "Completed" status text
      - "I've completed your research" message
      - "Writing your report..." (nearly done)
      - Absence of "Researching..." or "Analyzing..." 
   c. If complete → proceed to Phase 4
   d. If still running → continue loop
   e. If timeout → notify user with partial results from thinking process
```

**Completion indicators in snapshot:**
- `status` element containing "Completed"
- Message: "I've completed your research"
- Timestamp showing completion time (e.g., "Feb 2, 10:39 AM")

### Phase 4: Extract Results

```
1. Take final snapshot
   browser action=snapshot targetId=<TARGET_ID>

2. Report content is in the right panel
   - Heading: "Comprehensive..." or research title
   - Sections: h2/h3 headings with paragraph content
   - Sources: link elements at bottom

3. Export options (click "Share & Export" button if available)
   - Copy full text
   - Download as document

4. Save to FlashNotes
   Write extracted report to: FlashNotes/Research/<date>-<topic>.md
```

### Phase 5: Notify User

```
1. Send completion message with:
   - Summary of key findings
   - Link to saved report
   - Option to ask follow-up questions

2. Keep browser tab open for follow-ups
```

## Research Query Templates

### Company Research (Job Application)
```
Research [COMPANY_NAME] ([LOCATION]):

1. Company business: What does [COMPANY] do? Products, technology, target markets
2. Company culture & work environment: Employee reviews on Glassdoor/LinkedIn, work-life balance
3. Company reputation: Industry standing, news, growth trajectory
4. For their [JOB_TITLE] role: requirements, candidate profile, salary range
5. Red flags or concerns about working there

Provide comprehensive analysis for a job applicant.
```

### Technology/Tool Research
```
Research [TECHNOLOGY/TOOL]:

1. What is it and what problem does it solve?
2. Key features and capabilities
3. Comparison with alternatives
4. Pricing and licensing
5. Community adoption and support
6. Getting started guide

Target audience: [DEVELOPER/BUSINESS/etc]
```

### Market Research
```
Research the [INDUSTRY/MARKET] in [REGION]:

1. Market size and growth trends
2. Key players and market share
3. Emerging trends and disruptions
4. Regulatory environment
5. Opportunities and challenges
6. Future outlook (3-5 years)
```

## Timing Expectations

| Phase | Duration |
|-------|----------|
| Plan generation | 10-20 seconds |
| Plan approval | Instant (click) |
| Research execution | 3-8 minutes |
| Results analysis | 2-5 minutes |
| Report writing | 1-2 minutes |
| **Total typical** | **8-15 minutes** |

**Key insight:** Research never completes in under 5 minutes. Start monitoring after 5 min to save API calls.

## Error Handling

| Error | Solution |
|-------|----------|
| Login required | Open gemini.google.com manually, complete login, retry |
| Deep Research not available | Verify Gemini Advanced subscription active |
| Research stuck | Check for "Stop response" button, may need to restart |
| Browser timeout | Increase wait times, check network connectivity |
| Empty results | Research may have failed, check for error messages |

## Output Format

Save all research reports to:
```
FlashNotes/Research/<YYYY-MM-DD>-<topic-slug>.md
```

Include metadata header:
```markdown
# [Research Title]
*Generated via Gemini Deep Research | <date> <time> NZT*
*Query: [original query]*
*Duration: ~X minutes*
*Sources: X websites analyzed*

---
[Report content]
---
*Report generated by Lava 🌋 via Gemini Deep Research*
```
