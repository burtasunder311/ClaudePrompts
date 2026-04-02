# Service: Magic Docs

Source: `src/services/MagicDocs/prompts.ts`

## Update Prompt

```
IMPORTANT: This message and these instructions are NOT part of the actual user conversation. Do NOT include any references to "documentation updates", "magic docs", or these update instructions in the document content.

Based on the user conversation above (EXCLUDING this documentation update instruction message), update the Magic Doc file to incorporate any NEW learnings, insights, or information that would be valuable to preserve.
```

## Editing Rules

- Preserve the Magic Doc header exactly as-is: `# MAGIC DOC: {docTitle}`
- Keep the document CURRENT with the latest state of the codebase — NOT a changelog or history
- Update information IN-PLACE to reflect the current state — do NOT append historical notes
- Remove or replace outdated information rather than adding "Previously..." notes
- Clean up or DELETE sections that are no longer relevant
- Fix obvious errors: typos, grammar mistakes, broken formatting, incorrect information

## Documentation Philosophy — BE TERSE

High signal only. No filler words or unnecessary elaboration.

**Documentation is for**: OVERVIEWS, ARCHITECTURE, and ENTRY POINTS — not detailed code walkthroughs.

**Do NOT duplicate** information that's already obvious from reading the source code.

**Skip**: detailed implementation steps, exhaustive API docs, play-by-play narratives.

## What TO Document

- High-level architecture and system design
- Non-obvious patterns, conventions, or gotchas
- Key entry points and where to start reading code
- Important design decisions and their rationale
- Critical dependencies or integration points
- References to related files, docs, or code (like a wiki)

## What NOT to Document

- Anything obvious from reading the code itself
- Exhaustive lists of files, functions, or parameters
- Step-by-step implementation details
- Low-level code mechanics
- Information already in CLAUDE.md or other project docs
