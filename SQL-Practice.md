# SQL Practice - SQLZoo

## Objective 
Completed SQLZoo's full tutorial series to build SQL querying and data manipulation skills, with an eye toward how these skills apply to log analysis and security data review (e.g., querying SIEM-backend data, filitering large event datasets).

## Course
[SQLZoo](https://sqlzoo.net/wiki/SQL_Tutorial)

## Tutorials Completed
- **SELECT basics**: fundamental 'SELECT' and 'WHERE' filtering syntax
- **SELECT from WORLD**: filtering and conditional logic practice using a world country dataset
- **SELECT within SELECT**: writing subqueries, e.g., comparing a row's value against an aggregate computed in a nested query
- **SELECT from Nobel**: additional filtering practice using a real dataset of Nobel Prize winners
- **SUM and COUNT**: aggregate computed in a nested query
- **JOIN / More JOIN**: combining data across multiple related tables (e.g., matching event records to the entities they reference)
- **Using NULL**: handling missing/null values in filters and joins
- **Self JOIN**: joining a table to itself to compare rows within the same dataset

## Skill Areas Practiced

### Filtering & Conditional Logic
Practiced writing 'WHERE' clauses with multiple conditions: the same pattern used to isolate specific event types in a log table (e.g., filtering for failed logins above a threshold).

### Joins
Practiced joining two and three related tables together, similar to how a SOC analyst correlates user/account data with event or session data stored in separate tables.

### Aggregation
Practiced 'COUNT()', 'SUM()', and 'GROUP BY' to summarize data: directly parallel to counting event occurrences per account or per host, which is core to anomaly detection.

### Subqueries
Practiced nesting one query inside another to filter based on a computed value (e.g., comparing a row against an aggregate): useful for questions like "which accounts had more failed logins than the average."

### Why This Connects to My Other Work
The SPL query I wrote in my [Splunk SIEM lab](https://github.com/6c2r2fqpmq-a11y/home-siem-lab-splunk) to count failed logins by account ('stats count by Account_Name') follows the same logical structure as a SQL 'GROUP BY': this course reinforced how the same query logic applies across different tools (SQL, SPL, and even command line tools like 'awk', covered in my [Linux practice write-up](./linux-commands-practice.md)
