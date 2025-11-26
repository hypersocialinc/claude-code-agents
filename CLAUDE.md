# Claude Code Agents

Custom subagents for Claude Code.

## Why This Exists

**Problem:** When building new features, you often want to reference how you implemented something similar in another project. But:
- Starter repos get stale and don't reflect your latest patterns
- Dumping raw GitHub search results into Claude Code pollutes your context window
- Manually searching across repos is tedious

**Solution:** Subagents run in isolated contexts. The `extract-pattern` agent searches your GitHub repos, synthesizes the findings, and returns only a concise summary to your main conversation. This keeps your main context clean while giving you access to patterns from all your projects.

## Prerequisites

### Required

- **GitHub CLI (`gh`)** - authenticated with access to your repos
  ```bash
  brew install gh
  gh auth login
  ```

### Optional

- **Context7 MCP** - for fetching external library documentation alongside your code patterns
  - Setup: https://github.com/upstash/context7

## Structure

```
agents/           # Subagent prompt files (.md)
  extract-pattern.md
README.md         # User-facing documentation
LICENSE           # MIT
```

## Agent File Format

Each agent is a markdown file with YAML frontmatter:

```yaml
---
name: agent-name
description: Short description for agent selection
tools: Bash, Read, ...  # Comma-separated tool access
model: sonnet           # haiku | sonnet | opus
---
```

The body contains the agent's system prompt with instructions.

## Adding New Agents

1. Create `agents/{agent-name}.md` with frontmatter + prompt
2. Document in README.md under "Available Agents"
3. Test by installing to `~/.claude/agents/` and invoking in Claude Code
