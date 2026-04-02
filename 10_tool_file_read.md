# Tool: Read

Source: `src/tools/FileReadTool/prompt.ts`

## Description

```
Reads a file from the local filesystem. You can access any file directly by using this tool.
Assume this tool is able to read all files on the machine. If the User provides a path to a file assume that path is valid.
It is okay to read a file that does not exist; an error will be returned.
```

## Usage

- The `file_path` parameter must be an absolute path, not a relative path
- By default, reads up to 2000 lines from the beginning of the file
- You can optionally specify a line offset and limit (especially handy for long files)
- When you already know which part of the file you need, only read that part

## Output Format

- Results are returned using `cat -n` format, with line numbers starting at 1

## Special File Types

- **Images** (PNG, JPG, etc.): Contents are presented visually — Claude Code is a multimodal LLM
- **PDF files**: Can read PDF files. For large PDFs (more than 10 pages), you MUST provide the pages parameter. Maximum 20 pages per request.
- **Jupyter notebooks** (.ipynb): Returns all cells with their outputs, combining code, text, and visualizations

## Notes

- This tool can only read files, not directories. To read a directory, use `ls` via Bash.
- If the user provides a path to a screenshot, ALWAYS use this tool to view the file.
- If a file exists but has empty contents, you will receive a system reminder warning.

## Unchanged Stub

```
File unchanged since last read. The content from the earlier Read tool_result in this conversation is still current — refer to that instead of re-reading.
```
