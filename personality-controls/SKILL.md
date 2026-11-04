---
name: personality-controls
description: Design the personality of a conversational or voice AI agent with ten controls (identity, purpose, story, audience and relationship, goals, character, tone, voice, values and limits, conversation habits), test each one in conversation, and compile the result into a personality prompt. Use whenever someone is writing a system prompt, persona, character or brand voice for a chatbot, assistant or voice agent.
metadata:
  version: 0.1.0
---

# Personality Controls

Ten decisions that define how an agent presents itself, converses and acts. The controls are a metaphor: not scores, not universal technical parameters.

## How to use

1. Fill in each control with the sentence in [references/controles-es.md](references/controles-es.md) (canonical Spanish text, verbatim) or the English translation [references/controls-en.md](references/controls-en.md).
2. Run its test prompt in a real conversation and compare with the expected result.
3. Tick it only when the definition is observable in the conversation.
4. Check coherence (below), then compile all ten into the personality prompt.

## The ten controls

| # | Control | Question |
|---|---|---|
| 01 | Identity | Who it is |
| 02 | Purpose | Why it does what it does |
| 03 | Story | Where its approach comes from |
| 04 | Audience & relationship | Who it accompanies |
| 05 | Goals | What outcome it pursues |
| 06 | Character | How it usually acts |
| 07 | Tone | How it adapts to the moment |
| 08 | Voice | How it speaks and how it sounds |
| 09 | Values & limits | What it prioritises |
| 10 | Conversation habits | How it listens and moves forward |

## Coherence check

Tone and voice must fit the audience; goals must respect the limits; the story must support the purpose. A personality works when these decisions hold each other up.

## Hard rules

- The agent always identifies as an AI and never invents a human job, experience or biography.
- Never present a pending action as completed.
- An honest "no, this isn't for you" and a respected goodbye are valid outcomes.
