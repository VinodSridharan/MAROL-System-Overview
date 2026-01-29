# MAROL Technical Deep Dive (v2.3.0-alpha.1)

## Executive Summary

MAROL (Multi-Agent Reasoning Orchestration Lab) is a production-ready RAG console that lets you upload real-world content—documents, emails, long-form video/audio—and get grounded answers with clickable evidence. It is designed as an **Answer Guru** for complex technical and operational questions, not a toy chatbot.

Version **v2.3.0-alpha.1** is deployed on Google Cloud Run with a tiered access model (Demo, Evaluation, Collaborator) and a focus on three things: **multimodal ingestion**, **multi-agent orchestration**, and **strong grounding with safety**. It exists to demonstrate what modern RAG systems should look like in production: observable, predictable, and respectful of data boundaries.

MAROL is aimed at **AI/ML leads, knowledge-management owners, and hiring managers** who need both a credible demo and a blueprint for their own systems. It is intentionally transparent at the architecture level and intentionally opaque at the “secret sauce” level: you can see how it works, but not copy-paste it.

---

## Architecture at a Glance

At a high level, MAROL has four main layers:

1. **Browser Console** – a thin web UI for file attach, YouTube/audio links, and conversational Q&A with evidence.  
2. **Application API** – a FastAPI-based service orchestrating agents and enforcing tier/session rules.  
3. **Orchestration & RAG Layer** – multi-agent workflows (powered by LangGraph patterns) that coordinate ingestion, retrieval, and answer synthesis over vectorized content.  
4. **Data & Storage Layer** – Supabase Postgres with pgvector for embeddings, plus storage for uploaded files and transcripts.[cite:13][cite:39]

Requests flow like this:

- Users upload a file, drop a YouTube URL, or ask a question in the console.  
- The API layer invokes the right ingestion or query pipeline, guided by a router agent.  
- Ingested content is normalized, chunked, embedded, and stored with metadata in Supabase/pgvector.[cite:13]  
- Query-time agents retrieve relevant chunks, synthesize an answer, and attach evidence snippets for inspection.  
- Session and tier metadata are checked on every request so Demo/Evaluation/Collaborator limits are respected.

### Core Design Principles

- **Multi-agent by default** – work is split into ingestion agents, router agents, safety/guardrail agents, and answer refinement agents.  
- **Grounding first** – evidence chips and “I don’t know” responses are treated as features, not failures.  
- **Tier-aware** – every session knows what it is allowed to do, with different experiences for Demo vs Evaluation vs Collaborator.  
- **Cloud-native** – the system is containerized and deployed on **Google Cloud Run**, connected to **Supabase** for storage and vector search.[cite:4][cite:10][cite:13]

---

## Key Capabilities

### File Attach: The 30-Second “Aha” Path

The primary entry point into MAROL is a **file attach demo**. A user uploads a single PDF, DOCX, or image and, within seconds, sees:

- A concise summary of the document.  
- Five curated questions that highlight important aspects of the file.  
- Answers with **evidence badges** that link directly to the relevant text snippets.[cite:39]

This flow simulates what a real team would do during an incident review, design walkthrough, or documentation audit. It is engineered to be understandable by non-experts while still interesting to senior engineers and architects.

### YouTube & Audio with Whisper

MAROL can ingest **YouTube videos and audio files** and turn them into searchable, explainable knowledge:

- Downloads or accepts the audio.  
- Transcribes it using a Whisper-based pipeline.  
- Segments the transcript and embeds it for retrieval.  
- Routes questions through the same RAG engine used for documents.[cite:4]

A flagship demonstration is a **Gen AI concepts talk delivered in Tamil**, where MAROL correctly answers questions about the video in English or Tamil and shows exactly which transcript segments it relied on.[cite:4][cite:39]

### Multilingual Retrieval

Because transcripts and documents are stored as text with embeddings, MAROL naturally supports **multilingual retrieval**:

- Questions and sources can be in different languages (e.g., Tamil transcript, English questions).  
- The grounding layer ensures that the model is answering based on what was actually said or written, not on generic training data.  

This is particularly compelling for global organizations with multilingual documentation and training content.

### Tiered Access: Demo, Evaluation, Collaborator

MAROL v2.3 introduces a **tier system**:

- **Demo** – 1 file and 5 questions per session, enough for an interview or quick walkthrough.  
- **Evaluation** – higher limits and the ability to index a small, focused corpus (folders, email sets).  
- **Collaborator** – extended limits and deeper access to experimental agents and flows.[cite:1][cite:4]

Tiers are enforced by the backend using session identifiers (`marol_session_id`) and Supabase tables that track usage and tier per session. The goal is to make the experience generous enough to be useful and constrained enough to stay safe and predictable.

---

## Technical Innovation

### Multi-Agent Orchestration Beyond “Single Prompt” Apps

Most RAG demos are a thin wrapper around a single retrieval call. MAROL is built as a **multi-agent system**:

- A **Router agent** decides whether a query is best handled by:
  - **Research** – deeper, multi-hop reasoning over more context.  
  - **Direct** – quick answers for straightforward questions.  
  - **Perfection** – slower, more meticulous responses when stakes are high.  
- **Ingestion agents** manage the different content types:
  - Files (PDF/DOCX/images).  
  - YouTube/audio.  
  - Email archives (.eml).  
- A **Safety & Guardrails agent** coordinates checks on content, usage, and answer confidence before a response is finalized.[cite:13][cite:40]

This design is closer to how real teams work: different “specialists” handle different responsibilities, and the API orchestrates them into a coherent answer.

### Evidence-Badged Answers and Grounding

Every answer MAROL returns is accompanied by evidence chips that show:

- Which chunks were retrieved.  
- Where they came from in the original document or transcript.  
- How the system is grounding its claims.[cite:39]

This encourages healthy skepticism and makes MAROL suitable for use in **regulated or high-stakes environments**, where “because the model said so” is not an acceptable justification.

### Safety Harness with Multiple Checks

MAROL’s **safety harness** is implemented as a series of layered checks around each request:

- Tier limit checks (files and queries).  
- Input shape and size checks.  
- Basic content safety screening.  
- Grounding and confidence checks before emitting a strong answer.  
- Answer style guidance (prefer sourced, cautious language).  
- Fallback paths that allow the system to say “I don’t know” or request more context.

These checks are described at a policy level in the public repo (e.g., `SAFETY.md` and related docs) and are implemented in the orchestration layer so they are hard to bypass.[cite:29][cite:31][cite:38]

---

## Commercial Readiness

### Deployment and Operations

MAROL is deployed as a containerized application on **Google Cloud Run**, with the backend image built by **Cloud Build** and deployed as revisions that receive 100% of traffic when promoted.[cite:4][cite:10]

- **Runtime:** FastAPI application serving Web/API traffic.  
- **Data layer:** Supabase Postgres + pgvector for vector search and metadata.[cite:13]  
- **Sessions and tiers:** Managed via cookies and database tables keyed by session ID.  
- **Policies:** Public policy docs (acceptable use, security, privacy, retention) live in the repo and are kept in sync with behavior.[cite:29][cite:31][cite:38]

This gives evaluators confidence that MAROL is not just a prototype but a system that can be deployed, versioned, and rolled back in real environments.

### Production Metrics (Qualitative)

While detailed internal metrics are kept private, v2.3.0-alpha.1 is built and tested against:

- Realistic document and email corpora.  
- Non-English audio/video (Tamil) to validate multilingual behavior.  
- Conditions that stress ingestion, retrieval, and tier enforcement.

The result is a console that feels like a product, not a demo: errors are handled, limits are clearly communicated, and the system favors reliability over impressive but ungrounded outputs.

---

## Evaluation Invitation

MAROL is intentionally not a one-click, open-source product. It is a **reference implementation and evaluation console** for teams and organizations that:

- Want to see a serious RAG system in action, end to end.  
- Need to evaluate whether multi-agent RAG is the right pattern for their use cases.  
- Are considering hiring or collaborating with someone who can design and deliver systems like this.

### How to Evaluate MAROL

There are three common paths:

1. **Demo Tier (fastest)**  
   - Use the public console (when available) with the built-in demo corpus.  
   - Upload a single file and ask a handful of questions.  
   - Explore the Tamil YouTube example and email/folder samples.

2. **Evaluation Tier (your own data)**  
   - Share a small, carefully selected corpus (e.g., a project folder or anonymized email set).  
   - Run a time-boxed evaluation focusing on 10–20 representative questions.  
   - Discuss results, gaps, and next steps in a short debrief.

3. **Collaborator Tier (deep dive)**  
   - Schedule architecture reviews and code walkthroughs.  
   - Explore custom agents, retrieval strategies, or safety policies.  
   - Use MAROL as a sandbox for shaping your own production RAG roadmap.

### Getting in Touch

For evaluation access or collaboration discussions:

- Email: **vinod.sridharan@txvault.app**  
- LinkedIn: [https://linkedin.com/in/vinod-s-6a565b1b8](https://linkedin.com/in/vinod-s-6a565b1b8)  

Please include a brief description of your role, your organization, and what you want to learn from a MAROL evaluation. The goal is to make the time valuable for both sides: you get an honest look at a production-grade RAG system, and MAROL gets tested against realistic problems.

---
