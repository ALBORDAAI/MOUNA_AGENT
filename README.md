<div align="center">

<img src="MOUNA.png" alt="MOUNA — AI Executive Assistant" width="220">

# MOUNA
### The AI Executive Assistant, Native to Hassaniya

**Status:** 🟢 In Production &nbsp;·&nbsp; **Version:** 1.0 &nbsp;·&nbsp; **Built by** [Alborda AI](https://alborda.ai)

</div>

---

## 1. What is MOUNA?

**MOUNA** is Alborda AI's executive assistant product: an AI that manages the daily operational load of running a business — inbox, calendar, documents, meeting notes — and, for client-facing businesses, part of the client relationship as well.

Unlike generic international assistants (Notion AI, Google Workspace add-ons) that treat Hassaniya as an afterthought, MOUNA is powered by **Dimeyz**, Alborda's proprietary large language model natively trained on **Hassaniya Arabic**, paired with **Dimeyz Speech** for transcription.

MOUNA is not a bespoke integration rebuilt per client. It is a **configurable product**: every user or organization runs on the same core engine, with individual integrations, permissions, and feature flags — no forked codebases, no per-client maintenance debt.

**Who it's for:** executives, SMEs, and independent professionals (lawyers, doctors, consultants) in Mauritania who need their inbox, calendar, and documents handled — without losing control over what actually gets sent or filed.

**Guiding principle:** *MOUNA prepares. You decide.* No irreversible action is taken without explicit human validation on sensitive tasks.

---

## 2. Why MOUNA is different

| # | Differentiator | What it means in practice |
|---|---|---|
| 01 | **Native Hassaniya** | Draft emails, summaries, and meeting notes are generated directly in Hassaniya by Dimeyz — not translated from French or English. |
| 02 | **Human-in-the-loop by default** | Every draft, every filed document, every scheduled action is reversible and requires validation before it takes effect externally. |
| 03 | **Multilingual meeting transcription** | Detects and follows Hassaniya, Arabic, and French — including mid-meeting language switching — without manual language selection. |
| 04 | **Local business logic** | Quotes, invoices, and administrative paperwork (tax filings, CNSS renewals) are built around Mauritanian formalities, not adapted from generic templates. |
| 05 | **Mobile money integration** | Payment requests and reconciliation via Bankily, Masrvi, and Sedad — reusing the same integration already proven in SIDI. |
| 06 | **Confidentiality-first mode** | An enhanced privacy configuration for regulated professions (lawyers, doctors) with no extended content retention. |
| 07 | **Data sovereignty** | No third-party retention beyond what's strictly required by connected APIs (Gmail, Drive, Calendar). Meeting transcription is processed internally via Dimeyz Speech. |

---

## 3. How it works — architecture overview

```
                    ┌──────────────────────────────────────────┐
                    │   User data sources                        │
                    │   Gmail/Outlook · Calendar · Drive ·         │
                    │   CRM · Meeting platforms (Zoom/Meet/Teams)  │
                    └───────────────────┬─────────────────────────┘
                                        │
                              Agentic Orchestration Layer
                    · Email classification & prioritization
                    · Draft generation (never sent directly)
                    · Human-in-the-loop action detection
                                        │
                ┌───────────────────────┼───────────────────────────┐
                ▼                       ▼                           ▼
     ┌────────────────────┐  ┌─────────────────────┐  ┌───────────────────────┐
     │  Dimeyz (LLM)        │  │  Dimeyz Speech        │  │  Connectors             │
     │  served via vLLM      │  │  Meeting transcription │  │  Gmail · Calendar ·     │
     │  + LiteLLM             │  │  Hassaniya/AR/FR       │  │  Drive · CRM · Video    │
     └──────────┬───────────┘  └──────────┬────────────┘  └────────────┬────────────┘
                │                          │                            │
                └──────────────┬───────────┴────────────────────────────┘
                               ▼
                    ┌───────────────────────────────┐
                    │  Knowledge Base (RAG)             │
                    │  · Product/service catalog (Pro)  │
                    │  · Sorting history & preferences  │
                    └───────────────┬───────────────────┘
                                    ▼
                    ┌───────────────────────────────┐
                    │  Database — self-hosted Supabase  │
                    │  Contacts · pending actions ·       │
                    │  history                            │
                    └───────────────┬───────────────────┘
                                    ▼
                    ┌───────────────────────────────┐
                    │  Interface — dashboard +           │
                    │  validation queue                   │
                    └───────────────────────────────┘
```

Every stage stays decoupled: connectors know nothing about the LLM, the orchestration layer knows nothing about the underlying channel, and every generated action — a draft, a filed document, a CRM entry — sits in a validation queue before it becomes real.

---

## 4. Core components

| Component | Role |
|---|---|
| **Dimeyz** | Proprietary LLM natively trained on Hassaniya Arabic. Generates drafts, summaries, and meeting notes. |
| **Dimeyz Speech** | Transcription engine for meetings, with automatic language detection across Hassaniya, Arabic, and French. |
| **Connectors** | OAuth-scoped integrations with Gmail, Google Calendar, Google Drive, CRM, and video conferencing platforms. |
| **Orchestration Layer** | Classifies emails, drafts responses, detects actions requiring validation, never triggers irreversible actions alone. |
| **RAG Layer** | Grounds client-facing responses (Pro tier) in the user's own product/service knowledge base. |
| **Supabase (self-hosted)** | Stores contacts, pending validations, documents, meeting records, and audit history. |
| **Dashboard & Validation Queue** | The single interface where the user reviews and approves everything MOUNA prepares. |

---

## 5. What MOUNA does for you

- **Inbox, handled** — priority and category classification, with redirection suggestions for team accounts.
- **Draft replies, never sent without you** — generated in Hassaniya, Arabic, or French, matching tone to context.
- **Daily & weekly briefings** — short, decision-focused, not exhaustive lists.
- **Smarter contact management** — new contacts detected and enriched, validated before entering the CRM.
- **Organized documents** — automatic Drive sorting and duplicate detection, within existing permissions only.
- **Meeting transcription & summaries** — key points, decisions, and action items with assigned owners.
- **Client relationship support** *(Pro)* — automated client responses and appointment scheduling with real-time availability checks.

---

## 6. Plans & feature flags

| Plan | For | Includes |
|---|---|---|
| **Solo** | Individual executives & professionals | Email, calendar, documents, briefings |
| **Pro** | Client-facing businesses | Everything in Solo + client advisory & external appointment scheduling |
| **Team** | Growing SMEs | Everything in Pro + internal directory & email routing between team members |

Feature flags are modeled per user/organization at the data layer, reusing the same subscription architecture as SIDI and SOULEYMAN — every tenant runs the same core, regardless of plan.

---

## 7. Data & security principles

- **Human validation by default.** No email is sent, no document permanently modified or deleted, without explicit user approval — except in narrowly scoped, documented auto-response cases.
- **OAuth everywhere, least privilege.** No password storage; access scopes limited to what each feature strictly requires.
- **Encryption at rest** for all stored emails, documents, and transcriptions.
- **Full audit trail** of every action taken by MOUNA on the user's behalf.
- **Confidentiality-first mode** for regulated professions, with no extended content retention after summary generation.
- **Strict data isolation** per user and per organization — no cross-visibility without explicit authorization, even via AI suggestion.

---

## 8. Roadmap highlights

- Voice dictation for emails once Dimeyz Speech TTS/ASR is bidirectionally mature
- Proactive deadline and follow-up alerts from detected commitments in email threads
- Automatic meeting preparation briefs from CRM and email history
- Automated quotes & invoices with local tax handling and mobile money reconciliation
- Administrative assistant for Mauritanian SME formalities (tax filings, CNSS renewals)
- Self-service client portal for appointment and document access
- Multilingual document translation and review (Hassaniya, Arabic, French, English)

---

## 9. About Alborda AI

Founded in 2024 in Mauritania, Alborda AI is an international AI company democratizing artificial intelligence for underrepresented languages across the Middle East and North Africa (MENA). We develop language models and personalize them for a wide range of tasks, so millions can access advanced AI natively — in their own language, not a borrowed one.

**Products:** Dimeyz (LLM) · SIDI (B2B support agent) · MOUNA (executive assistant) · SOULEYMAN (AI tutor) · Dimeyz Chat (consumer chat)

---

## 10. Contact

📧 [contact@alborda.ai](mailto:contact@alborda.ai)
🌐 [alborda.ai](https://alborda.ai)

---

<div align="center">
<sub>© 2026 Alborda AI — Building AI that speaks your language.</sub>
</div>
