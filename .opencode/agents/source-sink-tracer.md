---
description: 从入口函数追踪到危险 sink，并输出候选漏洞 JSON。
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
从 project-profiler 输出的入口函数出发，追踪安全相关路径。

优先使用 CodeGraph MCP 分析正向调用链、被调函数、调用者和函数体。仅在 CodeGraph 不可用时使用 grep/lsp 降级。不要编造路径；每个发现都必须有具体 call_chain。

Source 范围：网络报文、协议 PDU、SCTP/UDP/TCP 输入、IPC、OAM/CLI、配置、升级包、文件导入、定时器/事件载荷等入口函数。

Sink 范围：memcpy/memmove/strcpy/sprintf、分配大小、指针运算、解析器长度使用、命令执行、文件写入/删除、鉴权决策、加密配置、动态加载、权限/状态迁移、标识符或敏感信息日志。

只写入 reports/<run_id>/02_source_sink_findings.json：
{
  "run_id": "",
  "input_profile": "reports/<run_id>/01_project_profile.json",
  "codegraph_status": "available|degraded|unavailable",
  "candidate_findings": [
    {
      "id": "",
      "title": "",
      "category": "",
      "cwe": "",
      "severity_guess": "critical|high|medium|low|info",
      "entrypoint_id": "",
      "source": {"function": "", "file": "", "line": 0, "controlled_by": ""},
      "sink": {"function": "", "file": "", "line": 0, "operation": ""},
      "call_chain": [
        {"function": "", "file": "", "line": 0, "evidence": ""}
      ],
      "missing_checks": [],
      "impact": "",
      "confidence": 0.0
    }
  ],
  "coverage_notes": [],
  "errors": []
}
