# Claude Code Agents

Custom subagents for [Claude Code](https://claude.com/claude-code) that extend its capabilities with specialized tools and workflows.

**Author:** Selcuk Atli (selcuk.atli@gmail.com)

## Why Use Subagents?

Claude Code subagents run in **isolated contexts**, meaning:

- **Clean main context**: Heavy search operations happen in the subagent, returning only synthesized findings
- **Token efficiency**: ~8x cleaner context vs dumping raw search results into your main conversation
- **Specialized prompts**: Each subagent is optimized for its specific task
- **Cost savings**: Subagents can use lighter models (like Sonnet) for research tasks

## Available Agents

### `extract-pattern`

Search your GitHub repositories for implementation patterns and code examples.

**Use cases:**
- "How did we implement authentication in project X?"
- "Find our Stripe checkout integration pattern"
- "What's our standard webhook handler structure?"
- Onboarding new team members to existing patterns
- Ensuring consistency across multiple projects
- Avoiding reinventing solutions you've already built

**Features:**
- Auto-discovers repos in your GitHub org
- Searches code across multiple repos
- Fetches and decodes file contents
- Integrates with [Context7 MCP](https://github.com/upstash/context7) for external library documentation

## Installation

1. Create the agents directory (if it doesn't exist):

```bash
mkdir -p ~/.claude/agents
```

2. Copy the agent file(s) you want:

```bash
# Option 1: Clone the repo and copy
git clone https://github.com/hypersocialinc/claude-code-agents.git
cp claude-code-agents/agents/extract-pattern.md ~/.claude/agents/

# Option 2: Download directly
curl -o ~/.claude/agents/extract-pattern.md \
  https://raw.githubusercontent.com/hypersocialinc/claude-code-agents/main/agents/extract-pattern.md
```

3. Restart Claude Code to load the new agent.

## Usage

Once installed, the agent is automatically available. Claude Code will invoke it when appropriate, or you can reference it explicitly:

```
"Use the extract-pattern agent to find how we handle user profiles in our repos"
```

```
"Search my-org repos for the Clerk webhook implementation pattern"
```

## Customization

### Hardcode your GitHub org

If you always search the same org, edit the agent file to hardcode it:

```markdown
## How to Search

### 1. Search repos in your org
gh repo list YOUR_ORG_HERE --limit 50 --json name
```

### Change the model

Edit the frontmatter to use a different model:

```yaml
model: haiku    # Faster, cheaper
model: sonnet   # Balanced (default)
model: opus     # Most capable
```

## Prerequisites

- **GitHub CLI (`gh`)**: Must be installed and authenticated
  ```bash
  brew install gh
  gh auth login
  ```

- **Context7 MCP** (optional): For external library documentation
  - [Setup instructions](https://github.com/upstash/context7)

## Contributing

Contributions welcome! Feel free to:
- Add new agents
- Improve existing agent prompts
- Fix bugs or improve documentation

## License

MIT License - see [LICENSE](LICENSE) for details.
