# Data Go

Explore and query your data warehouse. Get support from AI.
Works with BigQuery and Snowflake.

- Explore database objects
- Ad-hoc query windows
- Query runner
- Parameterised queries
- Clean data view
- Quick and beautiful charts
- AI Query Chatbot

![](media/readme/chart.gif)

## Explore your database objects

Choose what objects to sync and get good overview of tables and their schemas.

![](media/readme/schema_overview.png)

Bookmark the most important tables

![](media/readme/schema_bookmarked.png)

## Ad-hoc query window

`CMD+Option+N` / `Ctrl+Alt+N` to create an ad-hoc query window
Write a query and run it. If you like it, save it in your VSCode project.

## Run your queries

`CMD+Enter` / `Ctrl+Enter` to run any SQL file or ad-hoc query.

## Parameteriesed queries

- Define parameters in queries using either `:` or `@`.
- Set the values of the parameters in parameters panel.
- Use the python package `...` run parameterised queries in your python scripts or jupyter notebooks

    ![](media/readme/python_run_query.png)

## Data view

View you results

- Drag+select your data, and copy to any software supporting tables.
- Export to CSV, xlsx, and Google Sheets
- Clean view of arrays and structs.

    ![](media/readme/array_design.gif)

## Quick and beautiful charts

Create a chart from your data result.
![](media/readme/chart.png)

## Coming soon: ad-hoc dashboards

- Create a parameteriesed query and define connected charts.
- Export it to an ad-hoc dashboard with the parameters exposed.
- Set up a cloud connection to share with others.

## Code Completions and IntelliSense

SQL code highlighting, suggestions and completions.

![](media/readme/complete_columns.png)

## Query AI Chatbot

Chatbot that helps you write queries specific for you data warehouse.

![](media/readme/query_agent.png)

Choose what tables should be accessible for the AI, and the AI analyses the tables beforehand to understand all the logic and details that are neccessary to best help you write queries.

![](media/readme/toggle_ai_accessible.png)
![](media/readme/analysis_running.png)

The AI agent keeps learning while you use the tool. - Learns from your queries. - Learns from your chats. - Learns from the data results.

### Updates Coming Soon!

The AI chatbot is under development and some major updates will be released soon. The current version is a preview of the setup and workflow.

_You can disable AI if you don't want it._

## Interaction with other SQL extensions

If you are having trouble with code completions or running queries, the reason could be that another SQL-related extension hijacks everything that is SQL. Try disabling other extensions to see if it makes a difference.

## Coming: share AI knowledge across team

When your agent learns stuff about the data, you set up so that is shared within your team.

## Telemetry

This extension collects anonymous usage data to help improve the product. All telemetry respects VS Code's telemetry settings and follows best practices. We never collect personally identifiable information (PII), SQL query content, or file paths.

For detailed information about what data we collect, see [TELEMETRY.md](TELEMETRY.md).
