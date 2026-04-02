# Compact / Context Summarization Prompts

Source: `src/services/compact/prompt.ts`

## No-Tools Preamble

```
CRITICAL: Respond with TEXT ONLY. Do NOT call any tools.

- Do NOT use Read, Bash, Grep, Glob, Edit, Write, or ANY other tool.
- You already have all the context you need in the conversation above.
- Tool calls will be REJECTED and will waste your only turn — you will fail the task.
- Your entire response must be plain text: an <analysis> block followed by a <summary> block.
```

---

## Base Compact Prompt (Full Conversation)

```
Your task is to create a detailed summary of the conversation so far, paying close attention to the user's explicit requests and your previous actions.
This summary should be thorough in capturing technical details, code patterns, and architectural decisions that would be essential for continuing development work without losing context.

Before providing your final summary, wrap your analysis in <analysis> tags to organize your thoughts and ensure you've covered all necessary points.

Your summary should include the following sections:

1. Primary Request and Intent: Capture all of the user's explicit requests and intents in detail
2. Key Technical Concepts: List all important technical concepts, technologies, and frameworks discussed.
3. Files and Code Sections: Enumerate specific files and code sections examined, modified, or created. Pay special attention to the most recent messages and include full code snippets where applicable.
4. Errors and fixes: List all errors that you ran into, and how you fixed them. Pay special attention to specific user feedback that you received.
5. Problem Solving: Document problems solved and any ongoing troubleshooting efforts.
6. All user messages: List ALL user messages that are not tool results.
7. Pending Tasks: Outline any pending tasks that you have explicitly been asked to work on.
8. Current Work: Describe in detail precisely what was being worked on immediately before this summary request.
9. Optional Next Step: List the next step that you will take that is related to the most recent work you were doing. IMPORTANT: ensure that this step is DIRECTLY in line with the user's most recent explicit requests.

Output structure:

<analysis>
[Your thought process]
</analysis>

<summary>
1. Primary Request and Intent:
   [Detailed description]

2. Key Technical Concepts:
   - [Concept 1]
   - [Concept 2]

3. Files and Code Sections:
   - [File Name 1]
      - [Summary of why this file is important]
      - [Summary of changes made]
      - [Important Code Snippet]

4. Errors and fixes:
    - [Error description]:
      - [How you fixed it]
      - [User feedback if any]

5. Problem Solving:
   [Description]

6. All user messages:
    - [Message]

7. Pending Tasks:
   - [Task 1]

8. Current Work:
   [Precise description]

9. Optional Next Step:
   [Next step or omit if task is complete]
</summary>
```

---

## Partial Compact Prompt (Recent Messages Only)

Same structure as Base, but scopes to RECENT messages (the messages that follow earlier retained context). Used when context window is being compacted and earlier messages are being kept.

---

## Compact Up-To Prompt (Cache Hit Path)

Used when `up_to` direction — model sees only the summarized prefix. Summary precedes kept recent messages.

Includes "Work Completed" and "Context for Continuing Work" sections instead of "Current Work".

---

## Trailer (Appplied to All Variants)

```
REMINDER: Do NOT call any tools. Respond with plain text only —
an <analysis> block followed by a <summary> block.
Tool calls will be rejected and you will fail the task.
```

---

## Session Continuation Message

When resuming a compacted session:

```
This session is being continued from a previous conversation that ran out of context. The summary below covers the earlier portion of the conversation.

{Summary}

[If transcript path available]
If you need specific details from before compaction (like exact code snippets, error messages, or content you generated), read the full transcript at: {transcriptPath}

[If recent messages preserved]
Recent messages are preserved verbatim.

[If suppressFollowUpQuestions]
Continue the conversation from where it left off without asking the user any further questions. Resume directly — do not acknowledge the summary, do not recap what was happening, do not preface with "I'll continue" or similar. Pick up the last task as if the break never happened.
```
