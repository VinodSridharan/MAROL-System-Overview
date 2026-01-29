# Security Policy

**Effective Date:** January 28, 2026

## How We Protect Your Data

### Encryption
- **In transit:** TLS 1.3 (HTTPS)
- **At rest:** AES-256 encryption (Supabase default)

### Access Control
- **Row-Level Security (RLS):** Each key/session has its own isolated corpus namespace in Supabase
- **API key hashing:** Keys hashed with bcrypt before storage (plaintext keys never stored)
- **Session cookies:** HttpOnly, Secure, SameSite=Strict

### Abuse Prevention (Automated)
- **IP tracking:** Demo sessions track IP + user_agent for rate limiting (automated, not visible to users)
- **Fingerprinting:** IP + browser fingerprint combo (3 sessions per fingerprint per 24h for Demo)
- **Automated blocking:** System automatically blocks IPs exceeding rate limits (no human review)

### What We Track
- **Demo:** IP address, user_agent (for automated abuse prevention only, deleted after 24h)
- **Evaluation:** Email (for key issuance), key metadata (expiry, usage count)
- **No tracking:** No cookies, no analytics, no third-party trackers

## Security Incident Response

If you discover a security vulnerability:
1. **Email:** vinod.sridharan@txvault.app with subject "Security Issue"
2. **Do NOT publicly disclose** until we've had a chance to fix it
3. We'll respond within 48 hours and provide credit if you'd like

## Scope
- Backend API (FastAPI on Cloud Run)
- Database (Supabase/PostgreSQL with RLS)
- Frontend (Alpine.js SPA served from FastAPI)

**Out of scope:**
- Third-party services (OpenAI API, Whisper API)
- User's local browser/device security

***

**See also:** PRIVACY_POLICY.md, DATA_RETENTION_POLICY.md
