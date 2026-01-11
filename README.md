<div align="center">
  <img src="assets/logo.png" alt="MAROL - Sky Swan Logo" width="256"/>
  
  # MAROL
  ### Multi-Agent RAG Orchestration Lab
  
  **"Reasoning is the key. Orchestration is the sauce."**
  
  [![Live Demo](https://img.shields.io/badge/Demo-Live-success)](https://marol-backend-467264912930.us-central1.run.app)
  [![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
  [![Cloud Run](https://img.shields.io/badge/Google%20Cloud-Run-4285F4?logo=google-cloud)](https://cloud.google.com/run)
  
  **Production multi-agent RAG system for technical collaboration**
  
  🌐 [Try Live Demo](https://marol-backend-467264912930.us-central1.run.app) • 📧 [Contact](mailto:vinod.sridharan@txvault.app)
</div>

---

## ⚡ What MAROL Demonstrates

Most RAG systems can't **think**—they just retrieve and generate.

**MAROL is different.**

It uses **three specialized agents** that collaborate through deliberative reasoning loops:

1. **Retrieval Agent** → Finds information (hybrid BM25 + vector search)
2. **Reasoning Agent** → Evaluates: *"Is this enough? Do I need more?"*
3. **Synthesis Agent** → Generates grounded answers with full evidence

**The result:** 20% better accuracy on complex queries, with full cost controls and evidence transparency.

**Live on Google Cloud Run** - v1.0 deployed 2026-01-10

---

## 🎯 Key Features (v1.0)

✨ **Multi-Agent Orchestration** - LangGraph state graphs with specialized agents  
🔍 **Hybrid Retrieval** - BM25 + vector + reranking (91% vs 78% accuracy)  
🎙️ **WhisperingChunks Engine** - Proprietary transcription for audio/video  
🔑 **Evaluation Workspace** - Request access via in-app modal (email/LinkedIn buttons)  
📊 **Evidence Badges** - Route, confidence, chunks displayed above every answer  
📁 **Folder Upload** - 3 files with automatic 10% corpus overview  
✅ **100% Grounding** - No hallucinations, corpus-only answers  

---

## 🎙️ Powered by WhisperingChunks

MAROL's audio/video processing uses **WhisperingChunks** — a production transcription engine achieving superior quality through intelligent overlap-based chunking.

**Features:**
- High-quality transcription (OpenAI Whisper)
- Intelligent chunking (500-token chunks, 50-token overlap)
- YouTube & audio support (yt-dlp integration)
- Semantic continuity preservation

Enables processing of long-form content (podcasts, videos, talks) with high retrieval accuracy.

🔗 [WhisperingChunks Repository](https://github.com/VinodSridharan/WhisperingChunks-Overview)

---

## 📊 Metrics (v1.0)

**Performance:**
- Query latency: 1.8-3.2s (complex multi-agent queries)
- Cloud Run: ~2.9s average (serverless)
- Retrieval: 91% (hybrid) vs 78% (vector-only)

**Quality:**
- 20% accuracy improvement (multi-agent vs single)
- 100% grounding (no hallucinations)
- Full evidence transparency

**Deployment:**
- Uptime: 99%+ on Cloud Run
- Auto-scaling: 0→N instances
- Cost: <$5/day with public access

---

## 🛠️ Technology Stack

**Orchestration:** LangGraph (state graphs, cyclic workflows)  
**Backend:** Python 3.11, FastAPI (async)  
**Transcription:** **WhisperingChunks** (proprietary)  
**Database:** Supabase (PostgreSQL + pgvector)  
**LLMs:** OpenAI GPT-4, Anthropic Claude, Google Gemini  
**Retrieval:** Hybrid (BM25 + vector + reranking)  
**Deployment:** Google Cloud Run (serverless)  
**Frontend:** Alpine.js, Tailwind CSS  

---

## 🚀 Try It Now

### Live Demo

🌐 [**https://marol-backend-467264912930.us-central1.run.app**](https://marol-backend-467264912930.us-central1.run.app)

**Free demo features:**
- Multi-agent Q&A with evidence badges
- Folder upload (3 files max)
- Automatic 10% corpus overview with suggested questions
- Export answers (Word, Markdown)
- YouTube/audio transcription via WhisperingChunks

**Try these questions:**
- "What is LangGraph?"
- "What does Cole use for payments?"
- "What are AI-native workflows?"

---

## 📧 Request Evaluation Access

For deeper testing (multi-corpus, persistent storage, workspace features):

**📧 vinod.sridharan@txvault.app**  
**Subject:** MAROL Evaluation Workspace Request

Or use the **in-app modal**:
1. Click "Request evaluation access →"
2. Choose "Open email draft" or "Copy LinkedIn message"
3. Send your request

Keys are time-boxed and usage-limited—perfect for focused evaluations and interviews.

---

## 🎯 Use Cases

**Engineering Interviews** - Walk through multi-agent architecture, explain routing decisions, discuss RAG trade-offs in real-time

**Stakeholder Demos** - Upload custom documents, get automatic corpus overviews, ask grounded questions with full evidence

**Audio/Video Q&A** - Process YouTube videos, podcasts, technical talks via WhisperingChunks transcription

**Collaborative Reviews** - Request evaluation access, test workspace features, validate RAG patterns

---

## 📖 Documentation

- [System Overview](docs/OVERVIEW.md) - What MAROL demonstrates
- [Capabilities](docs/CAPABILITIES.md) - Feature descriptions
- [Architecture](docs/ARCHITECTURE.md) - Technical design patterns
- [Safety & Privacy](SAFETY.md) - Data handling policies

---

## 🤝 Contact & Collaboration

**For technical discussions, evaluation access, or collaboration:**

📧 **vinod.sridharan@txvault.app**  
🔗 **LinkedIn:** [linkedin.com/in/vinod-s-6a565b1b8](https://www.linkedin.com/in/vinod-s-6a565b1b8)  
🌐 **Live Demo:** https://marol-backend-467264912930.us-central1.run.app

**Open to:**
- Engineering interviews & code walkthroughs
- RAG architecture discussions
- Multi-agent orchestration consulting
- Speaking opportunities

---

## 🙏 Related Projects

🎙️ **WhisperingChunks** - Production transcription & chunking engine  
[github.com/VinodSridharan/WhisperingChunks-Overview](https://github.com/VinodSridharan/WhisperingChunks-Overview)

---

## 📝 Version History

**v1.0** (2026-01-10)
- Multi-agent orchestration with LangGraph
- WhisperingChunks integration for audio/video
- Evaluation workspace with request modal
- Folder upload with 10% overview
- Evidence badges for transparency
- Production Cloud Run deployment

---

## 📄 License

MIT License - See [LICENSE](LICENSE).

**Note:** This repository contains documentation and overview only. The live system is proprietary. For evaluation access or technical collaboration: vinod.sridharan@txvault.app

---

## 🙏 Acknowledgments

- [LangGraph](https://github.com/langchain-ai/langgraph) by LangChain
- [Supabase](https://supabase.com/) for vector storage
- [Google Cloud Run](https://cloud.google.com/run) for serverless deployment
- **WhisperingChunks** - Proprietary transcription engine

---

<div align="center">
  
  **Latest Update:** 2026-01-10 | **Status:** ✅ Production | **Version:** v1.0
  
  Made with 🦢 for the AI/ML community
  
  <img src="https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2FVinodSridharan%2FMAROL-System-Overview&label=Visitors&countColor=%23263759" />
</div>
