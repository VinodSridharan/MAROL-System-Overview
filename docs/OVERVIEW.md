# What MAROL Does

MAROL is a **production-deployed multi-agent RAG system** that demonstrates advanced LLM orchestration.

## The Problem

Most RAG systems do simple retrieval → generation. They can't:
- Self-correct when context is insufficient
- Request more information mid-reasoning
- Adapt their approach based on query complexity

## The Solution

MAROL uses **three specialized agents** that collaborate:

### Retrieval Agent
Finds relevant information using hybrid search (semantic + keyword)

### Reasoning Agent
Evaluates context quality and decides: "Do I need more information?"

### Synthesis Agent
Generates grounded answers with proper citations

## Why This Matters

This isn't theory—it's a **live system** handling real queries with:
- Cost controls that kept demo under $5/day with public access
- Security hardening for multi-tenant isolation
- Measurable quality improvements (~20% better accuracy vs. single-agent)

## Live Demo

🚀 [Try it now](https://marol-demo-467264912930.us-central1.run.app)

Ask preset questions or explore the UI. Rate limiting active for cost protection.

