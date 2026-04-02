# Shell Execution in Prompts

Source: `src/utils/promptShellExecution.ts`

## Overview

Parses prompt text and executes embedded shell commands. Supports two syntaxes:
- **Code blocks**: ` ```! command ``` `
- **Inline**: ` !`command` `

## Execution Flow

1. Parse the prompt text for both block and inline shell patterns
2. For each match, check permissions before executing
3. Execute via BashTool (or PowerShellTool if configured)
4. Replace the command in the prompt with its output
5. Return the modified prompt text

## Patterns

```typescript
// Code block pattern
const BLOCK_PATTERN = /```!\s*\n?([\s\S]*?)\n?```/g

// Inline pattern (positive lookbehind for !`command`)
const INLINE_PATTERN = /(?<=^|\s)!`([^`]+)`/gm
```

## Permission Checks

Before executing any shell command:
1. Call `hasPermissionsToUseTool` with the shell tool
2. If permission denied, throw `MalformedCommandError`
3. If command succeeds, process the result block

## Shell Selection

- `shell === 'powershell'` → PowerShellTool (if enabled)
- Default → BashTool
- The shell choice comes from `.md` frontmatter (`shell: powershell`), NOT from settings

## Error Handling

- `MalformedCommandError`: Re-thrown immediately (does not suppress)
- `ShellError`: Formatted output with stderr, then thrown
- Other errors: Formatted as `[Error: message]`

## Output Formatting

```typescript
// Stdout only
"command output"

// With stderr (separate lines)
"command output\n[stderr]\nstderr content"

// Inline with stderr
"command output [stderr: stderr content]"
```
