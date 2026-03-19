# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.6.10] - 2026-03-19

### Added

- **Indexation:** Internal indexation migration plan documentation.

### Changed

- **Telemetry:** Telemetry configuration and analytics initialization improvements.
- **Icons:** MCP and app icon updates.
- **Agent logging:** Clearer agent logging (#313).
- **Knowledge:** Clearer guidance for write-knowledge behavior (#312).
- **Query sampling:** Size limits use a bytes-based approach instead of `TABLESAMPLE` (#315).

### Fixed

- **Indexation:** Indexation fixes (#314).
- Miscellaneous small fixes (#316).

## [0.6.9] - 2026-03-16

### Added

- **Table data preview:** Sampling toggle and SQL filter input with column completion for table data preview.

### Changed

- **Table data preview:** View handler and message types updated for filter/sampling; NativeDataGrid and TableDataPreview app wiring.

## [0.6.8] - 2026-03-16

### Changed

- Version bump.

## [0.6.6] - 2026-03-16

### Fixed

- **App icons:** Corrected app icon display.
- **AI chat run_query tool:** Query results now render properly in AI chat tool messages (#303).

## [0.6.5] - 2026-03-16

### Added

- **Tauri desktop app:** Native desktop app support with OAuth and deep linking (#299).
- **Web app:** New web application with basic agent, MCP implementation, and accessibility (#274, #275, #276, #277, #278, #279, #280, #281).
- **Extension knowledge manager:** Knowledge manager UI in the extension (#298).
- **Permissions management:** Improved table access and permissions view (#300).
- **Parameters in queries:** Support for parameters in SQL queries (#282).
- **Dataset sync toggle:** Ability to toggle which datasets to sync (#288).
- **Knowledge view in table info:** Basic knowledge view in table info panel (#287).
- **Streaming reasoning:** Streaming reasoning in agent responses (#295).
- **Clarifying questions:** Agent can ask clarifying questions (#283).
- **Firebase and backend:** Firebase integration and backend updates (#290).
- **Present date:** Present date handling (#289).

### Changed

- **Redesign:** UI redesign (#296).
- **Design fixes:** Color and layout improvements (#297).
- **Query handling:** Refactored to use SafeQueryService (#292, #294).
- **Indexation:** Migrated to new agent system (#286).
- **Prompts:** Updated prompts and questions (#285).
- **MCP:** Refactored MCP API responses and error handling.
- **Project structure:** Renamed "knowledge-api" to "backend".

### Fixed

- **Indexation agent:** Fixed user messages in indexation agent.
- **Agent:** Fixed error handling (#284).
- **MCP:** Various MCP fixes.
- **Tool descriptions:** Fixed tool description (#291).
- **Review:** Improved review flow (#293).

## [0.6.4] - 2026-03-07

### Fixed

- **GrepTableNamesTool:** When no tables match a given pattern, return empty result instead of throwing so the agent can handle gracefully.
- **AI chat tool call UI:** Disable copy button on file tool call message boxes (delete/edit/write) to avoid redundant copy actions.

## [0.6.3] - 2026-03-07

### Fixed

- **PocketBase server:** Correct port conflict detection when multiple editor instances run; binds to 127.0.0.1 (same as PocketBase) to avoid IPv4 vs IPv6 false "free" reports; verifies server dataDir after spawn and retries with a different port if another instance's server is bound.

## [0.6.2] - 2026-03-07

### Changed

- **Schema Explorer progress:** Refactored indexation progress display and `useProgressData` hook; PocketBase subscription with data-change handling, hide/dismiss and completion-time tracking; simplified SchemaExplorerCore progress wiring.
- **Table indexation agents:** Agent core now normalizes model messages and preserves Gemini thought signature across tool-call rounds; overview and general-analysis agents aligned with updated core.
- **LanceDB:** Sync utilities and service cleanup.

## [0.6.1] - 2026-03-07

### Fixed

- **Learn agent prompts:** Expanded learn system prompt and fixed learn first-user message and write_knowledge tool description. Resolved race condition and parsing in base agent (#269).

## [0.6.0] - 2026-03-07

### Added

- **Semantic search with LanceDB:** Embedding-based search for chat messages, workspace files (.py, .sql), knowledge, and stored queries. LanceDB tables and sync with PocketBase; workspace file indexing runs automatically at extension start when AI connection is available.
- **Learn agent and task subagents:** Dedicated “learn” agent toolset (read-only plus writeKnowledge) and a task tool that launches explore/validate subagents with persisted state for multi-step analysis and query validation.
- **Chat insights and reference tools:** `getChatInsights` tool to extract insights from a chat; `grepReferences` and enhanced reference search for code/table references; improved chat and knowledge search parameters.
- **Knowledge Manager UI:** Dedicated Knowledge Manager subpage on the home screen with list, filters, entity picker, and create/edit/delete for knowledge items; edit-knowledge design fixes and general context input improvements.
- **AI query security checks:** RunQueryTool and Python Language Server enforce AI accessibility and TABLESAMPLE rules before executing queries; validation subagent supports structured checks and assumptions parsing.
- **Run-query abort:** Ability to cancel a running query from the RunQueryTool.
- **Agent lib and tool refactor:** Shared agent/tool logic in `src/lib` (tools, agents, prompts); tool renames (e.g. query → run_query), consolidated tool set and message formatters; GrepTableNames and related tools integrated into chat.
- **Project settings in FTUE:** Project-related settings surfaced in the first-time user experience flow.
- **BigQuery sync fix:** Table sync now correctly handles table names containing spaces.

### Changed

- **Chat and UI:** Refactored chat message handling and tool execution; improved message sorting and thought signature for last assistant message; various AI chat and home/settings UI fixes (icons, cards, Schema Explorer, Settings layout).
- **PocketBase and tooling:** ClientResponseError used for 404 checks in PocketBase prompts; environment and build updates; removal of deprecated TaskTool/NoOpMessageEmitter and obsolete plan docs.

## [0.5.1] - 2026-02-11

### Added

- **PocketBase hooks and server lifecycle:** PocketBase hooks for lifecycle and context-aware discovery; enhanced server listener management and lifecycle handling (#239). Documentation and diagrams for PocketBase lifecycle; test script for listener lifecycle.

### Changed

- **PocketBase server:** Refactored `pocketbaseServer.ts` for clearer listener management and hook integration. Esbuild updated for PocketBase hook build. BaseViewHandler minor adjustments for lifecycle.

## [0.5.0] - 2026-02-08

### Important notice

**This release uses a new local backend and data format. Updating to 0.5.0 will reset any settings and saved knowledge you have stored locally.** You will need to reconfigure the extension and re-run indexing if you rely on extracted knowledge.

### Breaking changes

- **Backend replaced:** Prisma/SQLite has been removed in favor of PocketBase. All local data (settings, knowledge, chat state, schema cache) is stored in a new format. Existing local data is not migrated.
- **Snowflake removed:** The extension now supports BigQuery only. Snowflake has been removed from the UI and configuration. See `docs/re-enable-snowflake-support.md` in the repo if you need to re-enable it.
- **Workspace required:** The extension only activates when a workspace folder is open (MAN-257). If you open VS Code without a folder, the extension will not run until you open a folder.

### Added

- **PocketBase backend:** New embedded PocketBase server for local storage, with migrations and multi-window support. Auth and subscription state are now stored in PocketBase (MAN-258, MAN-251).
- **Vertex AI:** Optional Vertex AI as an alternative AI provider alongside the existing GenAI provider. Configurable via settings and FTUE.
- **First-time user experience (FTUE):** Guided setup flow, setup-complete page, and improved loading of projects/datasets during onboarding.
- **Table sample settings:** Configurable default row limit and staleness for table sampling (e.g. 250M rows). New `distinct.tableSample.*` options and improved query rewriting (MAN-177).
- **Schema sync:** Schema is synced in the background via `SchemaSyncService`; previous "download" flow has been replaced with sync-based updates.
- **Structured knowledge:** Grain, main date, and column statistics for tables; "live" knowledge updates; label-based knowledge removed in favor of structured fields.
- **Chat and indexing refactor:** Agent sessions, indexation progress in chat, and refactored AI chat navigation and view handler initialization.
- **Test connection:** Data warehouse and Vertex AI connection tests from setup/settings.
- **Google Drive:** Command to invalidate Google Drive credentials.
- **Light mode and themes:** Data view and UI improvements for light mode and other color schemes (MAN-205, MAN-245).
- **Misc:** File references in chat (MAN-181, MAN-244), chart panel design fix (MAN-232), data tab overflow fix (MAN-247), improved Python Language Server init and error handling.

### Changed

- **Auth and uptime:** PocketBase auth and subscription handling rewritten for correctness and reliability (MAN-258, MAN-251). PocketBase migrations run automatically, including on first run and with multi-window support (MAN-233, #225, #227).
- **Settings:** Extension and frontend-available settings are stored in PocketBase and synced via `SettingsSyncerService`.
- **Chat:** New chat design, message formatters (user/assistant/tool), and improved credential error handling and client invalidation.
- **Telemetry:** Indexation error context no longer includes `tableId`; LLM telemetry restricted to development.
- **Build and tooling:** Prettier and ESLint added; type generation and formatting updated. Release workflows updated (e.g. POCKETBASE_STORAGE_BUCKET, pr-to-production).

### Removed

- **Prisma:** All Prisma dependencies, schema, and migrations removed. Local data is now managed by PocketBase.
- **Snowflake:** Snowflake support removed from the extension (BigQuery only). Backend code remains for potential re-enable (see docs).
- **Knowledge labels:** Label-based knowledge removed in favor of structured knowledge fields.

## [0.4.4] - 2025-12-12

### Changed

Version bump of better-sqlite3 to support new node version in VSCode (140).

## [0.4.3] - 2025-11-25

### Fixed

The google sheets export now does not require a folder ID for upload. However the user is alerted when it is missing. A section for this is now added to the settings.

## [0.4.2] - 2025-11-24

### Changed

Improved blockage for sign in

## [0.4.1] - 2025-11-23

### Changed

Documentation changes in linew with the renaming of the extension to distinct.

## [0.4.0] - 2025-11-21

### Changed

Renaming of all data-go references to distinct

## [0.3.4] - 2025-11-21

### Fixed

Correct initial state for google sheets upload folder in data view.

## [0.3.3] - 2025-11-19

### Added

- Add a getting started page.

### Fixed

- Bug with download schema UI.

## [0.3.2] - 2025-11-16

### Fixed

- Setup page failing to load the settings.
- Nested structs failed to show in query results.

## [0.3.1] - 2025-11-16

### Changed

- Redesigned start screen with improved layout, logo positioning, and button styling
- Enhanced SignedOut component with Data Go logo and improved visual design
- Updated sign-in button styling with rounded-full design and arrow icon
- Improved tooltip integration for logout and settings buttons in start screen
- Refined authentication UI with better spacing and typography

### Removed

- Removed "Syncing tables sometimes takes a while, please be patient" message from Schema Explorer empty state as it was ugly

## [0.3.0] - 2025-11-16

### Added

- Implemented authentication gating across all webview components to require user sign-in before accessing features
- Added AuthGate component that displays signed-out state when user is not authenticated
- Added authentication state listener in SchemaExplorer to automatically refresh schemas upon user authentication
- Added 'Open Start Page' command to Data Go extension for quick access to the start screen
- Implemented AuthProvider and authentication state management for webview components
- Added SignedOut component to display when users are not authenticated

### Changed

- Enhanced authentication service to parse JWT ID tokens locally without backend verification
- Updated all webview views (AiChat, DataView, KnowledgeViewer, ParameterPanel, SchemaExplorer, TablePreview, TableSchema) to require authentication before rendering
- Improved authentication state synchronization between extension and webview components
- Refactored BaseViewHandler to support authentication state management and initialization

## [0.2.17] - 2025-11-16

### Changed

- Updated Google Drive authentication to use OAuth credentials from environment variables
- Reduced Google Drive API scopes to only require drive.file access
- Enhanced build process to inject Google API OAuth credentials at build time

## [0.2.16] - 2025-11-16

### Changed

- Internal workflow and release process changes

## [0.2.14] - 2025-11-16

### Added

- Implemented comprehensive authentication service with login/logout functionality for Data Go extension.
- Added subscription verification before executing queries and sending AI chat messages.
- Introduced export to Excel/XLSX functionality for query results.
- Added cancel queries functionality to stop running queries.
- Implemented handling for unsaved adhoc query windows to prevent data loss.
- Added Firebase authentication integration with environment variable configuration.
- Created new documentation for authentication flows, subscription architecture, and quickstart guides.
- Added URI handler and authentication provider registration for seamless authentication flow.

### Changed

- Updated extension logo with new design.
- Enhanced authentication flow and UI integration in the start screen.
- Improved error handling and logging throughout the authentication process.
- Refactored command registration to streamline login/logout processes.
- Updated UI components to display authentication status and provide login/logout buttons.
- Enhanced Firebase configuration to use environment variables for flexibility in development and CI/CD.

### Fixed

- Improved session management and token refresh handling in authentication service.
- Enhanced error messages and logging levels for better debugging and user feedback.
- Fixed UI update notifications to immediately reflect authentication status changes.

## [0.2.13] - 2025-11-15

### Added

- Implemented a new AI-assisted workflow for reviewing and suggesting changelog entries based on Pull Request changes.
- Enhanced CI workflows with version comparison and explicit version bump outputs.

### Changed

- Replaced the fully automated changelog generation process with an AI-powered PR review suggestion model.
- Updated conditions for AI review and general changelog review within CI workflows.

### Fixed

- Improved JSON validation, extraction, and error handling across CI workflows, particularly `check-npm-version` and `review-changelog`.
- Enhanced API key validation and handling (`GEMINI_API_KEY`) in changelog and CI workflows.
- Updated the Gemini model version used in the changelog workflow.
- Addressed various minor issues in workflow logic and messaging.

## [0.2.12] - 2025-11-15

### Removed

- Remove `CHANGELOG.md` in favor of automated changelog management.

### Changed

- Automate changelog updates as part of the release process.
