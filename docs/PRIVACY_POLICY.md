# MAROL Privacy Policy

**Effective Date:** January 20, 2026

This policy describes how we collect, use, and protect your information.

---

## 📊 What We Collect

### Information You Provide
- **Email address** (only when requesting Evaluation or Premium access)
- **Uploaded documents** (stored temporarily per tier retention policy)
- **Query text** (your questions to MAROL)

### Automatically Collected
- **Usage logs:** Timestamps, corpus IDs, route decisions, query latency (for debugging and analytics)
- **Error logs:** Sanitized error messages (no PII)
- **API key metadata:** Issued-to email, expiration date, usage count (not the plaintext key)

### What We DON'T Collect
- ❌ Passwords (no user accounts yet)
- ❌ Payment info (manual billing for now; Stripe will handle when integrated)
- ❌ Browsing history outside MAROL
- ❌ Device fingerprints or tracking cookies

---

## 🎯 How We Use Your Information

| Purpose | Legal Basis (GDPR) |
|---------|-------------------|
| **Provide the service** (process queries, store corpora) | Contractual necessity |
| **Improve quality** (debug errors, optimize routing) | Legitimate interest |
| **Prevent abuse** (rate limiting, detect prompt injection) | Legitimate interest |
| **Communicate** (key expiration reminders, updates) | Contractual necessity |

**We do NOT:**
- Sell your data to third parties
- Use your corpus content to train models
- Share your data except as required by law

---

## 🔒 Data Storage & Security

### Where Your Data Lives
- **Corpora & embeddings:** Supabase (US-based, encrypted at rest)
- **Application backend:** Google Cloud Run (us-central1)
- **Logs:** Cloud Run logging (30-day retention)

### Security Measures
- **Encryption:** TLS 1.3 in transit, AES-256 at rest
- **Access control:** Row-Level Security (RLS) in Supabase
- **Key hashing:** API keys hashed before storage (bcrypt)

**See [SECURITY_POLICY.md](SECURITY_POLICY.md) for full details.**

---

## 🗑️ Data Retention & Deletion

| Tier | Retention | Deletion |
|------|-----------|----------|
| **Demo** | 24 hours | Auto-delete, no recovery |
| **Evaluation** | 7 days | Auto-delete on key expiration (7-day grace period) |
| **Premium** | Persistent | 30-day grace after cancellation, then deleted |

**Manual deletion:** You can delete corpora anytime via `/workspace` or email request.

**Right to erasure (GDPR):** Email [vinod.sridharan@txvault.app](mailto:vinod.sridharan@txvault.app?subject=Data%20Deletion%20Request) to request immediate deletion of all your data.

**See [DATA_RETENTION_POLICY.md](DATA_RETENTION_POLICY.md) for full details.**

---

## 🌍 International Users

**Data transfers:**
- MAROL is hosted in the US (Google Cloud, us-central1)
- EU/UK users: By using MAROL, you consent to data transfer to the US
- We rely on **Standard Contractual Clauses (SCCs)** for GDPR compliance

**Your rights under GDPR:**
- **Right to access:** Request a copy of your data
- **Right to erasure:** Request deletion
- **Right to portability:** Export your corpora (JSON/Word/Markdown)
- **Right to object:** Opt out of analytics logging (contact us)

**To exercise rights:** Email [vinod.sridharan@txvault.app](mailto:vinod.sridharan@txvault.app?subject=GDPR%20Request)

---

## 🍪 Cookies & Tracking

**We use minimal cookies:**
- **`localStorage` (browser-side):** Stores your API key locally (not a cookie, never sent to server except in API headers)
- **No tracking cookies:** No Google Analytics, Facebook Pixel, or similar

**Third-party services:**
- **OpenAI API:** We send query text to OpenAI for LLM synthesis (covered by OpenAI's DPA)
- **Supabase:** Hosts your corpora (covered by Supabase's DPA)

---

## 🔄 Policy Changes

We may update this policy to reflect new features or legal requirements. Changes effective immediately upon posting.

**We will notify you via email** (if we have it) for material changes affecting your rights.

**Last Updated:** January 20, 2026

---

## 📧 Contact & Questions

**Privacy concerns:** [vinod.sridharan@txvault.app](mailto:vinod.sridharan@txvault.app?subject=Privacy%20Inquiry)

**Data Protection Officer (when required):** Not yet designated (small operation); contact above email for all privacy matters.
