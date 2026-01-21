# MAROL Security Policy

**Effective Date:** January 20, 2026

This policy describes security measures protecting MAROL and your data.

---

## 🔐 Data Security

### Encryption
- **In transit:** TLS 1.3 (HTTPS) for all browser ↔ Cloud Run traffic
- **At rest:** AES-256 encryption in Supabase for all corpus chunks
- **API keys:** Hashed (bcrypt) before storage; plaintext keys never logged

### Access Control
- **Row-Level Security (RLS):** Supabase policies ensure your key = only your data
- **No shared access:** Evaluation/Premium keys are single-user; sharing violates terms
- **Admin access:** Limited to metadata only (file counts, timestamps); staff cannot read corpus content

---

## 🛡️ Infrastructure Security

### Cloud Run (Google Cloud Platform)
- **Auto-scaling:** Instances created/destroyed on demand; no persistent local storage
- **Secrets management:** API keys (OpenAI, Supabase) stored in Google Secret Manager, not in code
- **Network isolation:** Backend not directly exposed; Cloud Run handles TLS termination

### Supabase (PostgreSQL + pgvector)
- **Managed service:** Automatic security patches, backups
- **Rate limiting:** API request limits prevent abuse
- **Audit logs:** Query logs retained for 7 days (compliance/debugging only)

---

## 🚨 Incident Response

**If you suspect a security issue:**
1. **Email immediately:** [vinod.sridharan@txvault.app](mailto:vinod.sridharan@txvault.app?subject=Security%20Issue)
2. **Include:** Description, steps to reproduce, potential impact
3. **We will respond within:** 24 hours (business days) with initial assessment

**Responsible disclosure:**
- We appreciate security researchers reporting vulnerabilities privately (not public disclosure until patched)
- No bug bounty program currently, but serious findings will be credited in CHANGELOG

---

## 🔍 What We Log

**Logged (anonymized where possible):**
- Query timestamps, corpus IDs, route decisions (for debugging/analytics)
- Error messages (sanitized to remove PII)
- Rate limit violations, abuse attempts

**Never logged:**
- Raw corpus content (your uploaded documents)
- Full API keys (only hashed versions)
- Personal information beyond what you voluntarily provide (email for key issuance)

**Log retention:** 30 days, then purged

---

## 🔑 API Key Security Best Practices

**Do:**
- Store keys in environment variables or secure password managers
- Invalidate keys immediately if compromised
- Use separate keys for different projects (when Premium launches multi-key support)

**Don't:**
- Commit keys to GitHub or public repos
- Share keys via email or Slack (request separate keys for teammates)
- Embed keys in client-side JavaScript (keys are for server-side API use only)

---

## 🛠️ Vulnerability Disclosure

**Known limitations (not vulnerabilities):**
- **Prompt injection:** We filter common patterns, but sophisticated attacks may bypass filters (report novel techniques)
- **Rate limits:** Demo tier limits are soft; determined attackers can still query frequently (acceptable for demo; Evaluation tier has better controls)

**Future hardening (roadmap):**
- SOC 2 compliance audit (if Premium scales)
- Penetration testing by third-party firm
- Bug bounty program

---

**Last Updated:** January 20, 2026

**Security Contact:** [vinod.sridharan@txvault.app](mailto:vinod.sridharan@txvault.app?subject=Security%20Inquiry)
