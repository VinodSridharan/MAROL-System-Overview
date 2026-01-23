# MAROL Data Retention Policy

**Effective Date:** January 20, 2026

This policy describes how long we keep your uploaded documents and corpora.

---

## 🗂️ Retention by Tier

| Tier | Retention Period | Notes |
|------|-----------------|-------|
| **Demo** | 24 hours (auto-delete) | No exceptions; data deleted exactly 24h after upload |
| **Evaluation** | 7 days OR key expiration | Whichever comes first; corpora deleted when key expires |
| **Premium** | Persistent (until you delete) | 30-day grace period after cancellation |

---

## 🔑 Evaluation Key & Data Lifecycle

**During 7-day evaluation:**
- Your corpora persist as long as key is valid
- You can manually delete corpora anytime via `/workspace`

**When key expires (after 7 days):**
1. **Immediate:** Key becomes invalid; you lose access to corpora
2. **Grace period (7 days):** Corpora preserved but inaccessible
3. **After 7 days total (evaluation + grace):** Corpora permanently deleted

**Key invalidation = data death:** If you invalidate your Evaluation key early, corpora are deleted immediately (no grace period).

**Preservation option:** Email us before expiration to request corpus export (JSON dump) or extension.

---

## 💾 Backup & Recovery

**We maintain backups for:**
- System integrity (disaster recovery only)
- Not for user data recovery after deletion

**Once data is deleted (post-retention period), it cannot be recovered.**

---

## 🛡️ Security During Retention

- **Encryption at rest:** All corpora encrypted in Supabase (AES-256)
- **Row-Level Security (RLS):** Your key = only you can access your data
- **No employee access:** MAROL staff cannot view your corpus content (only metadata like file count, size)

---

## 🗑️ Manual Deletion (Right to Erasure)

**You can delete your data anytime:**
- Via `/workspace` → "Delete Corpus" or "Delete All Data"
- Via email: [vinod.sridharan@txvault.app](mailto:vinod.sridharan@txvault.app?subject=Data%20Deletion%20Request)

**Deletion is immediate and irreversible.**

---

## Medical Content and HIPAA

### User Responsibility
If you upload medical documents containing Protected Health Information (PHI):
1. You are responsible for HIPAA compliance
2. You warrant you have permission to upload these documents
3. You understand MAROL extracts information but does not provide medical advice

### MAROL's Protections
- ✅ Encryption at rest (Supabase)
- ✅ Encryption in transit (TLS/HTTPS)
- ✅ Access controls (RLS in Supabase)
- ✅ Automatic deletion per retention policy

### HIPAA-Compliant Collaborator Access
For HIPAA-compliant medical use cases:
- Contact us for Business Associate Agreement (BAA)
- Custom retention policies available
- Enhanced audit logging
- Dedicated workspace isolation

**Email**: vinod.sridharan@txvault.app  
**Subject**: MAROL Collaborator - HIPAA Medical Use Case

TESTING SCENARIO:

Upload medical document (e.g., lab_results.pdf)

Test ALLOWED question: "What cholesterol levels are shown in my lab results?"

Expected: Extract and display the values

Test REJECTED question: "Should I be worried about my cholesterol?"

Expected: "I can tell you what your lab results say, but I cannot provide medical advice. Please consult your doctor."

Verify disclaimer: Medical answers should include disclaimer footer

---

## 📜 Legal Compliance

This policy complies with:
- **GDPR** (EU): Right to erasure, data portability
- **CCPA** (California): Right to delete, right to know

**Data location:** Supabase (US-based cloud), Google Cloud Run (us-central1)

---

**Last Updated:** January 20, 2026

**Questions?** [vinod.sridharan@txvault.app](mailto:vinod.sridharan@txvault.app)
