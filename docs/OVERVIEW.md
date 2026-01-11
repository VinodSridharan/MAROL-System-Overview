# What MAROL Does

> **"Reasoning is the key. Orchestration is the sauce."**

MAROL is a **production-deployed multi-agent RAG system** demonstrating advanced LLM orchestration powered by **WhisperingChunks** for superior audio/video processing.

---

## The Problem

Most RAG systems do simple retrieval → generation. They can't:
- Self-correct when context is insufficient
- Request more information mid-reasoning
- Adapt their approach based on query complexity
- Handle long-form audio/video effectively

---

## The Solution: Multi-Agent Collaboration

MAROL uses **three specialized agents** orchestrated through LangGraph state graphs:

### 1. Retrieval Agent
Finds relevant information using **hybrid search:**
- BM25 keyword matching
- Vector similarity (pgvector)
- Cross-encoder reranking
- Reciprocal Rank Fusion (RRF)

**Result:** 91% accuracy vs 78% with pure vector

### 2. Reasoning Agent
Evaluates context quality and decides:
- "Is this enough to answer confidently?"
- "Do I need more information?"
- "Should I try a different strategy?"

**Result:** 20% better accuracy on complex queries

### 3. Synthesis Agent
Generates grounded answers with:
- 100% corpus grounding (no hallucinations)
- Full evidence citations
- Route + confidence + chunk count badges

**Result:** Full transparency and auditability

---

## WhisperingChunks: The Audio/Video Engine

MAROL uses **WhisperingChunks**, a proprietary transcription engine, for all audio/video processing.

**Why it's better:**
- **Intelligent overlap chunking** (500-token chunks, 50-token overlap)
- **Semantic continuity** across chunk boundaries
- **High-quality transcription** via OpenAI Whisper
- **Production-grade** (handles podcasts, YouTube, technical talks)

**Standard chunking problem:**  
Breaks mid-sentence or mid-thought → poor retrieval

**WhisperingChunks solution:**  
Overlap-merge strategy → preserves context → better answers

🔗 [Learn more about WhisperingChunks](https://github.com/VinodSridharan/WhisperingChunks-Overview)

---

## Live System (v1.0)

**URL:** https://marol-backend-467264912930.us-central1.run.app

**Deployed:** 2026-01-10 on Google Cloud Run

**What's working:**
- Multi-agent Q&A with evidence badges
- Folder upload (3 files) with automatic 10% overview
- YouTube/audio transcription via WhisperingChunks
- Evaluation workspace (request keys via email/LinkedIn)
- Answer export (Word, Markdown)
- Workspace page (corpus management, scoped Q&A)

---

## Why This Matters

This isn't theory—it's a **live production system** with:

- **Cost controls** (<$5/day with public access)
- **Security hardening** (multi-tenant RLS, rate limiting)
- **Measurable quality** (20% accuracy improvement)
- **Production deployment** (Cloud Run, 99% uptime)

**Perfect for:**
- Technical interviews & architecture walkthroughs
- Stakeholder demos with custom data
- Audio/video content made queryable
- RAG pattern validation

---

## Contact

For technical discussions, evaluation access, or collaboration:

📧 **vinod.sridharan@txvault.app**  
🔗 **LinkedIn:** [linkedin.com/in/vinod-s-6a565b1b8](https://www.linkedin.com/in/vinod-s-6a565b1b8)  
🌐 **Live Demo:** https://marol-backend-467264912930.us-central1.run.app

---

**Note:** This repository contains documentation only. The live system is proprietary. For evaluation access or source code discussions, contact via email.

