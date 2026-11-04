# Memory with Mem0

General practices for giving a voice agent or character memory with [Mem0](https://docs.mem0.ai), a memory layer for LLM agents that persists context across sessions. This describes how to use Mem0. It is not a description of how any specific project is built.

## Setup

- **Managed Platform** (`pip install mem0ai` / `npm install mem0ai`, `MemoryClient`) is Mem0's recommended path. Use **Open Source** (`Memory`, `mem0ai/oss`) when memory must stay self-hosted. Some features (custom categories, webhooks, advanced filters) are Platform-only.
- Keep the API key in an environment variable. Never put it in the repo or the prompt.

## Design practices

1. **Decide what the character remembers before writing code.** Use the controls in `personality-controls` to set what is worth remembering (preferences, names, unfinished threads) and what never is (sensitive data, anything said in distress unless needed).
2. **Scope every memory.** Use `user_id` for the person, `agent_id` for the character, and `run_id` for one session or call. With an anonymous public installation, don't invent a stable `user_id`. Keep memory per session unless the person opts in.
3. **Write after the turn, read before it.** `add()` the exchange (user + assistant messages) after each turn or at the end of a call. `search()` with the current utterance and the scope filters before generating. Inject only the top few results, never the whole history.
4. **Keep latency in budget for voice.** Retrieval sits on the critical path to the first spoken word. Search in parallel with other work, cap the number of results, and fall back to no memory rather than a silent pause.
5. **Let memories expire.** Use [memory expiration](https://docs.mem0.ai/platform/features/memory-expiration) for facts with a known shelf life, and [delete](https://docs.mem0.ai/core-concepts/memory-operations/delete) / `delete_all(user_id=…)` for outdated memories or when a person asks to be forgotten.
6. **Use metadata and categories** to separate kinds of memory (e.g. `preference`, `story_thread`) and filter them at search time ([metadata filtering](https://docs.mem0.ai/open-source/features/metadata-filtering), [custom categories](https://docs.mem0.ai/platform/features/custom-categories)).
7. **Be honest about memory in conversation.** The character says what it remembers and why, and never claims to remember something it didn't retrieve (control 09, Values & limits).
8. **Test it like a personality control.** Test: tell the agent your name in one session, then return in another. Expected: it only recalls the name if cross-session memory is in scope and consented, and it accepts corrections.

## Minimal example (Platform, Python)

```python
import os
from mem0 import MemoryClient

client = MemoryClient(api_key=os.environ["MEM0_API_KEY"])

# after a turn
client.add(messages, user_id=user_id, agent_id="character", run_id=call_id)

# before the next reply
hits = client.search(utterance, filters={"user_id": user_id})
```

Sources: Mem0 docs, https://docs.mem0.ai (llms.txt index, quickstart, memory operations, memory expiration, metadata filtering), retrieved 4 Nov 2026.
