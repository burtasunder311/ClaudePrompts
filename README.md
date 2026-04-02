# Claude Code Prompts

Extracted from [claw-codes](https://github.com/A3S-Lab/claw-codes) repository.

## File Structure

| # | File | Description |
|---|------|-------------|
| 01 | `01_system_prefix.md` | Three CLI system prompt prefixes (default, SDK preset, SDK) |
| 02 | `02_coordinator_mode.md` | Multi-agent coordinator orchestration system prompt |
| 03 | `03_compact_summary.md` | Context compaction/summarization prompts |
| 04 | `04_agent_general_purpose.md` | General-purpose subagent |
| 05 | `05_agent_plan.md` | Read-only software architect/planning agent |
| 06 | `06_agent_verification.md` | Adversarial verification specialist agent |
| 07 | `07_agent_explore.md` | Fast read-only file search specialist |
| 08 | `08_agent_claude_code_guide.md` | Claude Code/SDK/API documentation guide agent |
| 09 | `09_tool_bash.md` | Bash command execution tool |
| 10 | `10_tool_file_read.md` | File read tool |
| 11 | `11_tool_file_write.md` | File write tool |
| 12 | `12_tool_file_edit.md` | File edit (string replacement) tool |
| 13 | `13_tool_glob.md` | Glob file pattern matching tool |
| 14 | `14_tool_grep.md` | Grep content search tool |
| 15 | `15_tool_web_search.md` | Web search tool |
| 16 | `16_tool_web_fetch.md` | Web fetch/content retrieval tool |
| 17 | `17_tool_agent.md` | Agent spawning tool |
| 18 | `18_tool_task_create.md` | Task creation tool |
| 19 | `19_tool_task_update.md` | Task update/status management tool |
| 20 | `20_tool_enter_plan_mode.md` | Enter plan mode tool |
| 21 | `21_tool_exit_plan_mode.md` | Exit plan mode tool |
| 22 | `22_tool_ask_user_question.md` | Ask user question (multi-choice) tool |
| 23 | `23_tool_team_create.md` | Team creation tool |
| 24 | `24_tool_send_message.md` | Send message to teammate tool |
| 25 | `25_tool_brief.md` | Brief/send user message tool |
| 26 | `26_tool_config.md` | Configuration settings tool |
| 27 | `27_tool_lsp.md` | Language Server Protocol tool |
| 28 | `28_tool_skill.md` | Skill invocation tool |
| 29 | `29_services_session_memory.md` | Session memory template and update prompt |
| 30 | `30_services_extract_memories.md` | Persistent memory extraction agent |
| 31 | `31_services_magic_docs.md` | Magic docs documentation update service |
| 32 | `32_services_prompt_suggestion.md` | User prompt suggestion service |
| 33 | `33_undercover_mode.md` | Open-source repo safety protocol |
| 34 | `34_companion.md` | Companion/buddy agent prompt |
| 35 | `35_tool_task_list.md` | Task list, task get, task stop tools |
| 36 | `36_tool_remaining.md` | Remaining tools (sleep, powershell, mcp, etc.) |
| 37 | `37_shell_execution_in_prompts.md` | Shell command execution in skill prompts |

## Categories

### System Prompts
- System prefix (identity)
- Coordinator mode (multi-agent orchestration)

### Built-in Agents (5 types)
- `general-purpose` — research and multi-step tasks
- `Plan` — read-only software architecture planning
- `verification` — adversarial testing/verification
- `Explore` — fast file search
- `claude-code-guide` — documentation lookup

### Tools (20+ types)
File operations, task management, agent spawning, team coordination, web search, LSP, skills, etc.

### Services
- Compact/summarization (context management)
- Session memory (conversation state persistence)
- Memory extraction (persistent knowledge)
- Magic docs (documentation updates)
- Prompt suggestion (next-user-input prediction)
