# MAROL Repository Structure

This document explains the organization of the MAROL project across multiple repositories.

---

## This Repository: MAROL-System-Overview

**Purpose:** Public portfolio/overview repository  
**Type:** Documentation and system architecture  
**Status:** Public

**Contains:**
- Documentation (`docs/`) - Architecture, capabilities, highlights
- Screenshots - UI snapshots and demo visuals
- README.md - Project overview and live demo links
- CHANGELOG.md - Version history and release notes
- Architecture diagrams and design notes

**What this repo does NOT contain:**
- `app.py` or production backend code
- Test suites (191 automated tests)
- Deployment scripts
- Private API keys or configuration

This is a **curated showcase** for recruiters, technical interviewers, and collaborators to understand the system design and capabilities without access to the private codebase.

---

## cole-medin-ai-mirror (Private)

**Purpose:** Main application repository  
**Type:** Private production codebase  
**Status:** Private (proprietary)

**Contains:**
- FastAPI backend (`app.py`)
- LangGraph orchestration graphs
- Multi-agent RAG implementation
- 191 automated tests
- Supabase integration
- Google Cloud Run deployment scripts
- API key management and authentication

**Key Components:**
- Research Agent, Direct Answer Agent, Perfection Agent
- Hybrid retrieval (BM25 + vector + cross-encoder)
- WhisperingChunks API integration
- Exam-Ready evaluation harness
- Evidence badge generation
- Answer export (Word, Markdown)

This is where the **production system** lives. For evaluation access or technical collaboration, contact: [vinod.sridharan@txvault.app](mailto:vinod.sridharan@txvault.app)

---

## WhisperingChunks-Overview

**Purpose:** Audio/video transcription service  
**Type:** Separate project with own deployment  
**Status:** Public overview repository

**Repository:** [https://github.com/VinodSridharan/WhisperingChunks-Overview](https://github.com/VinodSridharan/WhisperingChunks-Overview)

**What it does:**
- Transcribes YouTube videos, podcasts, audio files
- Uses OpenAI Whisper for speech-to-text
- Intelligent overlap-based chunking (500-token chunks, 50-token overlap)
- Feeds transcribed content into MAROL as searchable corpora

**Integration:**
MAROL calls WhisperingChunks via APIs to process audio/video content. The transcribed and chunked content is then indexed in Supabase for Q&A queries.

---

## marol-demo (Archived)

**Purpose:** Earlier demo version  
**Type:** Archived repository  
**Status:** Not in use

This repository is archived and superseded by the current production deployment. Please refer to the live demo or this System Overview repository instead.

---

## Repository Ecosystem Summary

```
MAROL System Architecture
│
├── MAROL-System-Overview (Public)
│   └── Documentation, architecture, portfolio showcase
│
├── cole-medin-ai-mirror (Private)
│   └── Production backend, tests, deployment
│
├── WhisperingChunks-Overview (Public)
│   └── Transcription service (separate deployment)
│
└── marol-demo (Archived)
    └── Legacy demo (not in use)
```

---

## Live Demo

**URL:** [https://marol-backend-467264912930.us-central1.run.app](https://marol-backend-467264912930.us-central1.run.app)

The live demo is deployed from the private `cole-medin-ai-mirror` repository and serves as the production Answer Guru console.

---

## Contact

For technical questions, evaluation access, or collaboration:

📧 **vinod.sridharan@txvault.app**  
🔗 **LinkedIn:** [linkedin.com/in/vinod-s-6a565b1b8](https://www.linkedin.com/in/vinod-s-6a565b1b8)

---

**Last Updated:** January 20, 2026
