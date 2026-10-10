# LMS Phase 4B-02 — E41 Actual SQL Transaction Supplement (SQLite, NOT PostgreSQL 18)

> **Evidence:** `LMS-P4B02-E41-20261011`, local isolated engineering proof executed by assistant.  
> **Status:** `SQLITE_LOCAL_TRANSACTION_MODEL_8_OF_8_PASS`; `POSTGRESQL18_REAL_TEST_NOT_RUN`; `REDIS8_REAL_TEST_NOT_RUN`; `KEYCLOAK_NOT_ACCESSED`; `RATIFICATION_HOLD`.  
> **Parent:** [E40 replay/dual JWS feasibility](./phase4b-02-e40-d02-01-dual-assertion-and-d02-02-replay-integrity-feasibility-proof-20261011.md), [E40 owner choice](./phase4b-02-e40-owner-design-decision-d02-01-to-d02-05-and-ratification-reassessment-20261011.md), [E39 16-risk register](./phase4b-02-e39-pre-ratification-assurance-risk-register-20261011.md).

## 1. Why this supplementary experiment?

E40's independent durable anti-replay journal ran using an OS-locked temporary JSON file. That proved a limited **model**, not transactional database semantics. E41 executes the **real SQLite3 SQL engine** included with Python, in a disposable temporary directory, to test atomic insert, uniqueness and process crash behavior before owner decides whether a **material ADR change** to existing PostgreSQL18 service-owned DBs is worth engineering effort. **SQLite is NOT PostgreSQL** and lacks its identical WAL durability, replication, isolation, locks, ACLs and operational behavior. This supplement cannot close live PG18/Redis8 gates.

## 2. Actual observed execution, isolated container

Eight Python 3.13 standard-library sqlite3 test cases ran successfully. No network, Redis, PostgreSQL, Keycloak, VPS, Cloudflare or production access. A temporary SQLite file was deleted after the test, with no LMS application repository modification or signing-key provision.

| Case | Real SQLite experiment | Observed |
|---|---|---|
| `SQL-001` | Two JWS role nonces inserted together within a SQL transaction | PASS |
| `SQL-002` | Reused nonce rejected by composite unique primary key | PASS |
| `SQL-003` | Second nonce conflicts; first partial insertion rolled back; unclaimed nonce still available | PASS |
| `SQL-004` | **Simulated** Redis flush does not remove committed nonce in independent SQLite DB | PASS |
| `SQL-005` | Close and reopen SQLite DB; committed nonce still prevents replay | PASS |
| `SQL-006` | Two actual operating-system subprocesses race for identical nonce pair | PASS: **one succeeds, one denied** |
| `SQL-007` | Child process exits before COMMIT with open transaction; SQLite rolls it back | PASS |
| `SQL-008` | Authoritative SQL file unavailable | PASS: fail-closed in test |

```text
SQL_SUMMARY total=8 passed=8 failed=0
SQL_ENGINE=SQLITE3_ACTUAL_TRANSACTIONS_NOT_POSTGRESQL18
LIVE_REDIS_SERVER_ACCESSED=NO
LIVE_POSTGRES_SERVER_ACCESSED=NO
LIVE_KEYCLOAK_ACCESSED=NO
PRODUCTION_ACCESS=NO
PG18_REPLICA_FAILOVER_AND_WAL_PROOF=NOT_PERFORMED
```

**Reproducibility:** The original conversation includes the final five-file `LMS-P4B02-D02-D01-ISOLATED-PROOF-20261011.zip` (**ZIP SHA256 `7C06EBE907102C6B01CD939FEE3124363620581444CB24D3D9C5601BE5DFABE3`**), containing a cross-platform 30-case PHP/Sodium proof plus optional **`sql_ledger_proof.py`** and `run-sql-proof-ps51.ps1`. The Python file SHA256 is `A6BEAA88238F7C31D49268FA049BAD6928162444B31AC51A667440241F872859`. Python 3 is OPTIONAL on the Windows operator host; absence means E41 `NOT_RUN_ON_USER_HOST` and does not negate the assistant's actual 8/8 execution. **The ZIP is a separate chat artifact, not already a GitHub repo file.**

## 3. What this verifies and what remains blocked

**Proven under test conditions:** SQLite's actual SQL transaction plus unique index can prevent a duplicate pair even after a simulated volatile cache loss. It keeps committed entries across closing/reopening a local DB and denies concurrent duplicate inserts; uncommitted data is rolled back on worker crash.

**NOT PROVEN:** Any *real* Redis8 eviction/flush/restart, PostgreSQL18 `INSERT ON CONFLICT` transaction and WAL durability, acknowledged-commit loss on async standby failover, multi-owner PostgreSQL tenant/resource authority, cleanup retention under skew and clock failure, performance on a shared 1vCPU server, business/idempotency transaction integration, HTTP provider behavior or authorized/unauthorized user token handling.

**D02-02 result stays** `REDIS_ONLY_UNSAFE_COUNTEREXAMPLE` / `DURABLE_ATOMIC_LEDGER_SQLITE_ENGINE_PASS` / **`PG18_REDIS8_ISOLATED_RUNTIME_NOT_EXECUTED`**. Owner-approved **ADR-LMS-TRUST-002 candidate** and actual isolated PG18 + Redis8 tests remain required; no fifth database or production access. Additional SQL engine tests reduce uncertainty, **not** the absolute possibility of silent rollback, DBA tampering or data loss on real failover.

## 4. Ratification / permission status

`D02-01=17/17_REAL_ED25519_MODEL_PASS_OWNER_WIRE_PENDING`; `D02-02=13/13_REPLAY_MODEL_PASS_WITH_UNSAFE_REDIS_ONLY_COUNTEREXAMPLE + 8/8_ACTUAL_SQLITE_SQL_PASS; PG18_REDIS8_REQUIRED`; `D02-03=PROPOSED_NOT_RATIFIED`; `D02-04=ISOLATED_KEY_SIMULATION_PASS_REAL_SERVER_CUSTODY_PENDING`; `D02-05=KEYCLOAK_ALG_NOT_VERIFIED`.

**Gate remains:** `PHASE4B02_DESIGN_RATIFICATION=HOLD`; `T02_REAL_HTTP=0_OF_86_EXECUTED`; `BE_SOURCE_CODING=NOT_AUTHORIZED`; `PRODUCTION=NOT_AUTHORIZED`.

**Next:** Owner reviews material ADR direction; only after scoped permission run disposable real PG18 and Redis8 under explicit isolation to test unique constraints, WAL crash, negative replay store loss, owner-specific grants, concurrency and latency. No production credentials or Redis DB index should be accessed.
