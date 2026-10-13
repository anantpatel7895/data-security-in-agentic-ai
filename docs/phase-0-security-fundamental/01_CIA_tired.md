# Level 00 — Security Fundamentals

# 00.1 — CIA Triad

## Objective

Understand the three fundamental security objectives:

- Confidentiality
- Integrity
- Availability

And understand how they apply to Agentic AI systems.

---

# Q1. What is the CIA Triad?

The CIA Triad is a fundamental security model consisting of:

```text
C — Confidentiality
I — Integrity
A — Availability
```

It describes three primary goals of information security.

```text
Confidentiality → Who can SEE the data?
Integrity       → Who can CHANGE the data?
Availability    → Can the system be USED when needed?
```

---

# Q2. What is Confidentiality?

**Confidentiality means preventing unauthorized users, systems, or agents from accessing data.**

The goal is:

> Only authorized entities should be able to see or access the data.

### Example

Suppose a banking database contains:

```text
Account Number
Salary
Balance
Transaction History
```

User A should not be able to access User B's salary.

```text
User A
   |
   | Request User B's salary
   v
System
   |
   X
Unauthorized access
```

This is a **Confidentiality violation**.

---

# Q3. What is Confidentiality in Agentic AI?

Consider:

```text
User
  ↓
FastAPI
  ↓
Agent
  ↓
LLM
  ↓
Tool
  ↓
Database
```

Suppose the database contains:

```text
Account Number
Salary
Balance
Transactions
```

If the agent exposes User B's information to User A:

```text
User A
   ↓
Agent
   ↓
User B's salary
```

the system has violated **Confidentiality**.

### Key question

```text
Who is allowed to SEE this data?
```

---

# Q4. What is Integrity?

**Integrity means ensuring that data remains accurate, trustworthy, and is not modified by unauthorized entities.**

The goal is:

> Data should not be changed incorrectly or without authorization.

### Example

Original balance:

```text
Balance = ₹50,000
```

An attacker changes it to:

```text
Balance = ₹5,00,000
```

The data has been improperly modified.

This is an **Integrity violation**.

---

# Q5. What is Integrity in Agentic AI?

Suppose an agent has access to a banking tool:

```text
transfer_money(
    from_account,
    to_account,
    amount
)
```

The user requests:

```text
Transfer ₹1,000.
```

But the agent incorrectly or maliciously executes:

```text
Transfer ₹1,00,000.
```

The system state has been incorrectly modified.

This is an **Integrity problem**.

### Key question

```text
Who is allowed to CHANGE this data or system state?
```

---

# Q6. What is Availability?

**Availability means that authorized users and systems can access the service or data when required.**

The goal is:

> The system should remain usable when legitimate users need it.

### Example

```text
User
  ↓
API
  ↓
Database
```

If the database goes down:

```text
User
  ↓
API
  ↓
Database
  X
```

the user cannot access their data.

This is an **Availability problem**.

---

# Q7. What is Availability in Agentic AI?

Consider:

```text
User
  ↓
FastAPI
  ↓
Agent
  ↓
LLM
  ↓
Tool
  ↓
Database
```

An attacker may send a very large number of requests:

```text
Millions of requests
        ↓
     FastAPI
        ↓
      Agent
        ↓
       LLM
```

The system may become overloaded.

Legitimate users may no longer be able to use the service.

This is an **Availability violation**.

### Key question

```text
Can the authorized user use the system when needed?
```

---

# Q8. What is the difference between Confidentiality, Integrity, and Availability?

| Security Property | Main Question | Example |
|---|---|---|
| Confidentiality | Who can SEE? | User A sees User B's salary |
| Integrity | Who can CHANGE? | Balance changed without authorization |
| Availability | Can I USE it? | Database is unavailable |

### Easy mental model

```text
CONFIDENTIALITY → SEE
INTEGRITY       → CHANGE
AVAILABILITY    → USE
```

---

# Q9. Give an example involving a banking Agentic AI system.

System:

```text
User
  ↓
FastAPI
  ↓
Agent
  ↓
Tool
  ↓
Database
```

Database contains:

```text
Account Number
Transaction History
Salary
Balance
```

### Confidentiality violation

Agent exposes User B's transaction history to User A.

```text
Unauthorized READ
       ↓
Confidentiality violation
```

### Integrity violation

An attacker modifies a transaction record.

```text
Unauthorized WRITE
       ↓
Integrity violation
```

### Availability violation

The database server goes down and users cannot check their balance.

```text
Service unavailable
       ↓
Availability violation
```

---

# Q10. Classify the following situations.

## Situation 1

User A is able to see User B's salary.

### Answer

**Confidentiality**

Reason:

Unauthorized access to information occurred.

---

## Situation 2

The agent changes a customer's balance from ₹20,000 to ₹2,00,000 without authorization.

### Answer

**Integrity**

Reason:

The data was modified without authorization.

---

## Situation 3

The database server goes down and users cannot check their balance.

### Answer

**Availability**

Reason:

The system/resource is not available to authorized users.

---

## Situation 4

The agent exposes a customer's transaction history to an unauthorized user.

### Answer

**Confidentiality**

Reason:

Sensitive information was exposed to an unauthorized entity.

---

## Situation 5

An attacker modifies a transaction record.

### Answer

**Integrity**

Reason:

The transaction data was modified without authorization.

---

# Q11. Why is CIA important for Agentic AI?

Agentic AI systems are different from simple information-retrieval systems because agents can:

```text
READ data
   ↓
REASON about data
   ↓
CALL tools
   ↓
CHANGE real-world state
```

Therefore, security must consider both:

### Reading

```text
What data can the agent access?
```

This relates strongly to:

**Confidentiality**

### Writing / Actions

```text
What can the agent modify or execute?
```

This relates strongly to:

**Integrity**

### System operation

```text
Can users continue using the agent and its tools?
```

This relates strongly to:

**Availability**

---

# Q12. How does CIA connect to the rest of Security Foundations?

```text
                    CIA
                     |
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
Confidentiality   Integrity   Availability
       |             |             |
       ↓             ↓             ↓
Authentication   Authorization   Rate Limiting
Least Privilege  Tool Security   Resilience
Data Protection  Validation      Monitoring
```

Later concepts such as Authentication, Authorization, RBAC, ABAC, and Least Privilege help protect these security objectives.

---

# Q13. What is the simplest way to remember the CIA Triad?

```text
CONFIDENTIALITY
       ↓
   Who can SEE?

INTEGRITY
       ↓
  Who can CHANGE?

AVAILABILITY
       ↓
   Can I USE it?
```

---

# Key Takeaways

1. **Confidentiality** protects data from unauthorized access.
2. **Integrity** protects data and system state from unauthorized or incorrect modification.
3. **Availability** ensures authorized users can access the system when needed.
4. An Agentic AI system must protect all three.
5. Agent access to sensitive data is primarily a **Confidentiality** concern.
6. Agent ability to modify data or execute actions is primarily an **Integrity** concern.
7. Keeping the agent/API/tools/database operational is an **Availability** concern.

---

# Progress

- [x] Confidentiality understood
- [x] Integrity understood
- [x] Availability understood
- [x] CIA differences understood
- [x] Agentic AI examples understood
- [x] Security scenarios classified

**Status: 00.1 CIA Triad — COMPLETE**