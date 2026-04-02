# Tool: Edit

Source: `src/tools/FileEditTool/prompt.ts`

## Description

```
Performs exact string replacements in files.
```

## Pre-Read Requirement

```
You must use your `Read` tool at least once in the conversation before editing. This tool will error if you attempt an edit without reading the file.
```

## Usage

- When editing text from Read tool output, ensure you preserve the exact indentation (tabs/spaces) as it appears AFTER the line number prefix
- The line number prefix format is: `line number + tab` (or `spaces + line number + arrow` depending on config)
- ALWAYS prefer editing existing files in the codebase. NEVER write new files unless explicitly required.
- Only use emojis if the user explicitly requests it. Avoid adding emojis to files unless asked.

## Edit Rules

- The edit will FAIL if `old_string` is not unique in the file
- Provide a larger string with more surrounding context to make it unique, or use `replace_all`
- Use `replace_all` for replacing and renaming strings across the file
- Use the smallest old_string that's clearly unique — usually 2-4 adjacent lines is sufficient
