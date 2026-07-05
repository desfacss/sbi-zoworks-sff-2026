# SBI SFF Deterministic AI Framework for Customer Acquisition

> **Zoworks.ai** — Deterministic, Multilingual AI for Instant Loan Origination and Enterprise Vertical Workflows
> 
> **Hackathon Submission:** SBI SFF 2026
> **Theme:** Agentic AI & Emerging Tech | **Problem:** Zero-Friction Customer Acquisition

### 🎥 Watch the Demo
You can view the full end-to-end sandbox demo video here:
**[Zoworks SBI SFF Demo (Google Drive)](https://drive.google.com/file/d/1COXxpRKNOyovN3GD3SnD6sipgIVRGvCq/view)**


## 🏆 Executive Summary
Zoworks.ai is an **Active System of Intelligence** designed to solve the financial sector's greatest operational fear regarding AI: *Hallucination, Drift, and Unpredictable Action*. For this hackathon, we have built a fully functional 5-layer pipeline that compiles raw banking compliance guidelines directly into runtime execution graphs for the MUDRA Loan Origination process. The entire engine can be deployed alongside existing core systems within days - working along with the existing SBI API's. Its also scalable for any process based on SOP or BPMN or DMN or any structured format that the bank already has or with our frontier engineer setting up the required processes, based on consultation with the SBI.

Standard LLM agents that "guess" the next step are an immediate compliance and regulatory failure in enterprise banking. **The Zoworks Moat** fundamentally restricts the LLM to the **Cognitive Interface Layer**—limiting its role strictly to real-time conversational translation and semantic slot-filling. The actual business logic, state mutations, and eligibility boundaries are explicitly executed by our proprietary **Active Deterministic Engine (ADE)** acting as the **Deterministic State Core**. 

**The result?** Bank-grade execution certainty, absolute auditability, and **Zero Drift**.

## 📖 The Problem: Inclusion for the Bharat Economy
High-intent MSME customers don't just fail to qualify—they are frequently excluded by rigid, legacy digital onboarding funnels.
* **Language & Interaction Friction:** Traditional automated text systems and rigid voice menus force users down unnatural keyword paths. True financial inclusion demands processing natural conversational speech in Hinglish, native Kannada, Tamil, and other regional dialects seamlessly.
* **On-Demand Small Business Urgency:** Small business owners require instant, low-latency clarity. Dense multi-page web forms and delayed manual back-office reviews lead to massive application drop-offs.
* **Slow Eligibility Cycles:** Legacy setups treat all incoming applications through a uniform, slow evaluation pipeline. The industry requires dynamic, real-time rule execution—instantly auto-approving qualified micro-loans while securely routing complex files for human verification.

---

## 🏗 Architectural Blueprint (The 5-Layer Stack)

Our five-layer stack compiles standard bank documents (SOPs, BPMNs) directly into a live execution graph. 

*(Read our full [Architecture & E2E Process Whitebook](ARCHITECTURE.md) to see exactly how we route intents and execute state mutations across multiple banking workflows).*

```text
┌─────────────────────────────────────────┐
│              L0: SOURCES                │
│       OpenAPI, BPMN, Excel DMN          │
└────────────┬────────────────────────────┘
             │ Ingestion
             ▼
┌─────────────────────────────────────────┐
│           L1: ENTITY SCHEMA             │
│       external.loan_application         │
│         (Auto-tokenised PII)            │
└────────────┬────────────────────────────┘
             │ Binding
             ▼
┌─────────────────────────────────────────┐
│             L2: STATE CORE              │
│      Deterministic Engine Lifecycle     │
└────────────┬────────────────────────────┘
             │ Routing
             ▼
┌─────────────────────────────────────────┐
│         L3: DECISIONS + AGENTS          │
│      Structured Decision Registry       │
└────────────┬────────────────────────────┘
             │ Execution
             ▼
┌─────────────────────────────────────────┐
│             L4: TOOLS (MCP)             │
│        Secure Sandboxed Gateways        │
└─────────────────────────────────────────┘
```

### ⚡ Deep Technical Maturity (Production Architecture)

We bypass superficial AI wrappers and utilize deep enterprise integration components:

* **Client & Local Sync:** Highly optimized, ultra-low latency modular front-end orchestration layer.
* **Active Deterministic Engine (ADE):** Relational engine acting as the absolute Deterministic State Core with row-level data boundaries.
* **Cognitive Interface Layer:** Advanced parameter extraction and language localization framework.
* **API Routing:** Model Context Protocol (MCP) for secure, sandboxed external API gateway routing.
* **Governance:** SCIM 2.0 corporate identity provisioning, strict data protection law alignment, and hybrid search architectures.

---

## 🎛️ Zoworks Composer (The Bank Control Center)

How difficult is it for legacy bank IT departments to write ingestion parsers for their existing compliance systems? **Zero integration code is required on the bank's end.**

The **Zoworks Composer UI** is a dedicated administrative dashboard built for internal bank teams. If the bank already has OpenAPI 3.0 specs, BPMN 2.0 XML maps, or standardized Excel logic tables, compliance officers simply drag and drop them into the Composer. Our ingestion layer parses them natively and compiles them into active database-enforced workflow rules within days.

> **[ PLACEHOLDER: Insert screenshot of the Zoworks Composer (Deterministic Flow UI) dashboard here showing rule ingestion and FSM state mapping ]**

---

## 📸 Application Flow & Screenshots

*(Judges: See the screenshots below for the runtime view of the Deterministic Engine in action)*

### 1. Multilingual Voice Intake & Slot Filling

> **[ PLACEHOLDER: screenshot of the user interface showing Hindi voice note transcription and instant parameter extraction ]**
> *The customer requests a ₹3L loan via a Hindi voice note. The Cognitive Interface Layer instantly transcribes the audio, extracts `loan_amount`, and maps it to the internal entity schema.*

### 2. DMN Evaluation & Eligibility Check

> **[ PLACEHOLDER: screenshot of the Zoworks runtime showing the DMN decision table lighting up rule #4 for KISHORE tier ]**
> *Once the identity and turnover details are collected, the engine queries the Structured Decision Registry to calculate eligibility and automatically maps the applicant to the KISHORE tier.*

### 3. API Execution & Audit Trace

> **[ PLACEHOLDER: screenshot of the ADE trace log showing SUCCESS and HTTP 200 ]**
> *The engine confirms the validation requirements are satisfied and safely fires the standard gateway API call, completing the application in under 2.5 minutes with complete audit trails.*

---

## 📂 Executable Proof (The "Land & Expand" Specs)

To prove that our architecture scales universally across the entire financial institution, we have included the actual execution schemas for **four complete banking pipelines** in the `specs/` directory of this repository:

1. **MUDRA Loan Origination** (`01_mudra_...`)
2. **Fixed Deposit Opening** (`02_fd_...`)
3. **KYC Re-verification** (`03_kyc_...`)
4. **Savings Account Opening** (`04_savings_...`)

These schemas (rules within the Structured Decision Registry, workflow state machines, and API bindings) dictate the exact execution logic, completely removing the LLM from the decision-making loop.

---

## 🛡️ Strategic Risk Assessment (Q&A)

**Q1: How does Zoworks ensure that customer documents containing highly sensitive PII are not leaked during intermediate LLM inference steps?**
**A:** Our ingestion framework features an automated PII detector that intercepts input payloads before they hit public model endpoints. Sensitive identity markers and numbers are immediately tokenized into cryptographic mock values at the edge. Only clean, tokenized schemas pass through the Cognitive Interface Layer for slot-filling, keeping sensitive data within our secure perimeter.

**Q2: What happens if a user submits a blurred image, and how does your active correction loop avoid infinite agent loops?**
**A:** Our dedicated Vision Extraction Agent runs custom contrast calculations. If the document confidence score falls below our required threshold, the Deterministic State Core refuses to transition the workflow state and halts the pipeline. The user is prompted for a retake in their native language. If validation fails three consecutive times, the engine triggers a hard fallback to a live banking coordinator.

---

## 🚀 Sandbox Demo & Video Showcase

Since this is a public repository, we are sharing the deterministic configurations and API specs used for the SBI demo in the `specs/` directory instead of the full proprietary engine source code.

You can view the demo video here:
[Zoworks SBI SFF Demo (Google Drive)](https://drive.google.com/file/d/1COXxpRKNOyovN3GD3SnD6sipgIVRGvCq/view)

> **For the Live Presentation Stage:**
> When presenting to the panel, the demo showcases our recommended **split-screen layout**:
> * **Left Side:** The live user interaction (Customer speaking in a regional dialect).
> * **Right Side:** The scrolling live tracing log of the Active Deterministic Engine (watching the State Core execute transitions and evaluate the Structured Decision Registry in real-time).