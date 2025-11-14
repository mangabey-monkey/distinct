# Telemetry and Analytics

This extension collects anonymous usage data to help improve the product. All telemetry respects VS Code's telemetry settings and follows the [VS Code Telemetry Extension Guide](https://code.visualstudio.com/api/extension-guides/telemetry).

## Implementation

We use the official `@vscode/extension-telemetry` module which automatically respects the user's `telemetry.telemetryLevel` setting. Telemetry is sent to Azure Application Insights using a connection string configured at build time.

## Common Properties

All events automatically include these common properties:

- `warehouseType` - The type of data warehouse being used (e.g., "BigQuery", "Snowflake")
- `debug` - Set to "true" when running in development mode

## Tracked Events

| Event Name                        | Description                             | Properties                                                                                              | Measurements                                                                                                                                                                                                                                       |
| --------------------------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `analytics_initialized`           | Analytics system initialized            | None                                                                                                    | None                                                                                                                                                                                                                                               |
| `fully_initialized`               | Extension fully initialized             | None                                                                                                    | `initializationTimeMs` - Time taken to initialize (ms)                                                                                                                                                                                             |
| `extension_initialization_failed` | Extension initialization failed         | `errorMessage` (sanitized), `hasStack`                                                                  | `initializationTimeMs`                                                                                                                                                                                                                             |
| `schema_downloaded`               | Schema metadata downloaded              | `scope` - "project", "dataset", "table", or "dataset_schemas"                                           | `tablesCount` (for dataset_schemas scope)                                                                                                                                                                                                          |
| `schema_download_toggled`         | Schema download preference changed      | `scope` - "dataset" or "table"<br>`action` - "download" or "undownload"                                 | None                                                                                                                                                                                                                                               |
| `schema_refreshed`                | Schema metadata refreshed               | `scope` - "project", "dataset", "table", or "all"<br>`hasSchema` - "true" or "false" (table scope only) | `tablesNeedingColumnsCount` (project/dataset scope)<br>`datasetsCount` (project/all scope)<br>`successCount` (project/dataset/all scope)<br>`failureCount` (project/dataset/all scope)<br>`tablesCount` (all scope)<br>`projectsCount` (all scope) |
| `table_bookmarked`                | Table bookmark status changed           | `bookmarked` - "true" or "false"                                                                        | None                                                                                                                                                                                                                                               |
| `ai_indexing_selected`            | AI indexing option selected for a table | None                                                                                                    | None                                                                                                                                                                                                                                               |
| `table_preview_opened`            | Table preview view opened               | None                                                                                                    | None                                                                                                                                                                                                                                               |
| `table_schema_opened`             | Table schema view opened                | None                                                                                                    | None                                                                                                                                                                                                                                               |
| `column_discovery_started`        | Column discovery process started        | `scope` - "project", "dataset", or "table"<br>`source` - "discover_action" (optional)                   | None                                                                                                                                                                                                                                               |
| `query_created_from_table`        | Query created from table context        | `source` - "select_top", "schema_explorer", or "column"                                                 | None                                                                                                                                                                                                                                               |
| `column_name_copied`              | Column name copied to clipboard         | None                                                                                                    | `columnNameLength` - Length of column name                                                                                                                                                                                                         |
| `chat_created`                    | New AI chat session created             | `totalChats` - Total number of chats                                                                    | None                                                                                                                                                                                                                                               |
| `chat_message_sent`               | Message sent in AI chat                 | `isFirstMessage` - "true" or "false"                                                                    | `messageLength` - Length of message (characters)                                                                                                                                                                                                   |
| `parameter_value_filled`          | SQL parameter value filled              | None                                                                                                    | None                                                                                                                                                                                                                                               |
| `data_exported`                   | Query results exported                  | `format` - "csv" or "googlesheets"                                                                      | `rowCount` - Number of rows exported<br>`columnCount` - Number of columns exported                                                                                                                                                                 |
| `chart_exported`                  | Chart visualization exported            | `format` - "png" or "svg"                                                                               | None                                                                                                                                                                                                                                               |
| `query_executed`                  | SQL query executed                      | `hasFileUri` - "true" or "false"<br>`hasParameters` - "true" or "false"                                 | `sqlLength` - Length of SQL query (characters)<br>`parameterCount` - Number of parameters used                                                                                                                                                     |

## Privacy and Data Collection

- **No PII**: We never collect personally identifiable information (PII)
- **No Code**: SQL queries are not sent, only metadata like length and parameter count
- **No File Paths**: File paths are sanitized in error messages
- **User Control**: All telemetry respects VS Code's `telemetry.telemetryLevel` setting
- **Transparency**: Users can view telemetry data using VS Code CLI: `code --telemetry`

## Error Tracking

Errors are tracked using `logAnalyticsError()` which:

- Sanitizes error messages to remove file paths, emails, and table names
- Includes stack trace presence (but not the actual stack trace)
- Never includes sensitive data or PII
