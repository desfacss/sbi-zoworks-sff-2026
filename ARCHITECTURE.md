# Zoworks Architecture & E2E Process Execution

This document provides a deep dive into the Zoworks.ai Deterministic Brain, demonstrating how standard enterprise documents and user interactions are ingested, compiled, and executed at runtime. 

Our "Land-and-Expand" model proves that the Zoworks platform is not a hardcoded script for a single pipeline, but a compounding operating system capable of running multiple complex business workflows concurrently.

---

## 🏗 The Architectural Flow

Zoworks operates in a strict, two-phase pipeline designed to enforce enterprise-grade compliance, manage state mutations safely, and entirely eliminate LLM hallucination.

```
USER (WhatsApp / Voice / Chat)
│
▼
┌─────────────────────────────────────────┐
│     Zo Supervisor Router Gateway        │
│  "need loan"      → finance_lead        │
│  "FD/deposit"     → banking_lead        │
│  "KYC/compliance" → compliance_lead     │
└────────────┬────────────────────────────┘
│ Ingests & Slot-Fills
▼
┌─────────────────────────────────────────┐
│        Transient Session State          │
│  (Validates PII & Tokenizes In-Memory)  │
└────────────┬────────────────────────────┘
│ Commits on Complete Data
▼
┌─────────────────────────────────────────┐
│     Persistent Engine Schema Layer      │
│  external.loan_application              │
│  banking.fixed_deposit                  │
│  banking.kyc_case                       │
└────────────┬────────────────────────────┘
│ Triggers Engine Lifecycle
▼
┌─────────────────────────────────────────┐
│   ACTIVE DETERMINISTIC ENGINE (ADE)     │
│       (Deterministic State Core)        │
└─────────────────────────────────────────┘
```

---

## 🔄 Live Use Cases (The "Land and Expand" Proof)

To demonstrate the structural versatility of the engine, the following four workflows are fully wired and functional. The raw configurations (OpenAPI, BPMN, DMN) for these processes reside in the `specs/` directory of this repository.

### 1. MUDRA Loan Origination
* **Business Case:** An MSME owner applies for a MUDRA loan via WhatsApp voice notes. The system collects required data, runs credit-based eligibility via a Decision Model and Notation (DMN) table, and submits data to the core banking API.
* **Entity Schema:** `external.loan_application`
* **ADE Flow:** `SUBMITTED` → `CREDIT_CHECK` → `ELIGIBILITY_EVALUATION` → `APPROVED / REJECTED`
* **Decision Logic (DMN):** Turnover less than ₹1L or credit metrics below baseline triggers immediate rejection; higher thresholds automatically slot applicants into SHISHU, KISHORE, or TARUN tiers.

### 2. Fixed Deposit Opening
* **Business Case:** A customer opens a Fixed Deposit. A DMN evaluates the applicable interest rate based on amount and tenure tiers, dynamically applying a 0.5% bonus for senior citizens.
* **Entity Schema:** `banking.fixed_deposit`
* **ADE Flow:** `FD_ENQUIRY` → `CUSTOMER_DETAILS` → `INTEREST_CALCULATION` → `MATURITY_PREVIEW` → `CONFIRMED`
* **Decision Logic (DMN - 9 Rules):** Automatically calculates interest rates ranging from 3.50% (short term) to 7.50% (bulk + senior).

### 3. KYC Re-verification (with Human-in-the-Loop)
* **Business Case:** Automated compliance scoring assigns a risk tier (LOW/MEDIUM/HIGH). HIGH-risk cases are escalated to a human compliance officer, while LOW/MEDIUM are auto-cleared.
* **Entity Schema:** `banking.kyc_case`
* **ADE Flow:** `KYC_INITIATED` → `DOCUMENT_COLLECTION` → `RISK_ASSESSMENT` → `(HIGH_RISK → OFFICER_REVIEW)` or `(LOW_MEDIUM → AUTO_CLEARED)`
* **Decision Logic (DMN):** Flags like PEP (Politically Exposed Person) and stale documents from risky jurisdictions trigger immediate HITL escalation.

### 4. Savings Account Opening
* **Business Case:** Occupation-based product routing (regular/jan-dhan/salary) and auto-assignment to the nearest physical branch.
* **Entity Schema:** `banking.savings_account`
* **ADE Flow:** `ENQUIRY` → `PERSONAL_DETAILS` → `DOCUMENT_VERIFICATION` → `PRODUCT_SELECTION` → `BRANCH_ASSIGNMENT` → `ACCOUNT_CREATED`
* **Decision Logic (DMN - 6 Rules):** Determines account tier (e.g., zero minimum balance for salaried/Jan-Dhan, ₹10K minimum for regular savings).

---

## 🛡️ Deterministic Execution vs. Chatbots Vs Pure LLM driven Flows

Legacy LLM "agents" rely on dynamic, open-ended prompting, making them highly unpredictable for core business execution. Zoworks ensures that **the LLM interface only interprets; the core architecture decides.**

* **The Cognitive Interface Layer:** Acts exclusively as an intake and translation framework. It processes natural language, handles localization, and extracts parameters into structured slot-filling schema variables.
* **The Deterministic State Core (ADE):** Functions as the ultimate operational source of truth. It strictly governs workflow mutations, enforcing hard data validation boundaries before allowing any process state to advance.
* **The Structured Decision Registry (DMN):** Executes core business rules (like interest rates or risk scoring) with mathematical certainty via isolated logic execution, guaranteeing zero hallucination.

