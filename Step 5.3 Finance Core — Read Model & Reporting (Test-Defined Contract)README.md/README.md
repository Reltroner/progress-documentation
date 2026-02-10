# Step 5.3 Finance Core — Read Model & Reporting (Test-Defined Contract)

## Purpose & Responsibility

This documentation defines the **authoritative behavior of the finance core read model and reporting layer**, as enforced by the current test suite.

The scope covered here includes:

- Ledger read model
- Trial Balance
- Profit & Loss
- Balance Sheet
- Comparative statements (Balance Sheet & Profit & Loss)
- Read-only guarantees for reporting routes

**This document is test-driven, not intention-driven.**  
All guarantees below are derived strictly from passing tests and nothing else.

---

## Architectural Position

The components validated by these tests sit in the **read side** of the accounting system:

- They **consume immutable accounting data** (transactions, transaction lines).
- They **never mutate state**.
- They **derive financial statements deterministically** from ledger data.
- They are **downstream of posting, locking, and validation mechanisms**.

This layer assumes:

- Transactions are already valid and posted.
- Line ordering, balancing, and immutability are enforced elsewhere.
- Fiscal periods exist and are closed/open as required upstream.

---

## Invariants & Guarantees (Locked by Tests)

### Ledger Read Model

**Guaranteed invariants:**

- Ledger queries do **not mutate transactions or transaction lines**.
- Ledger lines preserve:
  - Account association
  - Debit / credit values
  - Deterministic calculated amount
- Transaction detail `line_no` is **strictly sequential and gapless**, starting from 1.

**Locked by:**
- `Tests\Unit\Accounting\Read\LedgerQueryServiceTest`
  - `it reads ledger lines without mutation`
  - `transaction lines have sequential line numbers`

---

### Trial Balance

**Guaranteed invariants:**

- Trial balance aggregates **all accounts** for a fiscal period.
- Total debits **must equal** total credits.
- Balance computation is purely derived from ledger lines.
- Returned balances are immutable value objects.

**Locked by:**
- `Tests\Unit\Accounting\Read\TrialBalanceServiceTest`
  - `trial balance is balanced`

---

### Balance Sheet

**Guaranteed invariants:**

- The accounting equation always holds:
```

Assets = Liabilities + Equity

```
- Values are derived from the same ledger source as Trial Balance.
- No mutation occurs during statement generation.

**Locked by:**
- `Tests\Feature\Reports\BalanceSheetTest`
- `balance sheet equation holds`

---

### Profit & Loss

**Guaranteed invariants:**

- Profit & Loss is deterministic for a given period.
- Repeated generation yields identical results.
- Income and expense aggregation is consistent with ledger data.

**Locked by:**
- `Tests\Feature\Reports\ProfitLossTest`
- `profit loss projection is deterministic`

---

### Comparative Balance Sheet

**Guaranteed invariants:**

- Multiple fiscal periods can be compared in a single statement.
- The accounting equation holds **independently per period**.
- No cross-period contamination of values occurs.

**Locked by:**
- `Tests\Feature\Reports\ComparativeBalanceSheetTest`
- `comparative balance sheet preserves equation per period`

---

### Comparative Profit & Loss

**Guaranteed invariants:**

- Comparative Profit & Loss supports **multiple periods** simultaneously.
- Each line contains an amount for **every requested period**.
- Missing data is normalized to zero, not omitted.
- An empty comparative result is allowed only if the ledger itself is empty.

**Locked by:**
- `Tests\Feature\Reports\ComparativeProfitLossTest`
- `comparative profit loss contains multiple periods`

---

### Read-Only Reporting Guarantees

**Guaranteed invariants:**

- All reporting routes are strictly read-only.
- No HTTP GET request under `/reports` mutates state.
- Middleware enforcement is respected during tests.

**Locked by:**
- `Tests\Feature\Reports\ReportsReadOnlyTest`
- `reports routes are read only`

---

## What This Layer Intentionally Does NOT Do

- Does **not** create, update, or delete transactions.
- Does **not** validate journal balancing at write time.
- Does **not** manage fiscal period lifecycle.
- Does **not** apply authorization beyond gateway/session checks.
- Does **not** infer business meaning beyond ledger data.
- Does **not** perform forecasting or projections beyond deterministic aggregation.

These responsibilities are explicitly out of scope.

---

## Test Coverage Summary (Authoritative)

**Passing Test Suite:**

- Unit Tests
- LedgerQueryService behavior
- TrialBalanceService correctness
- Feature Tests
- Balance Sheet
- Profit & Loss
- Comparative statements
- Read-only enforcement

**Status:**
- 10 tests
- 32 assertions
- All passing

The test suite is the **contract**.  
Any behavior not asserted here is undefined.

---

## Failure Modes & Edge Cases

- Empty ledger data may result in:
- Empty statement lines
- Zeroed comparative values
- Missing periods must be explicitly supplied by caller.
- Tests assume valid fiscal periods exist.
- Tests do not cover concurrent read scenarios.

These are accepted and intentional constraints.

---

## Notes for Future Extension (Freeze-Safe)

Extensions are allowed **only if they do not break existing tests** and do not violate these invariants:

- Additional read models may be added alongside existing ones.
- New comparative dimensions must preserve per-period isolation.
- Performance optimizations must not change observable output.
- Any new behavior **must be locked by tests first**.

Breaking any invariant above requires:
- New tests
- Explicit architectural review
- Versioned contract change

---

project repository link: [https://github.com/Reltroner/finance-reltroner](https://github.com/Reltroner/finance-reltroner)

---

## Final Statement

This finance core read model is **test-defined, immutable, and audit-ready**.

Tests are not supporting artifacts.  
**Tests are the system.**
