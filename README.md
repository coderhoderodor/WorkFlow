# WorkFlow

## Overview
WorkFlow is an iOS automation environment that lets power users design, execute, and share AI-enhanced workflows completely on-device. The project combines a visual editor, a resilient runtime, and deep integrations with Apple system features so automations can run securely without requiring dedicated servers.

## Vision
Deliver the first iOS-native workflow builder that is as extensible as professional automation suites while remaining safe to run on personal devices. The app targets automation enthusiasts who want to orchestrate AI tools, third-party APIs, and native iOS capabilities within a single experience.

## Core Capabilities
- **Graph-based workflow editor** built with SwiftUI supporting both canvas and list views for editing node-based flows.
- **AI building blocks** including chat, summarization, and classification nodes backed by pluggable AI providers such as OpenAI or Anthropic.
- **Integration nodes** for HTTP requests, JSON transformations, file operations, notifications, and other system interactions.
- **Custom API connectors** that store user-provided credentials securely in the Keychain and expose them as reusable nodes.
- **Robust execution engine** with logging, retry logic, scheduling, Shortcuts integration, and checkpointing to resume long-running jobs.

## Architecture Snapshot
1. **SwiftUI client** provides the workflow editor, execution dashboards, and onboarding.
2. **Execution engine** runs flows locally on-device and can optionally delegate heavy work to a minimal cloud relay when iOS background limits require it.
3. **Node library** bundles system, integration, and AI actions with an extensible registry so new capabilities can be added without app updates.
4. **Storage layer** persists workflows as JSON bundles, while secrets are isolated in the Keychain and never embedded directly in workflow definitions.
5. **App Intents bridge** exposes workflows to Shortcuts and Siri for quick triggering and inter-app automation.

## Roadmap
1. **MVP (Milestone 1)** – deliver editing basics, local execution with logging, built-in AI chat node, HTTP integration, and secure secrets handling.
2. **Milestone 2** – add scheduling, retries, checkpointing, and initial integrations (Notion, Slack, Gmail, Airtable).
3. **Milestone 3** – release optional cloud relay, multi-agent orchestration, and expanded AI node catalog.

## Documentation
Detailed requirements and design notes are available in [`docs/product_requirements.md`](docs/product_requirements.md).
