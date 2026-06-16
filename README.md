# uri2run


## AI Cost Tracking

![PyPI](https://img.shields.io/badge/pypi-costs-blue) ![Version](https://img.shields.io/badge/version-0.1.31-blue) ![Python](https://img.shields.io/badge/python-3.9+-blue) ![License](https://img.shields.io/badge/license-Apache--2.0-green)
![AI Cost](https://img.shields.io/badge/AI%20Cost-$0.18-orange) ![Human Time](https://img.shields.io/badge/Human%20Time-1.5h-blue) ![Model](https://img.shields.io/badge/Model-openrouter%2Fqwen%2Fqwen3--coder--next-lightgrey)

- 🤖 **LLM usage:** $0.1754 (3 commits)
- 👤 **Human dev:** ~$150 (1.5h @ $100/h, 30min dedup)

Generated on 2026-06-15 using [openrouter/qwen/qwen3-coder-next](https://openrouter.ai/qwen/qwen3-coder-next)

---

Neutral transport runtime for capability backends.

```txt
python     — python://module:function handlers
shell      — shell commands with timeout; argv mode can avoid shell=True
http       — HTTP/HTTPS requests with headers/body/retry support (httpx)
stdio      — subprocess JSON stdin/stdout protocol
sse        — Server-Sent Events stream reader
ws         — WebSocket client (requires pip install uri2run[stream])
docker     — docker:// compose/container control via uri3 controller
ssh        — ssh:// remote resolve + command execution
mcp        — mcp:// HTTP bridge to MCP tools endpoints
a2a        — a2a:// HTTP bridge to agent-card and task endpoints
uri_flow   — expand + validate + dry-run/run compact flow
uri_graph  — validate + dry-run/run workflow graph
```

`touri` delegates `python`, `shell`, `http`, `stdio`, `sse`, `ws`, `docker`,
`ssh`, `mcp`, `a2a`, `uri_flow`, and `uri_graph` backends here.

## CLI

```bash
uri2run call python://touri_examples.weather:handler --payload '{"place":"Gdansk","days":14}'
uri2run call 'echo ok' --type shell
uri2run call http://localhost:8101/health
```

## Python API

```python
from uri2run import run_backend

result = run_backend(
    {"type": "python", "target": "python://touri_examples.weather:handler"},
    {"place": "Gdansk", "days": 14},
    {"root": "."},
)
```

Every result includes `meta.transport`, `meta.duration_ms`, and `meta.runtime = uri2run`.
Backends with an explicit target also include `meta.target`.

See [`docs/URI2RUN_ARCHITECTURE.md`](../../docs/URI2RUN_ARCHITECTURE.md).
