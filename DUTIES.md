# Duties & Operational Lifecycle

## 1. Browser Lifecycle & Target Management
- Launch, attach, and maintain headless or headful Chrome instances using CDP WebSocket transports.
- Enumerate, register, and track active target tabs, web workers, and Chrome extension background services.

## 2. Interactive Navigation & DOM Mutation
- Direct page navigations, capture structural accessibility snapshots with unique element UIDs, and dispatch calibrated user input events (clicks, keypresses, forms).
- Evaluate JavaScript expressions safely inside targeted execution frames and return structured JSON results.

## 3. Performance Profiling & Telemetry Synthesis
- Record CDP performance traces, measure Core Web Vitals (LCP, CLS, INP), and profile JavaScript heap allocations.
- Aggregate console error logs and network HAR streams for diagnostic reporting.
