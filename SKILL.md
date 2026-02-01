---
name: gemini-deep-research
description: Use when conducting comprehensive multi-source research requiring 50-100+ website analysis, company due diligence, market research, or technical deep-dives via Gemini Deep Research.
---

# Gemini Deep Research

Automate Gemini's Deep Research feature for comprehensive multi-source investigations with smart monitoring.

## Core Principle
**Research is a marathon, not a sprint.** Never accept a "Still researching" state as a final result. Wait for the comprehensive report synthesis.

## When to Use
- **Company Analysis**: Deep dive for job applications or investment.
- **Market Research**: Competitive landscape and industry trends.
- **Tech Evaluation**: Comparison of tools, frameworks, or platforms.

## Workflow

### 1. Initiate & Plan
- Open `https://gemini.google.com/app` (Profile: `openclaw`).
- Navigate to **Tools > Deep Research**.
- Input query and **Approve the Plan**.

### 2. Smart Monitoring (Condition-Based Waiting)
Research takes 8-15 minutes. 
- **Wait 5 minutes silently** before first check (save tokens).
- Then poll every 30-60s for completion status.

### 3. Extraction
Extract full report content, citations, and sources. Save to `FlashNotes/Research/`.

## Rationalization Table

| Agent Excuse | Reality |
|--------------|---------|
| "It's taking too long, I'll just summarize the thinking process." | Thinking process is incomplete. Only the final report contains the full synthesis. |
| "I'll check every 10 seconds to be sure." | Waste of context and API calls. Research never finishes under 5 minutes. |
| "The plan looks fine, I won't check it." | Gemini might need clarification. Always verify the plan started. |

## Red Flags
- 🚩 Reporting "Done" while status is still "Analyzing..." or "Researching...".
- 🚩 Failing to extract the "Sources" section at the end.
- 🚩 Checking status more than 10 times in the first 5 minutes.

## Implementation Example
 Partner: "Research Seequent for my application."
 You: "Starting Deep Research... (Monitoring in background)"
 [Wait 5 min] -> [Poll] -> [Complete]
 You: "Research complete. Saved to FlashNotes/Research/2026-02-02-Seequent.md"
