# Tool: Sleep

Source: `src/tools/SleepTool/prompt.ts`

## Description

Introduces a delay in execution. Used for rate limiting or deliberate pacing.

## Rules

- Do not sleep between commands that can run immediately — just run them
- If you must sleep, keep the duration short (1-5 seconds) to avoid blocking the user
- Use `run_in_background` on Bash for long-running commands instead of polling with sleep

---

# Tool: PowerShell

Source: `src/tools/PowerShellTool/prompt.ts`

## Description

Executes PowerShell commands on Windows. Similar to BashTool but uses PowerShell runtime.

---

# Tool: ToolSearch

Source: `src/tools/ToolSearchTool/prompt.ts`

## Description

Search for available tools. Useful for discovering MCP tools or other dynamically registered tools.

---

# Tool: EnterWorktree / ExitWorktree

Source: `src/tools/EnterWorktreeTool/prompt.ts` / `src/tools/ExitWorktreeTool/prompt.ts`

## Description

Manage git worktrees for isolated agent execution.

- `EnterWorktree`: Creates a temporary git worktree with an isolated copy of the repository
- `ExitWorktree`: Exits the worktree and optionally cleans it up

The worktree is automatically cleaned up if the agent makes no changes; if changes are made, the worktree path and branch are returned.

---

# Tool: NotebookEdit

Source: `src/tools/NotebookEditTool/prompt.ts`

## Description

Edits Jupyter notebooks (.ipynb files). Can add, replace, or delete cells in a notebook.

---

# Tool: RemoteTrigger

Source: `src/tools/RemoteTriggerTool/prompt.ts`

## Description

Triggers remote operations or callbacks. Used for cross-session or remote execution scenarios.

---

# Tool: ScheduleCron

Source: `src/tools/ScheduleCronTool/prompt.ts`

## Description

Schedules prompts to run at recurring intervals using cron syntax.

---

# Tool: MCP (Model Context Protocol)

Source: `src/tools/MCPTool/prompt.ts`

## Description

Prompts for MCP tools are dynamically loaded from the MCP server configuration. The prompt content is defined by the MCP server and not statically defined in Claude Code.

---

# Tool: ListMcpResources / ReadMcpResource

Source: `src/tools/ListMcpResourcesTool/prompt.ts` / `src/tools/ReadMcpResourceTool/prompt.ts`

## Description

List and read resources provided by MCP servers.
