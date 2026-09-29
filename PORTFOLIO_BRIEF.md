# RetailRAG — Portfolio Integration Brief

## Project Identity

```text
Project: RetailRAG
Version: 1.0
Type: AI Automation / RAG Decision-Support System
Context: UrbanStitch Clothing Co. (fictional)
Status: Completed and frozen
```

---

## Purpose of This File

This file is the starting point for any portfolio or presentation work involving RetailRAG.

The GitHub repository is the technical source of truth.

Do not invent project capabilities, metrics, integrations, or technical claims that are not supported by this repository.

For deeper implementation details, refer to:

```text
README.md
PRODUCT.md
DESIGN.md
M9_VERIFICATION.md
M10_VERIFICATION.md
```

---

# Portfolio Positioning

RetailRAG should NOT be presented as:

```text
"an AI chatbot"
```

The stronger and more accurate positioning is:

> A production-style RAG decision-support system that retrieves internal policy knowledge, generates grounded operational recommendations, validates AI output, enforces deterministic security controls, and handles failures safely.

The main value of the project is the system architecture surrounding the LLM.

---

# Short Project Description

RetailRAG is an internal operations decision-support system built in n8n for a fictional retail company.

It uses Retrieval-Augmented Generation to answer operational questions from authorized company policies while enforcing active-policy boundaries, deterministic security rules, citation validation, evidence-quality checks, evaluation testing, production logging, and graceful failure handling.

---

# Problem

Retail employees may need answers to questions such as:

```text
What is the current return window?

Who approves a ₱32,000 refund?

Which policy applies to this case?

What should happen when required evidence is missing?

Can archived policies override the current policy?
```

A normal LLM can create several risks:

```text
hallucinated policies
invented thresholds
unsupported citations
outdated policy usage
prompt injection
authorization bypass
guessing live operational data
```

RetailRAG was designed to reduce those risks.

---

# Core Architecture

RetailRAG consists of four n8n workflows.

## Main Decision System

Handles:

```text
authenticated webhook
input validation
security controls
knowledge retrieval
evidence construction
LLM generation
structured output
grounding validation
runtime routing
failure handling
logging
production response
```

## Knowledge Retrieval

Handles:

```text
knowledge-scope enforcement
metadata filtering
Gemini embeddings
Supabase vector search
Top-K retrieval
```

## Knowledge Ingestion

Handles:

```text
Google Drive documents
text extraction
metadata parsing
chunking
embeddings
Supabase vector ingestion
```

## Run Logging

Handles:

```text
SUCCESS
DENIED
ERROR
```

production execution summaries.

---

# Main Engineering Highlights

Emphasize these in the portfolio case study.

### Retrieval-Augmented Generation

```text
Google Gemini embeddings
Supabase vector store
Top-K semantic retrieval
metadata filtering
```

### Trusted Knowledge Boundary

Production hardcodes:

```text
knowledge_scope = current_only
```

Employee input cannot change this trusted value.

### Active Policy Enforcement

Current operational questions use active knowledge rather than archived policy versions.

### Structured AI Output

The model returns a defined schema instead of unrestricted chatbot text.

### Grounding & Citation Validation

The workflow verifies:

```text
source document IDs
evidence ranks
retrieved documents
citation validity
evidence status
missing evidence
```

Final citations are reconstructed from retrieved evidence instead of blindly trusting model-generated citations.

### Evidence Quality

RetailRAG classifies evidence as:

```text
SUFFICIENT
PARTIAL
INSUFFICIENT
```

The system is designed to abstain when the available knowledge cannot safely answer the request.

### Live Data Boundary

Static policy retrieval is not treated as live operational data.

Requests requiring:

```text
current order location
live tracking
inventory
account status
```

must use an appropriate live system rather than being guessed from RAG documents.

### Deterministic Security Controls

Requests involving:

```text
credentials
passwords
secret keys
authorization bypass
approval bypass
```

can be blocked before knowledge retrieval.

### Prompt Injection Resistance

Employee text cannot modify:

```text
knowledge scope
permissions
system instructions
approval rules
active-policy precedence
```

Retrieved document content is also treated as untrusted data rather than system instructions.

### Graceful Failure Handling

RetailRAG defines controlled behavior for:

```text
HTTP 400 — invalid input
HTTP 502 — AI output validation failure
HTTP 503 — AI service unavailable
HTTP 503 — knowledge retrieval unavailable
```

### Observability

Production executions are recorded with:

```text
run ID
timestamp
outcome
case type
security decision
evidence status
source IDs
validation result
error code
```

---

# Evaluation Results

RetailRAG has a repeatable evaluation dataset.

Final result:

```text
7 / 7 evaluation cases passed
```

Evaluation includes:

```text
policy retrieval
multi-document reasoning
refund approval
live-data boundary
credential security
authorization bypass
knowledge-scope injection
```

Evaluation checks:

```text
source coverage
evidence status
security decision
expected answer content
grounding validity
```

---

# Production Regression

The final production regression suite passed:

```text
PR-00 Authentication protection       PASS
PR-01 Invalid input                   PASS
PR-02 Current return policy           PASS
PR-03 Refund approval                 PASS
PR-04 Live-data boundary              PASS
PR-05 Credential request              PASS
PR-06 Authorization bypass            PASS
PR-07 Knowledge-scope injection       PASS
```

Final result:

```text
8 / 8 PASS
```

Additional failure paths tested:

```text
AI output validation failure   PASS
AI service unavailable         PASS
Knowledge retrieval failure    PASS
```

---

# Production Verification

The production webhook was tested using:

```text
POST /webhook/retailrag
```

A valid policy request returned:

```text
HTTP 200
SUCCESS
ALLOW
SUFFICIENT
validated = true
```

A restricted credential request returned:

```text
HTTP 200
DENIED
DENY
validated = true
```

The production webhook uses Header Authentication.

---

# Tech Stack

```text
n8n
Supabase
Google Gemini Embeddings
Groq
GPT-OSS
Google Drive
Postman
Git
GitHub
```

---

# Screenshot Guide

Portfolio implementations should use the images inside:

```text
/screenshots
```

## 01-main-workflow.png

Use for:

```text
hero architecture
system overview
workflow complexity
```

Shows the complete RetailRAG orchestration including:

```text
manual execution
evaluation
production webhook
security
retrieval
generation
validation
failure paths
logging
production response
```

---

## 02-retrieval-workflow.png

Use for:

```text
RAG architecture
retrieval explanation
knowledge boundary section
```

Shows:

```text
Resolve Knowledge Boundary
Gemini Embeddings
Supabase Retrieve Knowledge
```

---

## 03-ingestion-workflow.png

Use for:

```text
knowledge ingestion section
RAG pipeline explanation
```

Shows:

```text
Google Drive
file download
Markdown extraction
metadata parsing
chunking
Gemini embeddings
Supabase vector storage
```

---

## 04A-evaluation-results.png

Use for:

```text
evaluation design
expected test cases
```

Shows the seven evaluation cases and their expected:

```text
sources
evidence status
security behavior
answer content
```

---

## 04B-evaluation-results.png

Use together with `04A`.

Shows the actual evaluation output:

```text
actual sources
actual evidence status
actual security decision
test_pass
failure_reasons
grounding_valid
```

This is the main proof for:

```text
7 / 7 evaluation cases passed
```

---

## 05-production-success.png

Use for:

```text
production proof
grounded response example
```

Shows:

```text
production webhook
HTTP 200
SUCCESS
ALLOW
SUFFICIENT
DOC-001 citation
validated = true
```

---

## 06-security-denial.png

Use for:

```text
security section
deterministic controls
```

Shows a credential request being safely returned as:

```text
DENIED
DENY
Restricted Request
credential_or_secret_request
citations = []
validated = true
```

---

## 07-run-logging.png

Use for:

```text
observability
production reliability
```

Shows multiple logged outcomes including:

```text
SUCCESS
DENIED
ERROR
AI_SERVICE_UNAVAILABLE
AI_OUTPUT_VALIDATION_FAILED
```

---

# Recommended Portfolio Case Study Structure

The portfolio case study should remain significantly shorter than the GitHub technical documentation.

Recommended structure:

```text
Hero
↓
Problem
↓
What I Built
↓
Architecture
↓
How RAG Works
↓
Security & Grounding
↓
Evaluation & Reliability
↓
Production Results
↓
What I Learned
↓
GitHub CTA
```

---

# Suggested Hero Copy

## Title

```text
RetailRAG
```

## Subtitle

```text
A production-style RAG decision-support system for reliable retail operations.
```

## Short Description

RetailRAG retrieves authorized company knowledge, generates grounded operational recommendations, validates AI-created evidence and citations, blocks restricted requests, and fails safely when the system does not have enough trusted information.

---

# Suggested Project Card Copy

## Title

```text
RetailRAG
```

## Description

```text
A production-style RAG system with grounded retrieval, security controls, automated evaluation, citation validation, and operational observability.
```

## Tags

Suggested:

```text
n8n
RAG
Supabase
AI Automation
Gemini
```

Do not overload the project card with every technology used.

---

# What the Portfolio Should Emphasize

Prioritize:

```text
system architecture
reliability
RAG grounding
security boundaries
evaluation
failure handling
observability
```

Do not make the main story about:

```text
prompt engineering alone
calling an LLM
having many workflow nodes
using AI for everything
```

The strongest story is that RetailRAG treats AI as one controlled component inside a larger software system.

---

# Important Accuracy Rules

Do not claim that RetailRAG:

```text
automatically issues refunds
changes customer accounts
tracks real orders
accesses production UrbanStitch systems
uses a real retail company's data
is deployed for real customers
```

UrbanStitch Clothing Co. is fictional.

RetailRAG is a portfolio engineering system designed to demonstrate production-style AI automation architecture.

---

# Live Demo

Do not use the temporary ngrok endpoint as a public permanent live-demo link.

The production endpoint was used for verification but may change or become unavailable.

Use GitHub as the primary external technical link unless RetailRAG is later deployed to permanent infrastructure.

---

# Repository Role

The repository should remain the detailed technical source of truth.

Use:

```text
Portfolio
= concise story, visuals, outcomes

GitHub
= architecture, implementation, verification, technical proof
```

The portfolio should link to the GitHub repository for visitors who want deeper technical details.

---

# Release

```text
RetailRAG v1.0
Stable baseline
Evaluation: 7 / 7 PASS
Production regression: 8 / 8 PASS
Production webhook: verified
```
