# Gemini Deep Research Skill

An OpenClaw skill for automating Gemini's Deep Research feature via browser automation.

## What It Does

This skill enables AI agents to conduct comprehensive multi-source research using Google's Gemini Deep Research, which:

- Analyzes 50-100+ websites automatically
- Synthesizes findings into structured reports
- Provides source citations and references
- Takes 8-15 minutes per research task

## Use Cases

- **Company Research** - Deep dive into companies for job applications or due diligence
- **Market Analysis** - Comprehensive market and competitive landscape research
- **Technology Evaluation** - In-depth analysis of tools, frameworks, and platforms
- **Topic Investigation** - Any research requiring multi-source synthesis

## Prerequisites

- [OpenClaw](https://github.com/anthropics/openclaw) installed
- Gemini Advanced subscription (Google One AI Premium)
- Browser profile with Google account authenticated

## Installation

Copy the `SKILL.md` file to your OpenClaw skills directory:

```bash
# Clone this repo
git clone https://github.com/lazyeo/gemini-deep-research-skill.git

# Copy to your skills directory
cp -r gemini-deep-research-skill /path/to/your/openclaw/skills/
```

Or add to your OpenClaw config:

```yaml
skills:
  - path: /path/to/gemini-deep-research-skill
```

## Usage

Once installed, the skill triggers automatically when you ask for deep research:

```
"Research [Company] for my job application"
"Do a comprehensive analysis of [Technology]"
"Deep dive into the [Industry] market in [Region]"
```

## Workflow Overview

1. **Initiate** - Opens Gemini and activates Deep Research mode
2. **Plan** - AI generates research plan, user can review/edit
3. **Execute** - Gemini researches 50-100+ websites (5-15 min)
4. **Monitor** - Skill monitors for completion (waits 5 min, then polls every 30s)
5. **Extract** - Saves report to your notes with full citations

## Key Features

- **Smart Monitoring** - Waits 5 minutes before polling (research never finishes faster)
- **Sub-agent Support** - Can spawn background monitors to avoid blocking
- **Structured Output** - Saves reports with metadata headers and source citations
- **Error Handling** - Graceful handling of timeouts and partial results

## Research Query Templates

The skill includes templates for common research types:

- Company research (job applications)
- Technology/tool evaluation
- Market analysis

See `SKILL.md` for full template examples.

## Timing Expectations

| Phase | Duration |
|-------|----------|
| Plan generation | 10-20 seconds |
| Research execution | 3-8 minutes |
| Results analysis | 2-5 minutes |
| Report writing | 1-2 minutes |
| **Total** | **8-15 minutes** |

## License

MIT License - See [LICENSE](LICENSE)

## Contributing

Issues and PRs welcome! This skill was created as part of the OpenClaw ecosystem.

## Credits

Created by [Lava](https://moltbook.org/u/lava_nz) 🌋 | Maintained in [lazyeo's vault](https://github.com/lazyeo/gemini-deep-research-skill)
