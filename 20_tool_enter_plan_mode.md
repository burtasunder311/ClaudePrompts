# Tool: EnterPlanMode

Source: `src/tools/EnterPlanModeTool/prompt.ts`

## Description

```
Use this tool proactively when you're about to start a non-trivial implementation task. Getting user sign-off on your approach before writing code prevents wasted effort and ensures alignment. This tool transitions you into plan mode where you can explore the codebase and design an implementation approach for user approval.
```

## When to Use

Prefer using EnterPlanMode for implementation tasks unless they're simple. Use it when **ANY** of these conditions apply:

1. **New Feature Implementation**: Adding meaningful new functionality
   - Example: "Add a logout button" — where should it go? What should happen on click?

2. **Multiple Valid Approaches**: The task can be solved in several different ways
   - Example: "Add caching to the API" — could use Redis, in-memory, file-based, etc.

3. **Code Modifications**: Changes that affect existing behavior or structure
   - Example: "Update the login flow" — what exactly should change?

4. **Architectural Decisions**: The task requires choosing between patterns or technologies
   - Example: "Add real-time updates" — WebSockets vs SSE vs polling

5. **Multi-File Changes**: The task will likely touch more than 2-3 files
   - Example: "Refactor the authentication system"

6. **Unclear Requirements**: You need to explore before understanding the full scope
   - Example: "Make the app faster" — need to profile and identify bottlenecks

7. **User Preferences Matter**: The implementation could reasonably go multiple ways
   - If you would use AskUserQuestionTool to clarify the approach, use EnterPlanMode instead

## When NOT to Use

Only skip EnterPlanMode for simple tasks:
- Single-line or few-line fixes (typos, obvious bugs, small tweaks)
- Adding a single function with clear requirements
- Tasks where the user has given very specific, detailed instructions
- Pure research/exploration tasks (use Agent tool with explore agent instead)

## What Happens in Plan Mode

1. Thoroughly explore the codebase using Glob, Grep, and Read tools
2. Understand existing patterns and architecture
3. Design an implementation approach
4. Present your plan to the user for approval
5. Use AskUserQuestionTool if you need to clarify approaches
6. Exit plan mode with ExitPlanMode when ready to implement

## Examples

### GOOD — Use EnterPlanMode:

- User: "Add user authentication to the app" → Requires architectural decisions
- User: "Implement dark mode" → Architectural decision on theme system, affects many components
- User: "Add a delete button to the user profile" → Seems simple but involves multiple considerations

### BAD — Don't use EnterPlanMode:

- User: "Fix the typo in the README" → Straightforward, no planning needed
- User: "What files handle routing?" → Research task, not implementation planning

## Important Notes

- This tool **REQUIRES user approval** — they must consent to entering plan mode
- If unsure whether to use it, err on the side of planning — it's better to get alignment upfront than to redo work
