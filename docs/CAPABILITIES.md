# MAROL Capabilities

## Core Features (v1.0)

### 1. Multi-Agent Q&A
Ask questions about uploaded documents or pre-loaded corpora. System automatically routes to appropriate agent (Research, Direct Answer, Perfection) based on query complexity. Evidence badges show routing transparency.

**What you get:**
- Route badge (which agent/corpus answered)
- Confidence score (0-100%)
- Chunk count (evidence used)

### 2. Folder Upload with 10% Overview
Upload 3 files in demo mode (.txt, .md, .pdf, .docx). System automatically generates:
- 10% corpus overview (key topics and themes)
- 4-6 suggested questions based on actual content
- Instant Q&A capability

**Perfect for:** Quick document reviews, exploratory Q&A, interview demos

### 3. Audio/Video Processing (WhisperingChunks)
Process YouTube videos, podcasts, and audio files with production-grade transcription.

**Powered by WhisperingChunks:**
- OpenAI Whisper for speech-to-text
- Intelligent overlap chunking (500-token chunks, 50-token overlap)
- Semantic continuity preservation
- Long-form content support

**Supported formats:**
- YouTube URLs
- Audio files (.mp3, .wav, .webm)
- Video files (via URL)

**Result:** Long-form audio/video content becomes queryable with high accuracy.

### 4. Evaluation Workspace
Request deeper access via in-app modal with built-in email/LinkedIn templates.

**What's included:**
- Multi-corpus uploads (unlimited)
- Persistent storage (beyond 24h demo limit)
- Workspace page (corpus management)
- Enhanced analytics

**How to request:**
- Click "Request evaluation access →" in UI
- Use "Open email draft" or "Copy LinkedIn message" buttons
- Send to: vinod.sridharan@txvault.app

### 5. Evidence Transparency
Every answer includes full evidence trail:

**Route badge:** Shows which corpus or agent answered  
**Confidence score:** System's certainty (0-100%)  
**Chunk count:** Number of evidence chunks used  

**Why it matters:** Full auditability, no black-box answers

### 6. Answer Export
Download Q&A sessions as formatted documents:
- **Word (.docx)** - Professional reports
- **Markdown (.md)** - Developer-friendly format

Evidence annotations included in exports.

### 7. Workspace Page
Dedicated page for advanced users:
- Corpus list with retention policies
- Scoped Q&A (query specific corpus)
- API key status and usage tracking
- Analytics shortcuts

---

## Three-Tier Access

### Demo (Free - No Signup)
- 3 files max
- 24h retention
- Single corpus
- All features, limited scale
- Perfect for portfolio showcase

### Evaluation (Request Access)
- Multi-corpus uploads
- Persistent storage
- Workspace features
- Time-boxed keys
- Perfect for interviews/reviews

**Request:** vinod.sridharan@txvault.app

---

## Technical Capabilities

### Retrieval
- **Hybrid search:** BM25 + vector + cross-encoder reranking
- **Accuracy:** 91% (hybrid) vs 78% (vector-only)
- **Sources:** Uploaded docs, YouTube transcripts, pre-loaded corpora

### Orchestration
- **LangGraph state graphs** with cyclic workflows
- **Agent selection:** Automatic based on query type
- **Self-correction:** Agents can request more context

### Grounding
- **100% policy:** Answers use only corpus content
- **No generic knowledge:** Explicit negation when no answer
- **Evidence required:** Every claim backed by chunk reference

### Audio/Video
- **WhisperingChunks engine:** Proprietary transcription
- **Quality:** Superior to naive chunking approaches
- **Formats:** YouTube, .mp3, .wav, .webm

### Deployment
- **Cloud Run:** Serverless, auto-scaling
- **Uptime:** 99%+ SLA
- **Latency:** 1.8-3.2s for complex queries
- **Cost:** Controlled with rate limiting

---

## What You Can Do

**Upload documents** → Get instant Q&A with evidence  
**Process audio/video** → Make long-form content queryable  
**Request evaluation access** → Test workspace features  
**Export Q&A** → Save as Word/Markdown  
**Ask complex questions** → See multi-agent collaboration in action  

---

## Contact

**Questions or collaboration:**  
📧 vinod.sridharan@txvault.app

**Live demo:**  
🌐 https://marol-backend-467264912930.us-central1.run.app

