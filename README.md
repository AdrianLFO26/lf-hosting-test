# LightForce Hosting Test - Firebase POC

## 🎯 Purpose

Testing project to validate **HIPAA-compliant** hosting architecture for LightForce applications before migrating production apps.

**Problem:** Current Render-hosted apps don't pass IT security requirements (HIPAA compliance for patient data).

**Solution:** Test Firebase + Angular + FastAPI stack to ensure IT approval.

---

## 📋 Checklist Progress (18 Tasks)

### Phase 1: Base Setup (Tasks 1-5)
- [x] **Task 1:** Create official GitHub repository ✅
- [ ] **Task 2:** Simple local Angular app
- [ ] **Task 3:** Firebase account (@lightforceortho.com)
- [ ] **Task 4:** Deploy Angular to Firebase Hosting
- [ ] **Task 5:** CI/CD with GitHub Actions

### Phase 2: Backend + Databricks (Tasks 6-10)
- [ ] **Task 6:** FastAPI server locally
- [ ] **Task 7:** Deploy FastAPI to Cloud Run/Functions
- [ ] **Task 8:** Update CI/CD to deploy server
- [ ] **Task 9:** Connect server → Databricks
- [ ] **Task 10:** CI/CD secrets (Databricks credentials)

### Phase 3: First Functional App (Task 11)
- [ ] **Task 11:** Simple dashboard with real data

### Phase 4: Production Ready (Tasks 12-14)
- [ ] **Task 12:** Risk assessment for IT (Jayke)
- [ ] **Task 13:** Custom domain
- [ ] **Task 14:** Sub-applications routing

### Phase 5: Advanced Features (Tasks 15-18)
- [ ] **Task 15:** Google OAuth (@lightforceortho.com only)
- [ ] **Task 16:** AI Bedrock access (optional)
- [ ] **Task 17:** Database (Firestore/Cloud SQL if needed)
- [ ] **Task 18:** Complete documentation

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────┐
│  Angular Frontend (Firebase Hosting)    │
│  - Dashboard UI                          │
│  - Google OAuth @lightforceortho.com     │
│  - Client-side routing                   │
└──────────────┬──────────────────────────┘
               │ HTTPS
               ▼
┌─────────────────────────────────────────┐
│  FastAPI Backend (Cloud Run/Functions)   │
│  - Databricks OAuth M2M                  │
│  - SQL queries                           │
│  - Business logic                        │
└──────────────┬──────────────────────────┘
               │ OAuth
               ▼
┌─────────────────────────────────────────┐
│  Databricks SQL Warehouse               │
│  - analytics.accounts_and_revenue.*      │
│  - Patient data (HIPAA protected)        │
└─────────────────────────────────────────┘
```

---

## 🔒 Security Requirements

- ✅ No data stored on external servers
- ✅ Firebase/GCP (HIPAA Business Associate Agreement eligible)
- ✅ OAuth M2M for Databricks (service principal, no user credentials)
- ✅ Google OAuth for users (only @lightforceortho.com)
- ✅ No transit through non-compliant services

---

## 📚 Reference Documentation

- [LightForce Google Auth Standard](../.docs/LIGHTFORCE_GOOGLE_AUTH.md)
- [Databricks Reference](../idb-quality-webapp/DATABRICKS_REFERENCE.md)
- [Deployment Notes](../idb-quality-webapp/DEPLOYMENT_NOTES.md)

---

## 🚀 Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Angular 18 (LTS) |
| Backend | FastAPI (Python) |
| Hosting | Firebase Hosting |
| Compute | Cloud Run / Cloud Functions |
| Auth | Google OAuth 2.0 |
| Data | Databricks SQL Warehouse |
| CI/CD | GitHub Actions |

---

## 📊 Timeline Estimate

| Phase | Hours | Outcome |
|-------|-------|---------|
| Phase 1 | 4-6 | Angular on Firebase with CI/CD |
| Phase 2 | 8-12 | Backend + Databricks working |
| Phase 3 | 4-6 | Dashboard with real data |
| Phase 4 | 6-10 | Production-ready (IT approval) |
| Phase 5 | 15-20 | Advanced features |
| **Total** | **37-54 hrs** | Complete POC + documentation |

---

## 🎯 Success Criteria

This POC is successful when:

1. ✅ Angular app deployed to Firebase Hosting
2. ✅ FastAPI backend on Cloud Run querying Databricks
3. ✅ Google OAuth restricting to @lightforceortho.com
4. ✅ Jayke (IT) approves security architecture
5. ✅ Documentation complete for replicating in production apps

---

## 👥 Team

- **Adrian Jimenez** - Development
- **Amos** - Development
- **Jayke** - IT/Security Approval

---

## 📝 Notes

- This is a **learning/testing project** - not production
- Goal: validate process before migrating existing apps (metal-ceramic-tracker, idb-quality, etc.)
- Once approved → apply same architecture to all LightForce analytics apps
