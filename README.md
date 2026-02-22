# MAROL — Multi-Agent Reasoning Orchestration Lab

**Upload a file. Ask a question. Get grounded answers over your own data.**

MAROL is a production RAG console and portfolio artifact for hiring managers,
technical evaluators, and practitioners who want to see real multi-agent
system design — not a toy notebook.

<p align="center">
  <img src="screenshots/SkySwim200.png" alt="MAROL Logo" width="220" />
</p>

<p align="center">
  <a href="#try-it-in-30-seconds">
    <img src="https://img.shields.io/badge/demo-v2.3.0--alpha.1-blue"
         alt="Version"></a>
  <a href="#current-production-status">
    <img src="https://img.shields.io/badge/status-production-green"
         alt="Status"></a>
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/license-private-important"
         alt="License"></a>
  <a href="https://github.com/VinodSridharan/MAROL-System-Overview/stargazers">
    <img src="https://img.shields.io/github/stars/VinodSridharan/
         MAROL-System-Overview?style=social"
         alt="Stars"></a>
</p>

---

## Try It in 30 Seconds

1. Upload a single PDF, DOCX, or image.
2. MAROL summarizes it and generates five smart questions.
3. Click a question or ask your own.
4. Inspect the answer and its **evidence chips** — every claim
   points back to the source chunk.

![MAROL console with grounded answer and evidence chips](
screenshots/answer-with-evidence.png)

> **Start here.**
> Upload one document and ask three questions.
> Everything else — YouTube ingestion, tiered access,
> multi-agent routing — builds on that same grounded RAG core.

---

## Why MAROL

| | |
|---|---|
| **Grounded answers** | Every response cites the exact chunks it used. No confident hallucinations. |
| **Multi-modal ingestion** | PDFs, DOCX, images, YouTube URLs, audio files — one unified pipeline. |
| **Multi-agent routing** | Research, Direct, and Perfection modes chosen per query. |
| **Production-deployed** | Google Cloud Run + Supabase/pgvector. Real infrastructure, not a demo notebook. |
| **Tiered access** | Safe for live demos; deeper access available for evaluators and collaborators. |
| **Tamil YouTube proven** | Whisper-transcribed Gen AI explainer in Tamil with grounded English/Tamil Q&A. |

---

## System Architecture

```mermaid
flowchart TD
    User([Browser UI])
    API[FastAPI Backend\nGoogle Cloud Run]
    LG[LangGraph Orchestrator]
    Router{Router Agent}
    Ingest[Ingestion Layer]
    Files[File Parser\nPDF · DOCX · Image]
    YT[YouTube · Audio\nWhisper Transcription]
    Email[Email Parser\n.eml threads]
    RAG[RAG Pipeline]
    Embed[Embed + Chunk]
    VDB[(Supabase Postgres\n+ pgvector)]
    Synth[Answer Synthesis\n+ Evidence Chips]
    Safety[Safety Harness\n6 checks]

    User -->|HTTPS| API
    API --> LG
    LG --> Router
    Router -->|research / direct / perfection| RAG
    Router -->|new content| Ingest
    Ingest --> Files
    Ingest --> YT
    Ingest --> Email
    Files --> Embed
    YT --> Embed
    Email --> Embed
    Embed --> VDB
    RAG -->|hybrid retrieval| VDB
    VDB -->|top chunks| Synth
    Synth --> Safety
    Safety -->|grounded answer| User
Multi-Agent Routing
The Router Agent picks one of three modes per query:

Mode	When	What it does
Direct	Simple, well-scoped questions	Single retrieval pass, fast response
Research	Multi-hop or comparative questions	Multiple retrieval rounds, deeper reasoning
Perfection	High-stakes answers	Multiple passes, explicit evidence review
Routing depends on question complexity, tier, and live retrieval quality.

RAG Pipeline
flowchart LR
    In([Input\nFile · URL · Audio])
    Parse[Parse + Normalize]
    Chunk[Chunk with overlap]
    Embed[Compute embeddings\nOpenAI]
    Store[(Supabase pgvector)]
    Retrieve[Hybrid retrieval\nsemantic + keyword]
    Synth[Answer synthesis]
    Evidence[Evidence chips\nchunk citations]
    Out([Grounded answer])

    In --> Parse --> Chunk --> Embed --> Store
    Store --> Retrieve --> Synth --> Evidence --> Out
Ingestion
Normalize input (text, HTML, audio transcripts from Whisper).

Chunk with overlap, preserving semantic boundaries.

Store embeddings and metadata keyed by corpus_id and source_id.

Retrieval
Semantic similarity search via pgvector.

Optional keyword filters and per-session corpus isolation.

Tier limits enforced per query.

Synthesis
Combine top-k chunks into a grounded answer.

Attach clickable evidence snippets with source references.

Safety harness vetoes or softens when evidence is weak.

Safety Harness
Six checks run per request:

Tier limit — enforces file and query limits per session tier.

Input shape — rejects oversized or malformed inputs.

Content safety — screens for out-of-scope content.

Grounding — requires sufficient evidence before a confident answer.

Answer style — prefers sourced, transparent responses.

Fallback — returns "I don't know" when retrieval is weak.

Deployment
flowchart TD
    GCR[Google Cloud Run\nmarol-backend]
    CB[Cloud Build\nDockerfile + cloudbuild.yaml]
    IMG[Container Image\nCPU-only Python 3.11\n~190MB torch vs 858MB CUDA]
    SB[(Supabase Postgres\npgvector · sessions · tiers)]
    GCS[Google Cloud Storage\nuploaded files + artifacts]
    FE[Browser UI\nHTML · JS · evidence chips]

    FE -->|HTTPS| GCR
    CB --> IMG --> GCR
    GCR --> SB
    GCR --> GCS
Backend: Containerized FastAPI on Google Cloud Run.
CPU-only image: 5.88s cold start, 3.66s warm.

Database: Supabase Postgres with pgvector for
vector similarity search.

Storage: Google Cloud Storage for uploads and artifacts.

Build: Google Cloud Build — 8m 53s build time.

Access Tiers
Tier	Use case	Limits	What you get
Demo	Quick interviews, first look	1 file, 5 questions	File attach, Tamil YouTube sample, evidence answers
Evaluation	Test on your own data	Higher limits	Custom corpora, folder/email ingestion, Perfection mode
Collaborator	Deep technical review	Flexible	Architecture sessions, code-level review, all flows
Start in Demo. Move to Evaluation when you want to test your own data.
Collaborator is for deeper technical partnerships.

Tech Stack
Layer	Technology
Language	Python 3.11
Web framework	FastAPI
Orchestration	LangGraph multi-agent workflows
Deployment	Google Cloud Run
Database	Supabase Postgres
Vector search	pgvector
Object storage	Google Cloud Storage
Transcription	OpenAI Whisper
Embeddings + LLM	OpenAI (GPT-4o)
Frontend	Lightweight HTML + JS
Getting Started
This repository is a system overview and portfolio artifact, not a
one-click product. It documents the live MAROL deployment.

1. Try the Demo
When the public demo is open, a Demo URL will appear here.

Recommended flow:

Open the demo link.

Upload a single PDF.

Click one of the suggested questions.

Inspect the answer and its evidence chips.

Paste a YouTube URL and ask a question about the video.

If no demo URL is shown, the environment is restricted to
Evaluation and Collaborator tiers.

2. Request Access
To evaluate MAROL with your own data or explore collaboration,
email vinod.sridharan@txvault.app with:

Subject: MAROL Evaluation Request or MAROL Collaboration

Your role and team

Types of data you want to evaluate

What you want to learn

You will receive a short questionnaire, a proposed evaluation scope,
and a suggested timeline.

Documentation
File	Contents
README.md	This file — high-level overview
llms.txt	System manifest for LLMs and agents
CHANGELOG.md	Version history and capability changes
docs/ARCHITECTURE.md	Deeper technical design and data flow
screenshots/	Demo screenshots
Acknowledgments
Cole Medin (coleam00) — Early LangGraph RAG patterns that
influenced MAROL's multi-agent design.

LangChain / LangGraph — Foundational frameworks for agentic
orchestration.

Supabase — Open-source backend powering Postgres, pgvector,
and session management.

OpenAI — GPT-4o, Whisper, and embeddings APIs.

FastAPI — Fast, type-safe Python web framework.

Current Production Status
Field	Value
Version	v2.3.0-alpha.1
Deployed to	Google Cloud Run (backend)
Database	Supabase Postgres + pgvector
Last updated	February 22, 2026
Status	Production — demo and evaluation usage
Cold start	5.88s
Build time	8m 53s
<div align="center">
Built by Vinod Sridharan
Production-grade multi-agent RAG system design and LLM orchestration

![GitHub Stars](https://img.shields.io/github/stars/VinodSridharan/
MAROL-System-Overview?style=social)

Questions or collaboration?
Email vinod.sridharan@txvault.app · Connect on LinkedIn

</div> ```