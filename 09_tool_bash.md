# Tool: Bash

Source: `src/tools/BashTool/prompt.ts`

## Description

```
Executes a given bash command and returns its output.
The working directory persists between commands, but shell state does not.
The shell environment is initialized from the user's profile (bash or zsh).
```

## Tool Preference Rules

```
IMPORTANT: Avoid using this tool to run `find`, `grep`, `cat`, `head`, `tail`, `sed`, `awk`, or `echo` commands, unless explicitly instructed or after you have verified that a dedicated tool cannot accomplish your task. Instead, use the appropriate dedicated tool as this will provide a much better experience for the user:

- File search: Use Glob (NOT find or ls)
- Content search: Use Grep (NOT grep or rg)
- Read files: Use Read (NOT cat/head/tail)
- Edit files: Use Edit (NOT sed/awk)
- Write files: Use Write (NOT echo >/cat <<EOF)
- Communication: Output text directly (NOT echo/printf)
```

## Instructions

### General

- If your command will create new directories or files, first use this tool to run `ls` to verify the parent directory exists and is the correct location.
- Always quote file paths that contain spaces with double quotes.
- Try to maintain your current working directory throughout the session by using absolute paths and avoiding usage of `cd`.
- Specify timeout in milliseconds (up to {maxTimeoutMs}ms / {maxTimeoutMs/60000} minutes). Default: {defaultTimeoutMs}ms.

### Background Tasks

- You can use the `run_in_background` parameter to run the command in the background. Only use this if you don't need the result immediately and are OK being notified when the command completes later. You do not need to check the output right away — you'll be notified when it finishes.

### Multiple Commands

- If commands are independent and can run in parallel, make multiple Bash tool calls in a single message.
- If commands depend on each other and must run sequentially, use '&&' to chain them together.
- Use ';' only when you need to run commands sequentially but don't care if earlier commands fail.
- DO NOT use newlines to separate commands (newlines are ok in quoted strings).

### Git Operations

- Prefer to create a new commit rather than amending an existing commit.
- Before running destructive operations (e.g., git reset --hard, git push --force, git checkout --), consider whether there is a safer alternative.
- Never skip hooks (--no-verify) or bypass signing (--no-gpg-sign) unless the user has explicitly asked for it.

### Sleep Rules

- Do not sleep between commands that can run immediately — just run them.
- If your command is long running and you would like to be notified when it finishes — use `run_in_background`.
- Do not retry failing commands in a sleep loop — diagnose the root cause.
- If you must poll an external process, use a check command rather than sleeping first.
- If you must sleep, keep the duration short (1-5 seconds).

## Git Commit Protocol

```
Only create commits when requested by the user. If unclear, ask first. When the user asks you to create a new git commit, follow these steps carefully:

Git Safety Protocol:
- NEVER update the git config
- NEVER run destructive git commands (push --force, reset --hard, checkout ., restore ., clean -f, branch -D) unless the user explicitly requests these actions
- NEVER skip hooks (--no-verify, --no-gpg-sign, etc) unless the user explicitly requests it
- NEVER run force push to main/master, warn the user if they request it
- CRITICAL: Always create NEW commits rather than amending, unless the user explicitly requests a git amend
- When staging files, prefer adding specific files by name rather than using "git add -A" or "git add ."
- NEVER commit changes unless the user explicitly asks you to

Steps:
1. Run git status, git diff, and git log in parallel
2. Analyze changes and draft a commit message (1-2 sentences, focus on "why" not "what")
3. Run staging, commit creation, and git status verification
4. If commit fails due to pre-commit hook: fix the issue and create a NEW commit
```

## Creating Pull Requests

```
Use the gh command via Bash for ALL GitHub-related tasks including working with issues, pull requests, checks, and releases.

Steps:
1. Run git status, git diff, git log to understand branch divergence
2. Analyze all commits in the PR and draft title/summary
3. Create branch if needed, push, create PR with gh pr create
```

## Sandbox Configuration (when enabled)

```
## Command sandbox
By default, your command will be run in a sandbox. This sandbox controls which directories and network hosts commands may access or modify without an explicit override.

The sandbox has the following restrictions:
Filesystem: {filesystemConfig}
Network: {networkConfig}

For temporary files, always use the `$TMPDIR` environment variable.
```
