# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **# Explainability & Decision Transparency Report** (`chrome-devtools-mcp`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** # Explainability & Decision Transparency Report (`chrome-devtools-mcp`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Browser Automation, Web Debugging & Chrome DevTools Protocol  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

### 1. Deterministic Multi-Stage Decision Pipeline
The agent inspects, controls, and diagnoses browser pages through a deterministic, 5-stage execution pipeline.

### 1. Decision Architecture

The runtime intake, state classification, evaluation, and execution tracking operate across a deterministic, five-stage pipeline:

```
+-----------------------------------------------------------------------------------+
|                        Deterministic Browser DevTools Pipeline                    |
+-----------------------------------------------------------------------------------+
|  [Stage 1: Tool Request Ingestion & Page Context Resolution]                      |
|     --> Validate incoming MCP tool invocation & resolve active target pageId/tab   |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 2: Security Validation & Navigation Bounds Gate]                          |
|     --> Screen target URL against forbidden browser schemes & local file exploits |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 3: CDP Command Serialization & Execution]                                 |
|     --> Dispatch CDP WebSocket frames (Page, Runtime, DOM, Network, HeapProfiler) |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 4: State Synchronization & DOM Diff Verification]                         |
|     --> Capture post-action accessibility snapshot & verify DOM transition state  |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 5: Telemetry Structuring & MCP Response Delivery]                         |
|     --> Format structured JSON response or save heavy artifacts to local filePath |
+-----------------------------------------------------------------------------------+
```

### 2. Decision Logic & Routing Formulations



### 3. Thresholding & Refusal Decision Criteria

# Explainability & Decision Transparency Report enforces strict operational boundaries and deterministic refusal thresholds:
- **Refusal on Policy Violation**: Requests violating boundary constraints halt with code `ERR_POLICY_VIOLATION`.
- **Refusal on Timeout**: Executions exceeding budget limits terminate with code `ERR_EXECUTION_TIMEOUT`.

### 4. Fallback Decision Mechanism

Continuous operational stability is maintained through layered fault recovery:
- **Model Fallback Cascade**: High-level reasoning and synthesis default to `gemini-2.0-flash` with automatic failover to `gpt-4o` and `claude-3-5-sonnet`.

### 5. Human-in-the-Loop Governance

Human operators retain sovereign authority over the multi-agent execution lifecycle:
- **Operational Review**: Sensitive actions require operator sign-off.
- **Audit Logging**: All decisions are recorded for auditability.

---

## The Data It Uses

# Explainability & Decision Transparency Report operates under strict principles of data minimization, environment isolation, and privacy protection.

### 1. Ingested Input Data

The framework processes only operational data necessary to perform its functions:
- **Input Directives**: Operational tasks and data payloads.

### 2. Configuration & Reference Data

- **Configuration Schemas**: Declarative system configuration files.

### 3. Base Model & Inference Lineage

- **Protocol Foundations**: Chrome DevTools Protocol (CDP), Model Context Protocol (MCP) TypeScript SDK.
- **Browser Engines**: Chromium / Google Chrome running under Puppeteer automation.

### 4. Data Privacy, Storage, and Retention

- **OWASP LLM & MITRE ATLAS Hardened**: Defended against indirect prompt injection, credential leakage, and unauthorized external API dispatch.
- **Local Environment Isolation**: Agent execution workspaces, intermediate scratchpads, and vector stores reside strictly within designated local project directories.
- **Automated Secret Scrubbing**: API keys, database credentials, and personal credentials are automatically redacted prior to embedding or logging.
- **Zero Commercial Monetization**: Prompts, intermediate reasoning trajectories, and task deliverables are never commercialized or shared with third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of # Explainability & Decision Transparency Report is essential for effective deployment.

### 1. Deterministic Multi-Stage Decision Pipeline
The agent inspects, controls, and diagnoses browser pages through a deterministic, 5-stage execution pipeline.

```
+-----------------------------------------------------------------------------------+
|                        Deterministic Browser DevTools Pipeline                    |
+-----------------------------------------------------------------------------------+
|  [Stage 1: Tool Request Ingestion & Page Context Resolution]                      |
|     --> Validate incoming MCP tool invocation & resolve active target pageId/tab   |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 2: Security Validation & Navigation Bounds Gate]                          |
|     --> Screen target URL against forbidden browser schemes & local file exploits |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 3: CDP Command Serialization & Execution]                                 |
|     --> Dispatch CDP WebSocket frames (Page, Runtime, DOM, Network, HeapProfiler) |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 4: State Synchronization & DOM Diff Verification]                         |
|     --> Capture post-action accessibility snapshot & verify DOM transition state  |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 5: Telemetry Structuring & MCP Response Delivery]                         |
|     --> Format structured JSON response or save heavy artifacts to local filePath |
+-----------------------------------------------------------------------------------+
```

### 2. Mathematical Decision & Affinity Scoring
Target element localization and interaction scoring across parsed accessibility nodes rely on a structured affinity formulation:

$$S_{\text{node}}(n) = w_1 \cdot \text{TextMatch}(\text{query}, \text{label}(n)) + w_2 \cdot \text{RoleWeight}(n) + w_3 \cdot \text{Visibility}(n) - w_4 \cdot \text{Depth}(n)$$

Where:
- $w_1 = 0.45$: Semantic matching score between target description and node label/ARIA text.
- $w_2 = 0.25$: Interactive role importance (e.g. `button`, `link`, `input` vs `generic`).
- $w_3 = 0.20$: Viewport visibility coefficient (1.0 if inside viewport, 0.0 if occluded).
- $w_4 = 0.10$: Normalized DOM tree nesting depth penalty.

Core Web Vitals diagnostic prioritization across performance metrics is calculated as:

$$S_{\text{perf}}(m) = \frac{\text{Observed}(m) - \text{GoodThreshold}(m)}{\text{PoorThreshold}(m) - \text{GoodThreshold}(m)}$$

Where metrics with $S_{\text{perf}}(m) > 1.0$ receive immediate remediation priority.

### 3. Thresholding & Refusal Decision Criteria
Commands violating browser security boundaries or resource thresholds are rejected with explicit error codes:

| Threshold Parameter | Value | Decision / Refusal Action | Error Code |
| :--- | :--- | :--- | :--- |
| **Restricted Browser Scheme** | `chrome://*`, `chrome-extension://*` | Refuse navigation to prevent browser privilege escalation | `ERR_DISALLOWED_NAVIGATION_SCHEME` |
| **Local Filesystem Access** | `file://*` without flag | Block file read attempt | `ERR_LOCAL_FILE_ACCESS_DENIED` |
| **Script Execution Timeout** | $> 30,000$ ms | Terminate evaluation to avoid hanging V8 thread | `ERR_SCRIPT_EVALUATION_TIMEOUT` |
| **Target Page Not Found** | Invalid `pageId` | Halt tool execution and request `list_pages` | `ERR_TARGET_PAGE_NOT_FOUND` |
| **Element UID Obsolete** | Node removed from DOM | Abort click/input and request fresh `take_snapshot` | `ERR_STALE_ELEMENT_REFERENCE` |

### 4. Multi-Tier Fallback Mechanisms & Human-in-the-Loop Governance
1. **Tier 1 (Automated Snapshot Refresh)**: If an interaction fails due to a stale element UID, the agent automatically retries with a freshly captured snapshot.
2. **Tier 2 (Browser Process Restart)**: If the Chrome instance crashes or the CDP WebSocket drops unexpectedly, the daemon relaunches a clean browser process within 1.5 seconds.
3. **Tier 3 (User Inspection Escalation)**: On complex bot detection challenges (Cloudflare Turnstile, reCAPTCHA), the agent displays an on-screen prompt delegating manual verification to the human user.

---

## The Data It Uses

### 1. Ingestion Data & Input Types
- **DOM & Accessibility Trees**: Structural text snapshots with assigned element `uid`s and attributes.
- **Visual Capture**: Full-page and viewport screenshots saved in PNG/JPEG format.
- **Network Telemetry**: HTTP request/response headers, status codes, payload sizes, and timing metrics.

### 2. Reference Standards & Diagnostic Rules
- **Web Standards**: W3C DOM, HTML5, CSSOM, ARIA accessibility specification.
- **Core Web Vitals**: Largest Contentful Paint (LCP), Cumulative Layout Shift (CLS), Interaction to Next Paint (INP).

### 3. Model Lineage & System Architecture
- **Protocol Foundations**: Chrome DevTools Protocol (CDP), Model Context Protocol (MCP) TypeScript SDK.
- **Browser Engines**: Chromium / Google Chrome running under Puppeteer automation.

### 4. Data Privacy, Governance & Retention
- **Ephemeral Sandbox Storage**: Debug traces and temporary screenshots are cleared upon MCP session disconnect.
- **Credential Masking**: Password fields and authorization tokens are masked in text snapshots and console logs.
- **Local Isolation**: All CDP socket communications bind strictly to `localhost` (127.0.0.1) with no remote telemetry leaks.

---

## Limitations

### 1. Heavy Memory Consumption During Continuous Profiling
- **Limitation**: Prolonged performance traces and consecutive heap snapshots consume several gigabytes of RAM.
- **Mitigation**: Stream trace files directly to disk via `filePath` arguments and enforce periodic browser restarts.

### 2. Canvas & WebGL Render Obfuscation
- **Limitation**: Text and buttons drawn directly inside `<canvas>` or WebGL shaders lack DOM accessibility nodes.
- **Mitigation**: Utilize visual viewport screenshots paired with coordinate-based OCR when canvas interactions are detected.

### 3. Cross-Origin Iframe Script Sandboxing
- **Limitation**: Cross-origin iframes with strict CSP headers cannot be evaluated directly from top-level page contexts.
- **Mitigation**: Resolve and target individual child execution context IDs through CDP `Runtime.enable`.

### 4. Dynamic Shadow DOM Encapsulation
- **Limitation**: Closed shadow roots hide internal elements from standard `querySelector` queries.
- **Mitigation**: Leverage Chrome DevTools' deep DOM traversal APIs (`DOM.flattenedTree`) to uncover all shadow DOM boundaries.

### 5. Bot Detection and Anti-Scraping Defenses
- **Limitation**: High-security commercial websites may identify automated Puppeteer signatures and deploy CAPTCHAs.
- **Mitigation**: Support headful browser execution and seamlessly hand off CAPTCHA resolution to human operators.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Decision logic & routing formulations | Section 2 | Verified |
| - Thresholding & refusal decision criteria | Section 3 | Verified |
| - Fallback decision mechanism | Section 4 | Verified |
| - Human-in-the-loop governance & oversight | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested input data & query streams | Section 1 | Verified |
| - Configuration & reference schemas | Section 2 | Verified |
| - Base model lineage & deterministic engines | Section 3 | Verified |
| - Data privacy, retention lifecycle & MITRE/OWASP | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - Deterministic Multi-Stage Decision Pipeline
The agent inspects, controls, and diagnoses browser pages through a deterministic, 5-stage execution pipeline.

```
+-----------------------------------------------------------------------------------+
|                        Deterministic Browser DevTools Pipeline                    |
+-----------------------------------------------------------------------------------+
|  [Stage 1: Tool Request Ingestion & Page Context Resolution]                      |
|     --> Validate incoming MCP tool invocation & resolve active target pageId/tab   |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 2: Security Validation & Navigation Bounds Gate]                          |
|     --> Screen target URL against forbidden browser schemes & local file exploits |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 3: CDP Command Serialization & Execution]                                 |
|     --> Dispatch CDP WebSocket frames (Page, Runtime, DOM, Network, HeapProfiler) |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 4: State Synchronization & DOM Diff Verification]                         |
|     --> Capture post-action accessibility snapshot & verify DOM transition state  |
+-----------------------------------------+-----------------------------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|  [Stage 5: Telemetry Structuring & MCP Response Delivery]                         |
|     --> Format structured JSON response or save heavy artifacts to local filePath |
+-----------------------------------------------------------------------------------+
```

### 2. Mathematical Decision & Affinity Scoring
Target element localization and interaction scoring across parsed accessibility nodes rely on a structured affinity formulation:

$$S_{\text{node}}(n) = w_1 \cdot \text{TextMatch}(\text{query}, \text{label}(n)) + w_2 \cdot \text{RoleWeight}(n) + w_3 \cdot \text{Visibility}(n) - w_4 \cdot \text{Depth}(n)$$

Where:
- $w_1 = 0.45$: Semantic matching score between target description and node label/ARIA text.
- $w_2 = 0.25$: Interactive role importance (e.g. `button`, `link`, `input` vs `generic`).
- $w_3 = 0.20$: Viewport visibility coefficient (1.0 if inside viewport, 0.0 if occluded).
- $w_4 = 0.10$: Normalized DOM tree nesting depth penalty.

Core Web Vitals diagnostic prioritization across performance metrics is calculated as:

$$S_{\text{perf}}(m) = \frac{\text{Observed}(m) - \text{GoodThreshold}(m)}{\text{PoorThreshold}(m) - \text{GoodThreshold}(m)}$$

Where metrics with $S_{\text{perf}}(m) > 1.0$ receive immediate remediation priority.

### 3. Thresholding & Refusal Decision Criteria
Commands violating browser security boundaries or resource thresholds are rejected with explicit error codes:

| Threshold Parameter | Value | Decision / Refusal Action | Error Code |
| :--- | :--- | :--- | :--- |
| **Restricted Browser Scheme** | `chrome://*`, `chrome-extension://*` | Refuse navigation to prevent browser privilege escalation | `ERR_DISALLOWED_NAVIGATION_SCHEME` |
| **Local Filesystem Access** | `file://*` without flag | Block file read attempt | `ERR_LOCAL_FILE_ACCESS_DENIED` |
| **Script Execution Timeout** | $> 30,000$ ms | Terminate evaluation to avoid hanging V8 thread | `ERR_SCRIPT_EVALUATION_TIMEOUT` |
| **Target Page Not Found** | Invalid `pageId` | Halt tool execution and request `list_pages` | `ERR_TARGET_PAGE_NOT_FOUND` |
| **Element UID Obsolete** | Node removed from DOM | Abort click/input and request fresh `take_snapshot` | `ERR_STALE_ELEMENT_REFERENCE` |

### 4. Multi-Tier Fallback Mechanisms & Human-in-the-Loop Governance
1. **Tier 1 (Automated Snapshot Refresh)**: If an interaction fails due to a stale element UID, the agent automatically retries with a freshly captured snapshot.
2. **Tier 2 (Browser Process Restart)**: If the Chrome instance crashes or the CDP WebSocket drops unexpectedly, the daemon relaunches a clean browser process within 1.5 seconds.
3. **Tier 3 (User Inspection Escalation)**: On complex bot detection challenges (Cloudflare Turnstile, reCAPTCHA), the agent displays an on-screen prompt delegating manual verification to the human user.

---

## The Data It Uses

### 1. Ingestion Data & Input Types
- **DOM & Accessibility Trees**: Structural text snapshots with assigned element `uid`s and attributes.
- **Visual Capture**: Full-page and viewport screenshots saved in PNG/JPEG format.
- **Network Telemetry**: HTTP request/response headers, status codes, payload sizes, and timing metrics.

### 2. Reference Standards & Diagnostic Rules
- **Web Standards**: W3C DOM, HTML5, CSSOM, ARIA accessibility specification.
- **Core Web Vitals**: Largest Contentful Paint (LCP), Cumulative Layout Shift (CLS), Interaction to Next Paint (INP).

### 3. Model Lineage & System Architecture
- **Protocol Foundations**: Chrome DevTools Protocol (CDP), Model Context Protocol (MCP) TypeScript SDK.
- **Browser Engines**: Chromium / Google Chrome running under Puppeteer automation.

### 4. Data Privacy, Governance & Retention
- **Ephemeral Sandbox Storage**: Debug traces and temporary screenshots are cleared upon MCP session disconnect.
- **Credential Masking**: Password fields and authorization tokens are masked in text snapshots and console logs.
- **Local Isolation**: All CDP socket communications bind strictly to `localhost` (127.0.0.1) with no remote telemetry leaks.

---

## Limitations

### 1. Heavy Memory Consumption During Continuous Profiling | Section 1 | Verified |
| - Canvas & WebGL Render Obfuscation | Section 2 | Verified |
| - Cross-Origin Iframe Script Sandboxing | Section 3 | Verified |
| - Dynamic Shadow DOM Encapsulation | Section 4 | Verified |
| - Bot Detection and Anti-Scraping Defenses | Section 5 | Verified |
