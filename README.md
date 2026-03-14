# Expense Tracker MCP Server

A **Remote MCP (Model Context Protocol) Server** built using **FastMCP** that allows AI assistants (like Claude Desktop or other MCP clients) to **record, list, and analyze personal expenses**.

This project demonstrates how AI agents can interact with external tools using the **Model Context Protocol (MCP)**.

---

# 🚀 Features

* Add expenses to a database
* List expenses within a date range
* Summarize expenses by category
* Provide predefined expense categories via MCP resources
* Asynchronous database operations using `aiosqlite`
* Remote HTTP MCP server
* Ready to integrate with AI assistants and agent frameworks

---

# 🧠 MCP Architecture

```
User
 │
 ▼
AI Assistant (Claude / Agent)
 │
 ▼
MCP Client
 │
 ▼
Expense Tracker MCP Server
 │
 ▼
SQLite Database
```

The MCP server exposes **tools** and **resources** that AI models can call dynamically.

---

# 📂 Project Structure

```
expense-tracker-mcp
│
├── main.py
├── categories.json
├── expenses.db (created automatically)
└── README.md
```


# 🧰 Available MCP Tools

## 1️⃣ Add Expense

Adds a new expense entry.

**Tool**

```
add_expense
```

**Parameters**

| Parameter   | Type   | Description          |
| ----------- | ------ | -------------------- |
| date        | string | Expense date         |
| amount      | float  | Expense amount       |
| category    | string | Expense category     |
| subcategory | string | Optional subcategory |
| note        | string | Optional note        |

Example:

```json
{
 "date": "2026-03-14",
 "amount": 500,
 "category": "Food",
 "subcategory": "Groceries",
 "note": "Supermarket"
}
```

---

## 2️⃣ List Expenses

Returns expenses within a date range.

**Tool**

```
list_expenses
```

**Parameters**

| Parameter  | Type   |
| ---------- | ------ |
| start_date | string |
| end_date   | string |

---

## 3️⃣ Summarize Expenses

Summarizes expenses grouped by category.

**Tool**

```
summarize
```

**Parameters**

| Parameter  | Type              |
| ---------- | ----------------- |
| start_date | string            |
| end_date   | string            |
| category   | string (optional) |

Example response:

```json
[
 {
  "category": "Food",
  "total_amount": 3200,
  "count": 5
 }
]
```

---

# 📚 MCP Resources

### Categories Resource

URI:

```
expense:///categories
```

Returns available expense categories in JSON format.

Example:

```json
{
 "categories": [
  "Food & Dining",
  "Transportation",
  "Shopping",
  "Entertainment",
  "Bills & Utilities",
  "Healthcare",
  "Travel",
  "Education",
  "Business",
  "Other"
 ]
}
```

---

# 🗄️ Database

The server automatically creates a SQLite database in the system temporary directory:

```
/tmp/expenses.db
```

Table structure:

| Column      | Type    |
| ----------- | ------- |
| id          | INTEGER |
| date        | TEXT    |
| amount      | REAL    |
| category    | TEXT    |
| subcategory | TEXT    |
| note        | TEXT    |

---

# ⚡ Why Async Database?

This server uses **aiosqlite** to support:

* concurrent requests
* better performance
* non-blocking MCP tool execution

---

# 🤖 Example Use Cases

This MCP server can be used with:

* Claude Desktop
* AI agents
* LangGraph
* CrewAI
* AutoGen
* Custom MCP clients

Example user prompt:

```
I spent 450 on groceries today
```

The AI assistant can automatically call:

```
add_expense
```

---

# 🔗 Connecting to Claude Desktop

You can register this MCP server in Claude Desktop using:

```bash
uv run fastmcp install claude-desktop main.py
```

Restart Claude Desktop after installation.

---

# 📈 Future Improvements

* Expense analytics
* Budget alerts
* Monthly reports
* Chart generation
* Vector search for notes
* Multi-user support

