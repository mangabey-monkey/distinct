# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

This changelog is automatically generated during releases based on git history and changes.

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
