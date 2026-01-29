# Data Retention Policy

**Effective Date:** January 28, 2026

## Retention by Tier

| Tier | Retention | Deletion Process | Grace Period |
|------|-----------|------------------|--------------|
| **Demo** | 24 hours | Automatic (hourly cleanup job) | None |
| **Evaluation** | 7 days | Automatic (daily cleanup job) | None |
| **Premium** | 365 days | Automatic after 30-day grace | 30 days |
| **Collaborator** | 30 days (project) | Automatic after 7-day grace | 7 days |

## Automatic Deletion (No Human Involvement)

All deletions are **fully automated** by the system:
- **Demo:** Hourly cleanup job deletes sessions older than 24h
- **Evaluation:** Daily cleanup job deletes keys older than 7d
- **Premium/Collaborator:** Automated after grace period expires

**No human review. No recovery. Deletion is immediate and final.**

## What Happens at Expiry

### Demo (24h)
- All uploads, chunks, and queries automatically deleted
- No export available
- No recovery possible

### Evaluation (7d)
- **Email reminder sent automatically 1 day before expiry:** "Your Evaluation key expires in 24 hours. Export your data now."
- **At expiry:** All corpora, chunks, and metadata automatically deleted by the system
- **Export available before expiry** (Word/Markdown with citations)
- **No grace period** (free tier)

### Premium (365d, future)
- **Subscription active** → workspace persists indefinitely
- **Subscription cancelled** → 30-day grace period, then automatic deletion
- **Email reminders sent automatically** at 7d, 3d, 1d before deletion
- **After grace period:** System automatically deletes all data (no recovery)

### Collaborator (30d project)
- **After project completion** → 7-day grace period for export/review
- **Email reminder sent automatically 1 day before deletion**
- **Then automatic permanent deletion** by the system
- Can extend if project continues (additional invoice)

## Ingestion = Consent

By uploading files, YouTube URLs, or audio to MAROL, you consent to:
- Storage according to your tier's retention policy
- **Automatic deletion** at expiry (system-driven, no human discretion)
- Processing for embedding generation and RAG retrieval

## Your Rights (GDPR/CCPA)

- **Right to access:** Email us for a copy of your data
- **Right to erasure:** Email us to delete your data early (before automatic expiry)
- **Right to export:** Download your corpora and answers (Evaluation tier and above)

**Contact:** vinod.sridharan@txvault.app

***

**See also:** PRIVACY_POLICY.md, SECURITY_POLICY.md
