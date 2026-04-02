# Tool: Agent

Source: `src/tools/AgentTool/prompt.ts`

## Description

```
Launch a new agent to handle complex, multi-step tasks autonomously.

The AgentTool launches specialized agents (subprocesses) that autonomously handle complex tasks. Each agent type has specific capabilities and tools available to it.
```

## Available Agent Types

```
Available agent types and the tools they have access to:
- general-purpose: General-purpose agent for researching complex questions, searching for code, and executing multi-step tasks
- Plan: Software architect agent for designing implementation plans (READ-ONLY)
- verification: Adversarial verification specialist (READ-ONLY)
- Explore: Fast file search specialist (READ-ONLY)
- claude-code-guide: Help users understand Claude Code/SDK/API
- [custom agents from .claude/agents/]
```

## When to Use

Use the Agent tool when:
- You need to research complex questions requiring multiple search strategies
- A task is complex enough that it would benefit from parallel work by multiple agents
- You need specialized behavior (verification, planning, exploration)

## When NOT to Use

- If you want to read a specific file path → use Read tool
- If you are searching for a specific class definition → use Glob/Grep tool
- If you are searching for code within a specific file → use Read tool

## Usage Notes

- Always include a short description (3-5 words) summarizing what the agent will do
- Launch multiple agents concurrently whenever possible to maximize performance
- When the agent is done, it will return a single message back to you — to show the user the result, send a text message
- To continue a previously spawned agent, use SendMessageTool with the agent's ID or name as `to` field
- Clearly tell the agent whether you expect it to write code or just to do research
- You can optionally set `isolation: "worktree"` to run the agent in a temporary git worktree

## Fork vs. Subagent (when fork feature enabled)

- **Fork (omit subagent_type)**: When intermediate tool output isn't worth keeping in your context. Shares your prompt cache. Don't set `model` on a fork.
- **Subagent (with subagent_type)**: Starts with zero context. Use for fresh independent analysis.

## Writing the Prompt

Brief the agent like a smart colleague who just walked into the room — it hasn't seen this conversation:
- Explain what you're trying to accomplish and why
- Describe what you've already learned or ruled out
- Give enough context for the agent to make judgment calls
- If you need a short response, say so

**Never delegate understanding**: Don't write "based on your findings, fix the bug." Those phrases push synthesis onto the agent. Write prompts that prove you understood: include file paths, line numbers, what specifically to change.

## Example

```
<example>
user: "What's left on this branch before we can ship?"
assistant: <thinking>Forking this — it's a survey question.</thinking>
AgentTool({
  name: "ship-audit",
  description: "Branch ship-readiness audit",
  prompt: "Audit what's left before this branch can ship. Check: uncommitted changes, commits ahead of main, whether tests exist, whether the GrowthBook gate is wired up, whether CI-relevant files changed. Report a punch list — done vs. missing. Under 200 words."
})
assistant: Ship-readiness audit running.
</example>
```
