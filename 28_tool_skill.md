# Tool: Skill

Source: `src/tools/SkillTool/prompt.ts`

Skill tool prompts are defined in skill definition files (`.md` files with frontmatter) located in the `.claude/skills/` directory. Each skill has its own prompt that defines its behavior.

## Skill Structure

A skill file typically contains:
- Frontmatter with name, description, and metadata
- A prompt that defines the skill's behavior and instructions
- Optional shell commands embedded with `!` syntax for execution during skill loading

## Shell Execution in Skills

Skills support embedded shell commands:
- **Code blocks**: ` ```! command ``` `
- **Inline**: ` !`command` `

Permission checks are run before execution. Commands that fail permission checks throw a `MalformedCommandError`.

## See Also

- `src/utils/promptShellExecution.ts` for the shell execution logic
- `.claude/skills/` directory for built-in and custom skill definitions
