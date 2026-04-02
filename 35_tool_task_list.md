# Tool: TaskList

Source: `src/tools/TaskListTool/prompt.ts`

## Description

List all tasks in the task list.

## Tool: TaskGet

Source: `src/tools/TaskGetTool/prompt.ts`

## Description

Retrieve a task by its ID from the task list. Use this to read a task's latest state before updating it.

---

## Tool: TaskStop

Source: `src/tools/TaskStopTool/prompt.ts`

## Description

Stop a running background task. Takes a `task_id` parameter.

## Usage

Used to stop a worker you sent in the wrong direction — for example, when you realize mid-flight that the approach is wrong, or the user changes requirements after you launched the worker.

Stopped workers can be continued with SendMessageTool.
