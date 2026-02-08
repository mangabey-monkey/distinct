# DISTINCT: BigQuery

> AI query coding agent with deep knowledge about your specific data warehouse which speeds up every data extraction and analysis.

### Data Privacy

Your data is only processed on your local machine and in your data warehouse—and by your AI model provider if you use AI features.

### AI Query Agent

- Coding Chatbot with deep knowledge about your specific data warehouse.
- **Bring Your Own Key**. Your data is only shared between you and your AI model provider.
- Choose what tables the AI should have access to.
- The tables are analyzed by AI to understand all the specific details about the format and structure of the actual data, beyond the table schemas.
- Coding AI chat that helps you write accurate queries, based on the learned knowledge.
- Knowledge learned from your chats and queries are remembered for later chats.

### Query and Exploration Tools

- View and explore your tables and schemas.
- Quick query window
- Powerful query runner with parameterized query support.
- Clean view of query results.
- Quick and beautiful charts.
  ![](media/readme/chart.gif)

## Explore Your Database Objects

Choose which objects to sync and get a comprehensive overview of tables and their schemas.

![](media/readme/schema_overview.png)

Bookmark the most important tables for quick access.

![](media/readme/schema_bookmarked.png)

## Ad-hoc Query Window

Create an ad-hoc query window with `CMD+Option+N` (Mac) or `Ctrl+Alt+N` (Windows/Linux).

Write and test queries quickly, then save them to your VSCode project when you're satisfied with the results.

## Run Your Queries

Execute any SQL file or ad-hoc query with `CMD+Enter` (Mac) or `Ctrl+Enter` (Windows/Linux).

## Parameterized Queries

- Define parameters in queries using either `:` or `@` syntax
- Set parameter values in the parameters panel
- Use the Python package to run parameterized queries in your scripts or Jupyter notebooks

    ![](media/readme/python_run_query.png)

## Data View

View your query results in a clean, interactive interface.

- Drag and select data to copy to any application that supports tables
- Export to CSV, XLSX, and Google Sheets
- Clean visualization of arrays and structs

    ![](media/readme/array_design.gif)

## Quick and Beautiful Charts

Create charts from your query results with just a few clicks.

![](media/readme/chart.png)

## Coming Soon: Ad-hoc Dashboards

- Create parameterized queries and define connected charts
- Export to an ad-hoc dashboard with exposed parameters
- Set up cloud connections to share dashboards with your team

## Code Completions and IntelliSense

Get intelligent SQL code highlighting, suggestions, and completions as you write.

![](media/readme/complete_columns.png)

## AI Query Chatbot

An intelligent chatbot that helps you write queries specific to your data warehouse.

![](media/readme/query_agent.png)

Choose which tables should be accessible to the AI. The AI analyzes tables beforehand to understand all the logic and details necessary to help you write better queries.

![](media/readme/toggle_ai_accessible.png)
![](media/readme/analysis_running.png)

The AI agent continuously learns while you use the tool:

- Learns from your queries
- Learns from your conversations
- Learns from the data results

### Updates Coming Soon!

The AI chatbot is under active development with major updates coming soon. The current version is a preview of the setup and workflow.

_Note: You can disable AI features if you prefer not to use them._

## Interaction with Other SQL Extensions

If you experience issues with code completions or query execution, another SQL-related extension may be conflicting with _DISTINCT_. Try disabling other SQL extensions to resolve the issue.

## Coming Soon: Share AI Knowledge Across Your Team

When your AI agent learns about your data, you'll be able to share that knowledge with your entire team.

## Data Processing

_DISTINCT_ is designed with privacy in mind. All your data, query results, and AI learned knowledge are stored locally in a SQLite database on your computer. When using AI features, requests are sent directly to Google Gemini without any intermediate processing by _DISTINCT_. Only anonymous usage analytics are sent to Microsoft Azure to help improve the extension - no queries, results, or personal information ever leaves your machine except when you explicitly connect to your data warehouse. Read more under Telemetry.

![](media/readme/data_processing.png)

## Telemetry

This extension collects anonymous usage data to help improve the product. All telemetry respects VS Code's telemetry settings and follows industry best practices. We never collect personally identifiable information (PII), SQL query content, or file paths.

For detailed information about data collection, see [TELEMETRY.md](TELEMETRY.md).
