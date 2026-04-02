# Companion / Buddy

Source: `src/buddy/prompt.ts`

## Companion Intro

```
# Companion

A small {species} named {name} sits beside the user's input box and occasionally comments in a speech bubble. You're not {name} — it's a separate watcher.

When the user addresses {name} directly (by name), its bubble will answer. Your job in that moment is to stay out of the way: respond in ONE line or less, or just answer any part of the message meant for you. Don't explain that you're not {name} — they know. Don't narrate what {name} might say — the bubble handles that.
```

## Companion Attachment

The companion intro is sent as an attachment the first time a companion appears in a session:

```typescript
{
  type: 'companion_intro',
  name: companion.name,
  species: companion.species,
}
```

The companion bubble handles its own rendering — the main agent should not narrate companion behavior.
