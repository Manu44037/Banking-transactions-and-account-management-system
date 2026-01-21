# 🏦 Banking / Capital Markets SQL Project (PostgreSQL)

An end-to-end PostgreSQL database project simulating a simplified Banking/Capital Markets system.  
This project demonstrates schema design, transaction-safe fund transfers using stored procedures, trigger-based audit logging for compliance, reporting views, and query performance analysis using `EXPLAIN ANALYZE`.

---

## 🚀 Features Implemented

✅ Relational Schema Design (bank schema)  
✅ Tables: Customers, Accounts, Transactions, Audit Log  
✅ Sample Data Insert Scripts  
✅ Stored Procedure for Secure Fund Transfer  
✅ Trigger-based Audit Logging (old/new values captured)  
✅ Reporting View: `account_summary`  
✅ Query performance testing using `EXPLAIN ANALYZE`

---

## 🧱 Database Schema

### Tables Created
- `bank.customers` → customer details + KYC status
- `bank.accounts` → account details + balance + status
- `bank.transactions` → deposit/withdraw/transfer records
- `bank.audit_log` → captures updates (old_data/new_data) for compliance

---

## 🔐 Audit Logging

Audit trigger is implemented on `bank.accounts` updates:

- Automatically logs:
  - table_name
  - action (UPDATE)
  - record_id
  - old_data (JSONB)
  - new_data (JSONB)
  - timestamp

✅ Useful for compliance, security monitoring, and fraud investigation.

---

## ⚙️ Stored Procedure: `transfer_money()`

Procedure: `bank.transfer_money(p_from_account, p_to_account, p_amount)`

### Logic
- Locks sender row (`FOR UPDATE`)
- Validates:
  - sender exists
  - receiver exists
  - sufficient funds
- Updates balances safely
- Logs transfer into `bank.transactions`

---

## 📊 Reporting Layer

### View Created
✅ `bank.account_summary`

Provides a customer-to-account reporting format:
- customer_id
- full_name
- account_number
- account_type
- balance
- status

---

## 🧪 Testing & Verification

Example execution:
```sql
CALL bank.transfer_money(1, 2, 700);
