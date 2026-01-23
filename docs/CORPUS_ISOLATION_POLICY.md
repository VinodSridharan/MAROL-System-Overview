# Corpus Isolation Policy

**Last Updated**: 2026-01-23

## Core Principle
**Default: Isolated. Exception: Contributed with Attribution.**

***

## Default Behavior: Isolated Corpora

When you upload documents to MAROL:
- ✅ Your corpus is PRIVATE and ISOLATED
- ✅ Only YOU can query your corpus (via your API key)
- ✅ Other users CANNOT access your documents
- ✅ No cross-corpus querying without permission

### Technical Implementation
- Row-Level Security (RLS) in Supabase enforces isolation
- Each API key maps to specific corpus IDs
- Queries filtered by `source_id` and `api_key`

***

## Exception: Contributing Your Corpus

You can CONTRIBUTE your corpus to MAROL's public questions:

### How to Contribute
Email: vinod.sridharan@txvault.app  
Subject: Contribute Corpus - [Your Use Case]

**Include**:
1. Your API key ID
2. Corpus name (e.g., "Email Archive 2025")
3. Attribution preference (e.g., "John Doe" or "Anonymous")
4. Confirmation: "I authorize MAROL to use this corpus for public questions"

### What Happens
- ✅ Your corpus joins MAROL's preset questions
- ✅ Other users can benefit from your expertise
- ✅ Clear attribution in every answer
- ✅ You retain ownership and can revoke anytime

### Attribution Format
Every answer using your contributed corpus shows:
```
Based on [Email Archive 2025] (Contributed by: john@example.com)
```

***

## Answer Attribution

### User's Own Corpus
```
Based on Your Corpus: FU Test 2-folder-1769188157
```

### MAROL Preset Corpus
```
Based on Ai Tech Stack 2026 (MAROL Curated)
```

### Contributed Corpus
```
Based on Email Archive Analysis (Contributed by: jane@example.com)
```

***

## Revocation

To stop sharing your contributed corpus:
1. Email: vinod.sridharan@txvault.app
2. Subject: Revoke Corpus Contribution - [Corpus Name]
3. Your corpus becomes private again within 24 hours

***

## Privacy Guarantees

### What We Track
- Corpus name and source_id
- Contributor email (for attribution)
- Contribution date

### What We DON'T Track
- Document content (only metadata)
- Your query history on your own corpus
- Personal data beyond what you provide

***

## FAQ

**Q: Can other users see my document content?**  
A: No. Only metadata (corpus name, contributor) is visible. Document content remains in your isolated corpus.

**Q: What if I upload sensitive data?**  
A: Don't contribute it. Keep it isolated in your private corpus.

**Q: Can I contribute anonymously?**  
A: Yes. Specify "Anonymous" as your attribution preference.

**Q: Can MAROL staff see my documents?**  
A: No. RLS prevents staff access to corpus content. Only metadata (file count, size) is visible.

***

**Contact**: vinod.sridharan@txvault.app
