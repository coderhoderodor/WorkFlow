# WorkFlow Product Requirements

## 1. Problem Statement
Existing automation tools either require a server (n8n, Zapier, IFTTT) or offer limited extensibility on iOS (Shortcuts). Power users need an iOS-native environment that combines visual workflow design, AI capabilities, and extensibility without sacrificing security or reliability.

## 2. Goals & Success Metrics
- **Goal:** Deliver a working MVP that proves technical feasibility of complex AI-enabled automations running on iOS 17+ devices.
- **Success Metric:** Ship an MVP where users can build, execute, and share workflows that combine AI nodes and third-party integrations entirely from an iPhone.

## 3. Target Users
- Automation enthusiasts and productivity power users.
- Workflow designers who want to mix Apple platform features with custom APIs.

## 4. User Journey
1. **Guided onboarding** introduces core concepts and imports a sample workflow.
2. **Build first flow** using templates, AI nodes, and integrations.
3. **Expand automations** with custom API connectors, scheduling, and Shortcuts triggers.

## 5. Scope Overview
- Node-based workflow editor with support for AI, integration, and system actions.
- Execution engine capable of running locally, with optional cloud relay for background-safe execution.
- Support for multi-agent and AI-centric workflows.

## 6. Functional Requirements
### 6.1 Workflow Editing
- Provide both canvas and list representations of workflows.
- Support drag-and-drop node placement, connection management, and in-place configuration.
- Offer reusable templates and inline documentation for each node.

### 6.2 AI Nodes
- Built-in nodes for chat interactions, summarization, and classification.
- Allow selection of AI providers (OpenAI, Anthropic, local models) with configurable parameters.
- Support conversation memory, temperature controls, and output schema definition.

### 6.3 Integration Nodes
- HTTP client node supporting REST, GraphQL, and webhook endpoints.
- JSON manipulation node for mapping, filtering, and merging payloads.
- File I/O node for reading/writing to app sandbox and iCloud Drive when available.
- Notification node for user alerts (push, local notifications).

### 6.4 Custom API Connectors
- Enable users to define authenticated connectors with API keys or OAuth tokens.
- Store secrets exclusively in Keychain; reference them via secure handles within workflows.
- Provide per-connector rate limiting and error handling configuration.

### 6.5 Execution & Monitoring
- Local execution engine with structured logs, per-node metrics, and replayable traces.
- Automatic retries with exponential backoff and conditional retry rules.
- Checkpointing to allow resumable runs and mid-execution edits.
- Scheduler for time-based and event-based triggers.
- App Intents integration to invoke workflows from Shortcuts, Siri, and widgets.

## 7. Non-Functional Requirements
- Reliable operation on iOS 17+ devices with constrained resources.
- Secrets must be stored in Keychain and never exported in plain text.
- Background execution must respect iOS limits, using ActivityKit, BackgroundTasks, or optional cloud relay.
- Ensure data durability via on-device persistence and iCloud sync for user-authored workflows.
- Provide export/import as signed JSON bundles for sharing.

## 8. Architecture Overview
1. **SwiftUI interface** renders the workflow editor, execution console, and settings.
2. **Flow runtime** built with Combine/Swift Concurrency to orchestrate node execution, manage dependencies, and handle retries.
3. **Node registry** uses protocol-based adapters so new node types can be added dynamically.
4. **Storage layer** persists workflow definitions in Core Data or SQLite, with secrets isolated to Keychain.
5. **Bridge layer** exposes workflows via App Intents and handles inbound/outbound Shortcuts communication.
6. **Optional cloud relay** queues jobs when background execution is impossible; communicates over encrypted channels using user-owned servers.

## 9. Integrations Roadmap
- Phase 1: OpenAI, Anthropic, generic HTTP/JSON, local files, Notifications.
- Phase 2: Gmail, Slack, Notion, Airtable, Google Drive.
- Phase 3: Additional SaaS (Asana, Linear), multi-agent orchestration, custom SDKs.

## 10. Security & Privacy
- Keychain-backed secret storage with biometric-unlock option.
- Signed workflow bundles to prevent tampering when importing/exporting.
- On-device audit logs to trace API usage; user-controllable data retention policies.
- Explicit scopes for each connector to prevent cross-workflow leakage.

## 11. Open Questions
- What sandboxing strategy ensures third-party nodes can run without compromising app stability?
- How much computation can reliably stay on-device versus requiring the optional relay?
- Which pricing model (one-time, subscription, marketplace) best aligns with power user expectations?

## 12. Next Steps
- Validate technical feasibility of on-device execution with a prototype engine.
- Conduct user interviews with Shortcuts power users to refine editing experience.
- Define analytics and telemetry strategy compliant with privacy expectations.
