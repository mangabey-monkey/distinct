# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

This changelog is automatically generated during releases based on git history and changes.

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
