# Banking Transaction & Capital Markets Trade Management System (SQL)

A **portfolio-ready SQL project** that combines **core banking operations** (customers, accounts, money transfers) with **capital markets trading** (instruments, trades, portfolio holdings). Designed to showcase **stored procedures, triggers, indexing and reporting views** for a SQL Developer role.

---

## 🚀 Highlights

- **Core Banking Model**: `customers` → `accounts` → `transactions`
- **Stored Procedure (bank-grade)**: `transfer_money()`
  - Validates accounts + balance
  - Uses row-level locks (`FOR UPDATE`)
  - **Deadlock prevention** via deterministic lock ordering (`LEAST/GREATEST`)
- **Audit Trigger (Compliance)**
  - Logs `INSERT/UPDATE/DELETE` on `accounts` into `audit_log`
  - Stores `old_data` + `new_data` as **JSONB**
- **Capital Markets Module**
  - `instruments`, `trades`, `portfolio_holdings`
  - Stored Procedure: `execute_trade()` supports **BUY/SELL**
- **Reporting Views**: `account_summary`, `portfolio_summary`
- **Performance Proof**
  - Composite + supporting indexes
  - `EXPLAIN ANALYZE` demo query included

---

## 🧰 Tech Stack

- PostgreSQL 13+ (works on 14/15/16/17)
- pgAdmin / DBeaver (recommended)

---

## 📁 Project Structure

```
bank_capital_sql_project/
│
├── sql/
│   ├── 01_schema.sql
│   ├── 02_tables.sql
│   ├── 03_demo_data.sql
│   ├── 04_views.sql
│   ├── 05_procedures.sql
│   ├── 06_triggers.sql
│   ├── 07_indexes.sql
│   └── 08_demo_queries.sql
│
├── docs/
│   ├── project_overview.md
│   └── interview_script.md
│
└── README.md
```

---

## ✅ Setup & Run (Copy-Paste)

### 1) Create DB + connect

```sql
CREATE DATABASE bank_capital_db;
```

Connect to the DB, then run scripts in this order:

### 2) Run scripts (ORDER matters)

```sql
\i sql/01_schema.sql
\i sql/02_tables.sql
\i sql/03_demo_data.sql
\i sql/06_triggers.sql
\i sql/05_procedures.sql
\i sql/04_views.sql
\i sql/07_indexes.sql
\i sql/08_demo_queries.sql
```

> If you are using **DBeaver/pgAdmin**, just open each file and execute in the same order.

---

## 🧪 Demo (Manager Ready)

### A) View customer accounts
```sql
SELECT * FROM bank.account_summary;
```

### B) Money transfer demo
```sql
CALL bank.transfer_money(1, 2, 700);

SELECT account_id, balance
FROM bank.accounts
WHERE account_id IN (1,2);
```

### C) Audit log proof
```sql
SELECT *
FROM bank.audit_log
ORDER BY changed_at DESC
LIMIT 10;
```

### D) Execute a trade (Capital Markets)
```sql
CALL bank.execute_trade(3, 'TCS', 'BUY', 5);
SELECT * FROM bank.portfolio_summary;
```

### E) Performance proof
```sql
EXPLAIN ANALYZE
SELECT *
FROM bank.transactions
WHERE from_account = 1
ORDER BY created_at DESC;
```

---

## 📌 Interview Explanation (30-45 sec)

> “I built a Banking and Capital Markets SQL system. Core banking includes customers, accounts and a transactions ledger. I implemented a bank-grade `transfer_money()` stored procedure with row-level locks and deterministic lock ordering to prevent deadlocks under concurrent transfers. For compliance, I created triggers capturing INSERT/UPDATE/DELETE changes on accounts into an `audit_log` with old and new JSON values. On the capital markets side, I modeled instruments, trades and portfolio holdings with an `execute_trade()` procedure that updates cash and holdings. I added composite indexes and validated performance using `EXPLAIN ANALYZE`, and created views for reporting: `account_summary` and `portfolio_summary`.”

---

## 🔮 Future Enhancements

- Transaction reversal / chargeback workflow
- Role-based access (PostgreSQL roles)
- Partition large transaction tables by month/year
- AML / fraud flags and alerting queries

---

## 👤 Author

**Manoj Kumar** (Portfolio Project)
# Banking-transactions-and-account-management-system
