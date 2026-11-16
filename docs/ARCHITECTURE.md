# Architecture & Interface Contracts

The whole point of this design: **modules talk only through fixed contracts**, so each
build agent works in isolation without breaking others. Do not change a contract
signature without updating this file and notifying dependent agents.

## Layers
1. **Channels** (`channels/`) — thin clients. Convert a modality to/from text. No AI logic.
2. **Engine** (`core/engine.py`) — single HTTP entry point. Auth + routing only.
3. **Brain** (`core/agent_loop.py`) — the agentic loop. Orchestrates memory + tools + model.
4. **Memory** (`memory/`) — RAG + persistence.
5. **Tools** (`tools/`) — native actions + MCP bridge, unified behind one registry.

## Contracts (the load-bearing interfaces)

### Engine HTTP (channels depend on this)
```
POST /message   body: {session_id: str, text: str}   header: X-Agent-Secret
                -> 200 {reply: str}
GET  /health    -> {status: "ok"}
```

### Brain (engine depends on this)
```python
async def run_turn(session_id: str, user_text: str) -> str
```

### Memory (brain depends on this)
```python
async def retrieve(query: str, top_k: int) -> str        # text block to inject, "" if none
async def remember(user_text: str, assistant_text: str) -> None
```

### Tools (brain depends on this)
```python
def get_tool_schemas() -> list[dict]                     # Anthropic tool schemas
async def execute_tool(name: str, args: dict) -> str
```

### MCP manager (registry depends on this)
```python
mcp.tool_schemas() -> list[dict]
mcp.owns(name: str) -> bool
async mcp.call(name: str, args: dict) -> str
```

### Channel client (channels depend on this)
```python
EngineClient.send(session_id: str, text: str) -> str
```

## Golden rule
If your agent needs data from another module, call its **contract**. Never reach into
another module's internals. If a contract is insufficient, propose a change here first.

## Scheduler / proactive (capability N)
The scheduler (`scheduler/`) is NOT a new layer — it's another consumer of the brain.
Jobs talk to the engine ONLY through the same channel contract:
```python
EngineClient.send(session_id: str, text: str) -> str
```
Scheduler contract (owned by the proactive agent):
```python
register(job_callable, trigger)   # cron/interval
start()                           # begin running; failures log, never crash the loop
```
A job asks the brain to do the work (e.g. "assemble my morning briefing") and pushes the
result to a channel. The engine itself never changes.
