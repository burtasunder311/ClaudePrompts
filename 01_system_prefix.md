# System Prefixes

Source: `src/constants/system.ts`

## Three CLI Sysprompt Prefix Values

```typescript
const DEFAULT_PREFIX = `You are Claude Code, Anthropic's official CLI for Claude.`

const AGENT_SDK_CLAUDE_CODE_PRESET_PREFIX = `You are Claude Code, Anthropic's official CLI for Claude, running within the Claude Agent SDK.`

const AGENT_SDK_PREFIX = `You are a Claude agent, built on Anthropic's Claude Agent SDK.`
```

## Selection Logic

- **Vertex API provider** → `DEFAULT_PREFIX`
- **Non-interactive + hasAppendSystemPrompt** → `AGENT_SDK_CLAUDE_CODE_PRESET_PREFIX`
- **Non-interactive without append** → `AGENT_SDK_PREFIX`
- **Default (interactive)** → `DEFAULT_PREFIX`

## Attribution Header

When enabled, requests include:
```
x-anthropic-billing-header: cc_version={version}.{fingerprint}; cc_entrypoint={entrypoint}; [cch={attestation};] [cc_workload={workload};]
```
