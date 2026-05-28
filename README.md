# AI SQL Analyst Agent using AutoGen, LLM, Python, and SQL

## Project Overview

This project demonstrates an AI-powered SQL analyst agent that converts natural language business questions into SQL queries, executes those queries against a relational analytics database, validates the results, and returns stakeholder-ready insights.

The goal of this project is to show how Large Language Models (LLMs) can be combined with SQL, Python, and agentic AI frameworks like Microsoft AutoGen to support business analytics workflows. Instead of manually writing SQL for every ad hoc business question, the analyst agent can interpret the user’s question, understand the database schema, generate SQL, execute the query, and return a clear business answer.

This project is designed for data analyst, business intelligence, and analytics engineering use cases where teams frequently need to answer questions about revenue, orders, customers, products, regions, and performance trends.

## Business Problem

Business teams often ask data teams questions such as:

* Which product category generated the highest revenue?
* Which region had declining sales over the last few months?
* Who are the top customers by total order value?
* What is the monthly revenue trend?
* Which products have high sales volume but low profit margin?

Answering these questions usually requires an analyst to manually inspect the schema, write SQL, run the query, validate the output, and explain the result in business terms.

This project simulates how an AI SQL analyst agent can reduce manual effort by automating parts of that workflow while still keeping the logic transparent and reviewable.

## Solution

The AI SQL Analyst Agent is designed to:

1. Accept a natural language business question from the user.
2. Read or reference the database schema.
3. Generate a SQL query based on the question.
4. Execute the SQL query against a relational database.
5. Validate whether the query ran successfully.
6. If the query fails, use error feedback to revise and retry.
7. Return the final answer in simple business language.

## Tools and Technologies

* Python
* Microsoft AutoGen
* Large Language Model API
* SQLite
* SQL
* Pandas
* Jupyter Notebook
* Retail analytics dataset
* GitHub

## Key Skills Demonstrated

* LLM-powered analytics automation
* Natural language to SQL generation
* SQL query execution
* Agentic AI workflow design
* Error handling and iterative query correction
* Business question interpretation
* Relational database querying
* Data analysis using Python
* Stakeholder-ready insight generation

## Project Architecture

```text
User Business Question
        ↓
AutoGen User Proxy Agent
        ↓
LLM SQL Analyst Agent
        ↓
Database Schema Context
        ↓
Generated SQL Query
        ↓
SQL Execution Function
        ↓
Query Result / Error Feedback
        ↓
Agent Query Correction Loop
        ↓
Final Business Answer
```

## Dataset

This project uses a retail analytics database that contains sample business data related to:

* Customers
* Orders
* Products
* Product categories
* Sales
* Revenue
* Profit
* Regions
* Order dates

The dataset is structured as relational tables so that the AI agent can answer realistic business questions using SQL joins, aggregations, filters, date logic, and ranking functions.

## Example Database Tables

### Customers Table

| Column Name   | Description                |
| ------------- | -------------------------- |
| customer_id   | Unique customer identifier |
| customer_name | Customer name              |
| segment       | Customer segment           |
| region        | Customer region            |

### Orders Table

| Column Name  | Description                  |
| ------------ | ---------------------------- |
| order_id     | Unique order identifier      |
| customer_id  | Customer linked to the order |
| order_date   | Date of order                |
| product_id   | Product purchased            |
| quantity     | Number of units ordered      |
| sales_amount | Total sales amount           |
| profit       | Profit from the order        |

### Products Table

| Column Name  | Description               |
| ------------ | ------------------------- |
| product_id   | Unique product identifier |
| product_name | Product name              |
| category     | Product category          |
| sub_category | Product sub-category      |

## Example Business Questions

The agent can answer questions such as:

```text
Which product category generated the highest total revenue?
```

```text
What are the top 5 customers by total sales?
```

```text
Which region had the highest profit margin?
```

```text
Show monthly revenue trends for 2024.
```

```text
Which products had high sales but low profit?
```

```text
Which customer segment had the highest average order value?
```

## Example Agent Workflow

### User Question

```text
Which product category generated the highest revenue in 2024?
```

### Agent-Generated SQL

```sql
SELECT
    p.category,
    SUM(o.sales_amount) AS total_revenue
FROM orders o
JOIN products p
    ON o.product_id = p.product_id
WHERE strftime('%Y', o.order_date) = '2024'
GROUP BY p.category
ORDER BY total_revenue DESC
LIMIT 1;
```

### Final Business Answer

```text
The product category with the highest revenue in 2024 was Technology, with total revenue of $245,000.
```

## Core Features

### 1. Natural Language to SQL

The agent converts plain English business questions into executable SQL queries.

### 2. Schema-Aware Query Generation

The agent uses database schema context to understand table names, column names, and relationships before writing SQL.

### 3. SQL Execution

A Python function executes the generated SQL query against the SQLite database and returns the result.

### 4. Error Feedback Loop

If the SQL query fails due to incorrect syntax, table names, or column names, the error message is passed back to the agent so it can revise the query.

### 5. Business-Friendly Output

The final output is not just a raw SQL result. The agent explains the result in simple language that a stakeholder can understand.

## Repository Structure

```text
ai-sql-analyst-agent/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── retail_orders.csv
│   ├── customers.csv
│   └── products.csv
│
├── database/
│   ├── create_tables.sql
│   ├── insert_sample_data.sql
│   └── retail_analytics.db
│
├── notebooks/
│   └── ai_sql_analyst_agent.ipynb
│
├── src/
│   ├── config.py
│   ├── database.py
│   ├── schema_context.py
│   ├── sql_executor.py
│   └── agent_workflow.py
│
├── examples/
│   ├── sample_questions.md
│   └── sample_outputs.md
│
└── screenshots/
    ├── agent_question.png
    ├── generated_sql.png
    ├── query_result.png
    └── final_answer.png
```

## How the Project Works

### Step 1: Prepare the Database

The retail dataset is loaded into a local SQLite database. The database contains normalized tables for customers, orders, and products.

### Step 2: Define Schema Context

The schema context gives the LLM information about available tables, columns, and relationships. This helps the agent generate accurate SQL.

### Step 3: Configure the AutoGen Agents

The project uses Microsoft AutoGen to create an agent workflow. One agent acts as the SQL analyst, while another acts as the user proxy that executes approved functions.

### Step 4: Register SQL Execution Function

A Python function is created to execute SQL queries against the SQLite database. This function is registered with the agent so the LLM can call it during the workflow.

### Step 5: Ask Business Questions

The user asks a natural language question. The agent interprets the question and generates SQL.

### Step 6: Execute and Validate SQL

The SQL query is executed. If the query succeeds, the result is returned. If it fails, the error message is used to correct the SQL.

### Step 7: Return Final Insight

The agent summarizes the result in business-friendly language.

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/ai-sql-analyst-agent.git
cd ai-sql-analyst-agent
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate the environment:

```bash
# Mac/Linux
source venv/bin/activate
```

```bash
# Windows
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Add API Key

Create a `.env` file in the project root.

```text
OPENAI_API_KEY=your_api_key_here
```

Do not upload your `.env` file to GitHub.

## Requirements

Example `requirements.txt`:

```text
pyautogen
openai
pandas
python-dotenv
sqlite-utils
jupyter
```

## Example Code Structure

### SQL Execution Function

```python
import sqlite3
import pandas as pd

def execute_sql(query: str, db_path: str = "database/retail_analytics.db"):
    try:
        conn = sqlite3.connect(db_path)
        result = pd.read_sql_query(query, conn)
        conn.close()
        return result.to_string(index=False)
    except Exception as e:
        return f"SQL execution error: {str(e)}"
```

### Example Schema Context

```python
schema_context = """
Database contains the following tables:

customers(customer_id, customer_name, segment, region)

products(product_id, product_name, category, sub_category)

orders(order_id, customer_id, product_id, order_date, quantity, sales_amount, profit)

Relationships:
orders.customer_id = customers.customer_id
orders.product_id = products.product_id
"""
```

## Sample Questions and Expected Outputs

### Question 1

```text
Which region generated the highest total revenue?
```

Expected output:

```text
The West region generated the highest total revenue based on total sales_amount.
```

### Question 2

```text
Which product category had the lowest profit margin?
```

Expected output:

```text
The agent calculates profit margin by category and identifies the category with the lowest margin.
```

### Question 3

```text
Show the monthly revenue trend.
```

Expected output:

```text
The agent groups sales by month and returns the revenue trend over time.
```

## Business Impact

This project shows how AI can support analytics teams by reducing the time required to answer repetitive business questions. Instead of manually writing SQL for every request, the agent can generate, execute, and validate queries while keeping the process transparent.

Potential business benefits include:

* Faster ad hoc analysis
* Reduced manual SQL writing effort
* Improved access to data for non-technical stakeholders
* Consistent query generation using schema context
* Faster exploration of business trends and KPIs

## Resume Description

**AI SQL Analyst Agent — AutoGen, LLM, Python, SQL**
Built an LLM-powered SQL analyst agent using Microsoft AutoGen to translate natural language business questions into SQL, execute queries against a retail analytics database, validate results, and return stakeholder-ready insights through iterative agent feedback loops.

## Future Enhancements

* Add a Streamlit interface for business users
* Connect the agent to Snowflake instead of SQLite
* Add query safety checks before execution
* Add support for chart generation
* Add semantic layer definitions for business metrics
* Add user role-based access controls
* Add dashboard export to Tableau or Power BI
* Add query history logging and performance tracking

## Important Note

This project is intended for educational and portfolio purposes. The dataset used is sample or synthetic retail data and does not contain confidential information.
