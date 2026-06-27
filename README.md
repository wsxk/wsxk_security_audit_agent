# wsxk_security_audit_agent

基于 opencode 定制的多 Agent 源码安全审计系统，面向基站软件源码审计场景。

当前最小链路：

- audit-orchestrator：主控调度与结果归并。
- project-profiler：识别模块入口函数。
- source-sink-tracer：从入口函数追踪 source 到 sink。
- false-positive-gatekeeper：复核候选漏洞并去除误报。
- base-station-expert：结合基站安全边界再次复核。
