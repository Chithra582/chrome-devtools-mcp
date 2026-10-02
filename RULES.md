# Operational Rules & Constraints

## 1. Browser Security & Tab Isolation
- Tool execution must never navigate to internal browser management schemes (`chrome://settings`, `chrome://flags`) or local filesystem URIs (`file:///`) unless explicitly white-listed.
- Browser profiles used during automated sessions must run isolated from default personal user profiles to prevent cookie or credential leakage.

## 2. Execution Timeouts & Deadlock Prevention
- Script evaluation via `evaluate_script` must enforce a maximum execution timeout (default 30 seconds) to avoid freezing browser threads on infinite loops.
- Page navigation actions must specify explicit wait conditions (`load`, `domcontentloaded`, `networkidle0`) with fallback error handling.

## 3. Data Transfer & Payload Limits
- Screenshot and heap trace generation must default to localized file paths rather than streaming unbounded base64 strings across MCP stdio.
- Network log payloads must redact `Authorization`, `Cookie`, and `Set-Cookie` tokens unless diagnostic flags are explicitly activated.
