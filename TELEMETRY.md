# Telemetry and Analytics

This extension collects anonymous usage data to help improve the product. All telemetry respects VS Code's telemetry settings and follows the [VS Code Telemetry Extension Guide](https://code.visualstudio.com/api/extension-guides/telemetry).

## Privacy Commitment: What We Do NOT Collect

We follow a strict **"Context, Not Content"** philosophy. This means we track _what actions_ you take, but **never** the actual data you work with:

| Category                  | What We DO NOT Collect                                          |
| ------------------------- | --------------------------------------------------------------- |
| **Your Data**             | Table contents, query results, preview data, row values         |
| **Schema Information**    | Table names, column names, dataset names, project names         |
| **Descriptions**          | Any AI-generated or user-written descriptions of tables/columns |
| **Queries**               | SQL query text, query parameters values, query errors with data |
| **AI Conversations**      | Chat messages, prompts, AI responses, tool call arguments       |
| **Knowledge**             | Any extracted or written knowledge about your data warehouse    |
| **Credentials**           | API keys, tokens, passwords, service account details            |
| **File Paths**            | File paths are never collected, not even in error messages      |
| **Identifiable Settings** | We track _which_ setting changed, never the actual value        |

## User Control

- **Respects VS Code Settings**: All telemetry follows VS Code's `telemetry.telemetryLevel` setting
- **Easy Opt-Out**: Set `telemetry.telemetryLevel` to `"off"` to disable all data collection
- **Transparency**: You can view telemetry data using VS Code CLI: `code --telemetry`

## Implementation

We use the official `@vscode/extension-telemetry` module which:

- Automatically respects the user's telemetry preferences
- Sends data to Azure Application Insights
- Provides VS Code-standard privacy guarantees

## What We Track (By Category)

We organize telemetry into 5 meta-event types. Each is designed to give us insight into how the extension is used without exposing sensitive information.

### 1. System Status Events

Tracks extension lifecycle and component health. Helps us understand startup success rates and identify infrastructure issues.

| What                 | Example Data                                                                                                        |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Extension startup    | Duration in milliseconds, success/failure status                                                                    |
| Component health     | Which component (analytics, pocketbase, auth, language_server), lifecycle event (start, ready, stop), health status |
| Service availability | Whether services started successfully                                                                               |

**Never includes:** Server URLs, ports, configuration details, error messages with data

### 2. Feature Execution Events

Tracks when features complete (success or failure). Helps us understand which features are used and their performance.

| Feature             | What We Track                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------------- |
| **Query Execution** | Duration, success/failure, character count of SQL, row count returned, parameter count used       |
| **Schema Sync**     | Duration, success/failure, count of tables synced                                                 |
| **Export**          | Format type (csv/excel/googlesheets), row count, column count                                     |
| **AI Indexing**     | Duration, success/failure                                                                         |
| **LLM Generation**  | Model name (e.g., "gemini-3-pro"), token counts, duration. **Not** the prompt or response content |
| **Tool Calls**      | Tool name (e.g., "queryTool"), duration, success/failure. **Not** the arguments or results        |
| **Connection Test** | Success/failure, which settings were configured (as booleans like `hasProjectId: true`)           |

**Never includes:** Actual SQL text, query results, table names, error details with data, AI prompts or responses, tool arguments

### 3. UI Interaction Events

Tracks clicks, toggles, and navigation. Helps us understand which UI elements are used.

| What           | Example Data                                                                                                    |
| -------------- | --------------------------------------------------------------------------------------------------------------- |
| Button clicks  | Which view (schema_explorer, data_view, settings), which element (export_btn, refresh_btn), action type (click) |
| Toggle changes | Element (ai_accessible_toggle), action (toggle_on/toggle_off)                                                   |
| Navigation     | Tab switches, expand/collapse actions                                                                           |

**Never includes:** What was clicked on (no table names, no column names), what was expanded/collapsed

### 4. Settings Change Events

Tracks when settings are modified. Helps us understand which settings users customize.

| What             | Example Data                                                                                                  |
| ---------------- | ------------------------------------------------------------------------------------------------------------- |
| Setting modified | Setting ID (warehouse_type, project_id, ai_auto_index), change type (enabled, disabled, value_updated, reset) |

**Never includes:** The actual setting value - only that it changed and how (e.g., "enabled" vs "disabled" for boolean settings)

### 5. Error Events

Tracks failures to help us identify and fix bugs. All errors go through strict sanitization.

| What            | Example Data                                                                        |
| --------------- | ----------------------------------------------------------------------------------- |
| Error category  | database, network, auth, ai, validation, internal                                   |
| Safe error code | Pre-defined codes like `BQ_PERMISSION_DENIED`, `NETWORK_TIMEOUT`, `AI_RATE_LIMITED` |
| Context         | Which feature was being used when error occurred, whether error was shown to user   |

**Never includes:** Actual error messages (which could contain table names, file paths, or other sensitive data)

#### Error Sanitization

All errors pass through a sanitization layer before being logged. The raw error message (which may contain file paths, table names, or other sensitive information) is **never** sent to our backend. Instead, we analyze the error locally and map it to a pre-defined safe error code (e.g., `BQ_PERMISSION_DENIED`, `NETWORK_TIMEOUT`, `AI_RATE_LIMITED`). Only this generic code is logged, never the actual error message or stack trace.

## Common Properties

All events automatically include these common properties:

| Property          | Description                                            |
| ----------------- | ------------------------------------------------------ |
| `warehouseType`   | Type of data warehouse (e.g., "BigQuery", "Snowflake") |
| `sessionId`       | Random UUID generated at extension startup             |
| `debug`           | Set to "true" when running in development mode         |
| `clientTimestamp` | When the event occurred                                |

## Correlation IDs

For understanding user flows, we use random UUIDs:

- **Session ID**: Generated when extension activates (resets each VS Code session)
- **Chat ID**: Random UUID per chat thread (for correlating chat events)
- **Job ID**: Random UUID per background job (for indexing operations)
- **Trace ID**: Random UUID for a single user action flow

These IDs are **opaque** - they contain no semantic information about your data or workspace.

## Summary

The extension is designed with privacy as a core principle:

1. **No content** - We never see your data, queries, or conversations
2. **No schema identifiers** - Table names, column names, project names are never logged
3. **No credentials** - API keys, tokens, and passwords are never logged
4. **No file paths** - File paths are never collected
5. **Enumerated values only** - Settings and errors use pre-defined codes, not actual values
6. **User control** - All telemetry respects VS Code's telemetry settings
7. **Opaque IDs** - Session and trace IDs are random UUIDs with no semantic meaning

If you have questions or concerns about telemetry, please [open an issue](https://github.com/mangabey-monkey/distinct/issues) on our GitHub repository.
