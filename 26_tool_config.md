# Tool: Config

Source: `src/tools/ConfigTool/prompt.ts`

## Description

```
Get or set Claude Code configuration settings.
```

## Usage

- **Get current value**: Omit the "value" parameter
- **Set new value**: Include the "value" parameter

## Global Settings (stored in ~/.claude.json)

| Setting | Type | Description |
|---------|------|-------------|
| `theme` | string | UI theme |
| `editorMode` | string | Editor mode (e.g., vim) |
| `verbose` | boolean | Verbose output |

## Project Settings (stored in settings.json)

| Setting | Type | Description |
|---------|------|-------------|
| `model` | string | Override the default model |
| `permissions.defaultMode` | string | Permission mode (e.g., plan) |

## Examples

```json
{ "setting": "theme" }                    // Get theme
{ "setting": "theme", "value": "dark" }   // Set dark theme
{ "setting": "editorMode", "value": "vim" }
{ "setting": "verbose", "value": true }
{ "setting": "model", "value": "opus" }
{ "setting": "permissions.defaultMode", "value": "plan" }
```
