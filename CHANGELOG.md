# Changelog

All notable changes to MAROL will be documented in this file.

---

## [v1.0] - 2026-01-10

### 🚀 Initial Public Release

**Deployment:**
- Service: marol-backend-00004-lzp
- Platform: Google Cloud Run
- Status: ✅ Production
- URL: https://marol-backend-467264912930.us-central1.run.app

### ✨ Features

**Multi-Agent Orchestration**
- LangGraph state graphs with specialized agents
- Research Agent for complex queries
- Direct Answer Agent for factual questions
- Perfection Agent for definitions
- Automatic routing based on query type

**Retrieval & Search**
- Hybrid search (BM25 + vector + cross-encoder reranking)
- 91% accuracy vs 78% vector-only
- Supabase pgvector integration
- RRF fusion for result merging

**WhisperingChunks Integration**
- Audio/video transcription (YouTube, podcasts)
- Intelligent overlap-based chunking
- 500-token chunks with 50-token overlap
- Superior quality vs naive approaches

**Evaluation Workspace**
- Request access modal with email/LinkedIn buttons
- Activate key section
- Multi-corpus upload support (evaluation keys)
- Persistent storage beyond 24h demo limit

**Evidence & Transparency**
- Route badges (which agent/corpus answered)
- Confidence scores (0-100%)
- Chunk counts (evidence used)
- Full auditability

**Folder Upload**
- 3 files in demo mode
- Automatic 10% corpus overview
- Suggested questions based on content
- Instant Q&A capability

**Answer Export**
- Word (.docx) format
- Markdown (.md) format
- Evidence annotations included

**Workspace Page**
- Corpus management
- Scoped Q&A (query specific corpus)
- API key status tracking

### 🛠️ Technical Highlights

- Async middleware with cache-first validation (99% DB call reduction)
- Zero-downtime key provisioning (5 min activation)
- Format-aware routing (100x speedup on plain text)
- Graceful degradation (missing key → demo mode)
- Row-level security (RLS) for multi-tenant isolation
- Rate limiting (<$5/day cost with public access)

### 📊 Metrics

- Query latency: 1.8-3.2s (complex queries)
- Cloud Run: ~2.9s average
- Uptime: 99%+ (Cloud Run SLA)
- Accuracy: 20% improvement (multi-agent vs single)

### 🔒 Security

- API key validation via Supabase
- One-key-per-IP enforcement
- RLS for data isolation
- 24h auto-deletion (demo mode)
- Rate limiting (5 req/min per IP)

### 🎯 Known Issues (Deferred to v2.0)

**Minor (non-blocking):**
- Upload overview timing (shows "no chunks" briefly)
- YouTube processing error (backend fix needed)
- Answer verbosity (tightening code exists, not deployed)

All deferred work saved in private repo tag `wip-v257`.

---

## [Unreleased] - v2.0 (Planned)

### Planned Features

**Template Extraction (Prerequisite)**
- Extract HTML from monolithic app.py to Jinja2 templates
- Enable faster UI iteration
- Eliminate quote escaping issues

**Upload Overview Fix**
- Add retry logic with exponential backoff
- Fix "no chunks" timing issue
- Improved progress indicators

**File-Level Summaries**
- Clickable file names in upload list
- Per-file 10% summaries
- File-scoped Q&A

**Answer Tightening**
- Simple questions: <50 words
- Corpus-agnostic detection
- Generic phrase filtering

**YouTube Processing Fix**
- Review Cloud Run logs
- Fix backend handler
- Add progress updates

**MinIO Pilot**
- Chunk text offloading to object storage
- Dual-write pattern (Supabase + MinIO)
- Cost optimization for large corpora

---

## Version Format

Versions follow semantic versioning: `MAJOR.MINOR.PATCH`

- **MAJOR:** Breaking changes or major feature sets
- **MINOR:** New features, backward-compatible
- **PATCH:** Bug fixes, documentation updates

---

## Contact

For technical questions, evaluation access, or collaboration:  
📧 **vinod.sridharan@txvault.app**

---

**Repository:** https://github.com/VinodSridharan/MAROL-System-Overview  
**Live Demo:** https://marol-backend-467264912930.us-central1.run.app  
**Version:** v1.0 (2026-01-10)

