# Tool: TeamCreate

Source: `src/tools/TeamCreateTool/prompt.ts`

## When to Use

Use this tool proactively whenever:
- The user explicitly asks to use a team, swarm, or group of agents
- The user mentions wanting agents to work together, coordinate, or collaborate
- A task is complex enough that it would benefit from parallel work by multiple agents

When in doubt about whether a task warrants a team, prefer spawning a team.

## Choosing Agent Types for Teammates

- **Read-only agents** (e.g., Explore, Plan) cannot edit or write files. Only assign them research, search, or planning tasks.
- **Full-capability agents** (e.g., general-purpose) have access to all tools including file editing, writing, and bash.
- **Custom agents** defined in `.claude/agents/` may have their own tool restrictions.

## What TeamCreate Does

Creates a team + its task list:
- Team file at `~/.claude/teams/{team-name}/config.json`
- Corresponding task list directory at `~/.claude/tasks/{team-name}/`

## Team Workflow

1. **Create a team** with TeamCreate — this creates both the team and its task list
2. **Create tasks** using Task tools — they automatically use the team's task list
3. **Spawn teammates** using AgentTool with `team_name` and `name` parameters
4. **Assign tasks** using TaskUpdate with `owner` to give tasks to idle teammates
5. **Teammates work** on assigned tasks and mark them completed via TaskUpdate
6. **Teammates go idle** between turns — be patient! Don't comment on their idleness until it impacts your work.
7. **Shutdown your team** when the task is completed via SendMessage with `message: {type: "shutdown_request"}`.

## Task Ownership

Tasks are assigned using TaskUpdate with the `owner` parameter.

## Automatic Message Delivery

Messages from teammates are **automatically delivered** to you. You do NOT need to manually check your inbox. When you spawn teammates:
- They will send you messages when they complete tasks or need help
- These messages appear automatically as new conversation turns
- The UI shows a brief notification with the sender's name

## Teammate Idle State

Teammates go idle after every turn — this is **normal and expected**. Idle means they are waiting for input. Idle teammates can receive messages and will process them normally.

## Discovering Team Members

Teammates can read `~/.claude/teams/{team-name}/config.json` to discover other team members. The config contains a `members` array with each teammate's name, agentId, and agentType.

**Always refer to teammates by their NAME** (e.g., "team-lead", "researcher", "tester") when sending messages or assigning tasks.

## Task List Coordination

Teammates should:
1. Check TaskList periodically, **especially after completing each task**, to find available work
2. Claim unassigned tasks with TaskUpdate (set `owner` to your name). **Prefer tasks in ID order** (lowest ID first)
3. Create new tasks with TaskCreate when identifying additional work
4. Mark tasks completed with TaskUpdate when done
5. Coordinate with other teammates by reading the task list status

## Important Communication Notes

- **Do not use terminal tools** to view your team's activity — always send a message to teammates
- **Do NOT send structured JSON status messages** like `{"type":"idle",...}`. Just communicate in plain text.
- Use TaskUpdate to mark tasks completed.
