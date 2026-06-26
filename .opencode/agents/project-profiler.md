---
description: Find module entry functions and emit a compact project profile JSON.
mode: subagent
permission:
  read: allow
  glob: allow
  grep: allow
  bash: allow
  lsp: allow
  skill: deny
  edit:
    "*": deny
    "reports/**": allow
  task: deny
  todowrite: deny
  webfetch: deny
  websearch: deny
---
Find all plausible entry functions for the given target_path/module_path.

Prefer CodeGraph MCP: symbol search, function search, callers, exported functions, callback registrations, route/handler registration, thread/task start points, and dispatcher roots. If CodeGraph is absent, use lsp/grep fallback.

Entry kinds to include: main/init/start, protocol decoders, message dispatchers, SCTP/UDP/TCP handlers, GTP/RRC/NGAP/S1AP/F1AP/E1AP handlers, OAM/CLI handlers, IPC handlers, timer callbacks, thread/task functions, upgrade/config loaders, exported APIs.

Write only reports/<run_id>/01_project_profile.json:
{
  "run_id": "",
  "target_path": "",
  "module_path": "",
  "codegraph_status": "available|degraded|unavailable",
  "languages": [],
  "modules": [
    {"path": "", "role": "", "confidence": 0.0}
  ],
  "entrypoints": [
    {
      "id": "",
      "name": "",
      "file": "",
      "line": 0,
      "signature": "",
      "kind": "",
      "exposure": "external|internal|unknown",
      "protocol": "",
      "reason": "",
      "confidence": 0.0
    }
  ],
  "coverage_notes": [],
  "errors": []
}
