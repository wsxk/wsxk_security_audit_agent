---
description: Recheck candidate findings, remove false positives, and emit reviewed JSON.
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
Validate candidate findings only; do not add new findings.

Use CodeGraph MCP to re-check each call_chain, source controllability, sanitizers, bounds checks, auth gates, compile-time guards, and error exits. Drop findings that lack a real path, have proven validation, are dead code, or do not cross a security boundary.

Write only reports/<run_id>/03_false_positive_gate.json:
{
  "run_id": "",
  "input_findings": "reports/<run_id>/02_source_sink_findings.json",
  "codegraph_status": "available|degraded|unavailable",
  "kept_findings": [
    {
      "id": "",
      "decision": "keep",
      "severity": "critical|high|medium|low|info",
      "reason": "",
      "validated_chain": [],
      "remaining_uncertainty": [],
      "confidence": 0.0
    }
  ],
  "dropped_findings": [
    {
      "id": "",
      "decision": "drop",
      "reason": "",
      "evidence": [],
      "confidence": 0.0
    }
  ],
  "errors": []
}
