# AI SQL Analyst Agent using AutoGen, LLM, Python, and SQL

## Project Overview

This project builds an AI-powered SQL analyst agent that converts natural language business questions into SQL queries, executes those queries against a relational SQLite database, validates the results, and returns business-friendly outputs.

The goal of this project is to demonstrate how Large Language Models (LLMs), Microsoft AutoGen, Python, and SQL can be combined to support analytics workflows. Instead of manually writing SQL for every ad hoc business question, the agent uses database schema context to generate SQL, run the query, and return the result in a reviewable format.

This project is designed for data analyst, business intelligence, and analytics engineering use cases where teams frequently need to answer questions about customers, revenue, invoices, products, genres, artists, and sales performance.

---

## Business Problem

Analytics teams often receive business questions such as:

- Who are the top customers by total revenue?
- Which countries generate the most revenue?
- What are the top-selling genres?
- Which sales support agent manages the highest revenue customers?
- Which artists generated the most sales?

Answering these questions usually requires an analyst to inspect the schema, identify the right tables, write SQL joins, execute the query, validate the result, and explain the output.

This project simulates how an AI SQL analyst agent can reduce manual effort by helping generate and validate SQL while keeping the query logic transparent and reviewable.

---

## Solution

The AI SQL Analyst Agent is designed to:

1. Accept a natural language business question from the user.
2. Read the SQLite database schema.
3. Generate a SQL query using only available tables and columns.
4. Extract the SQL query from the LLM response.
5. Execute the SQL query against the Chinook SQLite database.
6. Validate whether the query ran successfully.
7. If the query fails, pass the SQL error back to the agent for correction.
8. Return the generated SQL, execution status, query result, and business explanation.

---

## Tools and Technologies

- Python
- Microsoft AutoGen
- OpenAI-compatible LLM API
- SQLite
- SQL
- Pandas
- Jupyter Notebook
- Chinook relational database
- Anaconda

---

## Key Skills Demonstrated

- LLM-powered analytics automation
- Natural language to SQL generation
- AutoGen agent workflow design
- SQLite database querying
- Schema-aware SQL generation
- SQL execution using Python
- Query validation and error handling
- Iterative SQL correction using feedback loops
- Relational joins and aggregations
- Business insight generation from SQL outputs

---

## Project Architecture

```text
User Business Question
        ↓
AutoGen User Proxy Agent
        ↓
AutoGen SQL Analyst Agent
        ↓
Database Schema Context
        ↓
Generated SQL Query
        ↓
SQL Extraction Function
        ↓
Python SQL Execution Function
        ↓
Query Result or SQL Error
        ↓
Error Feedback Loop
        ↓
Final SQL Output + Business Result
