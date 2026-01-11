# MAROL Architecture

## High-Level Design

MAROL implements a **multi-agent RAG pipeline** with intelligent routing and evidence-based synthesis.

---

## Component Layers

### 1. Request Layer
- FastAPI async handlers
- API key validation (async middleware with 5-min cache)
- Rate limiting (per-IP, configurable)
- Session management

### 2. Routing Layer (LangGraph)
- State graph orchestration
- Agent selection based on query type:
  - **Research Agent:** Complex, multi-hop queries
  - **Direct Answer Agent:** Factual questions
  - **Perfection Agent:** Definition-style queries
- Confidence scoring

### 3. Retrieval Layer
- **Supabase pgvector** (semantic search)
- **BM25** keyword ranking
- **Cross-encoder** reranking
- **RRF fusion** (Reciprocal Rank Fusion)

### 4. Synthesis Layer
- LLM-based generation (GPT-4/Claude/Gemini)
- Evidence validation
- 100% grounding enforcement
- Answer quality checks

### 5. Storage Layer
- Supabase (PostgreSQL + pgvector)
- Row-level security (RLS)
- API key management
- Corpus lifecycle hooks

---

## Data Flow
User Query
↓
API Validation (cached, <1ms)
↓
LangGraph Router (selects agent)
↓
Agent Node (retrieve strategy)
↓
Hybrid Search (BM25 + vector + rerank)
↓
Supabase pgvector (return chunks)
↓
Synthesis Node (LLM + evidence validation)
↓
Response (answer + evidence badges)

---

## Audio/Video Pipeline (WhisperingChunks)
YouTube URL / Audio File
↓
yt-dlp (audio extraction)
↓
OpenAI Whisper (speech-to-text)
↓
WhisperingChunks (overlap-based chunking)
↓
Embedding Generation (OpenAI)
↓
Supabase Storage
↓
Available for Q&A


**Key innovation:** Overlap-merge strategy (500-token chunks, 50-token overlap) preserves semantic continuity across boundaries.

---

## Deployment Architecture

### Google Cloud Run
- **Serverless containers** (no server management)
- **Auto-scaling** (0→N instances based on load)
- **HTTPS load balancing** (built-in)
- **Environment-based config** (25 variables)

### Supabase Backend
- **Vector storage** (pgvector extension)
- **API key table** with RLS
- **Chunk metadata** and embeddings
- **Scheduled cleanup** (24h retention for demo)

### Multi-Tier Access
- **Demo:** Public, 3 files, 24h retention
- **Evaluation:** API key, unlimited corpora, persistent storage
- **Developer:** Local, all features, no restrictions

---

## Key Patterns

### 1. Cache-First Validation
**Problem:** API key validation on every request = latency + DB load  
**Solution:** 5-min cached validation with async usage tracking

**Impact:**
- 99% reduction in DB calls
- <1ms validation latency (vs 50ms per request)
- Fire-and-forget usage tracking (non-blocking)

### 2. Zero-Downtime Key Management
**Problem:** Cloud Run redeploy takes 60 min, can't give instant access  
**Solution:** Store keys in Supabase (not env vars), cache with TTL

**Impact:**
- New keys active in 5 min (cache refresh)
- No redeployment needed
- Dual expiration (time + usage limits)

### 3. Format-Aware Routing
**Problem:** Docling PDF parser has overhead, wasteful for plain text  
**Solution:** Decision matrix routes by file type

**Impact:**
- 100x speedup on plain text (60% of corpus)
- Zero cost for text (no Docling calls)
- Full structure preservation for PDFs

### 4. Graceful Degradation
**Problem:** Hard auth walls hurt UX for portfolio demos  
**Solution:** Missing key → Demo mode (not HTTP 401)

**Impact:**
- Frictionless portfolio showcase
- Feature-level security (not endpoint-level)
- Clear upgrade prompts

---

## WhisperingChunks Integration

### Chunking Strategy

**Standard approach:**  
Fixed-size chunks → breaks context → poor retrieval

**WhisperingChunks approach:**  
Overlap-merge chunking → preserves context → superior retrieval

**Implementation:**
- 500-token base chunks
- 50-token overlap between chunks
- Merge overlapping segments
- Preserve semantic flow

**Result:**  
Long-form audio (podcasts, talks) becomes highly queryable.

---

## Security Architecture

**Multi-tenant isolation:**
- Row-level security (RLS) in Supabase
- API key ownership enforcement
- Corpus-key lifecycle binding

**Rate limiting:**
- Per-IP request limits (5 req/min in demo)
- Token budgeting (prevent runaway costs)
- Abuse detection and blocking

**Data retention:**
- Demo: Auto-delete after 24h
- Evaluation: Persist while key active
- Cascade delete on key expiry

---

## Observability

**Structured logging:**
- Every LLM call logged (latency, tokens, cost)
- Routing decisions tracked
- Evidence validation recorded

**Analytics:**
- UI event tracking
- Query performance metrics
- Usage patterns (gitignored config)

---

## Contact

For technical deep-dives or architecture discussions:  
📧 **vinod.sridharan@txvault.app**

Live system:  
🌐 https://marol-backend-467264912930.us-central1.run.app
