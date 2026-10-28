# EtlabPro

<!-- documentation-navigation -->
[Developer guide](docs/PROJECT_GUIDE.md) · [Source reference](docs/REFERENCE.md) · [Contributing](CONTRIBUTING.md)
<!-- /documentation-navigation -->


<img src="frontend/assets/images/splash-icon.png" alt="EtlabPro app icon" width="120" align="right" />

EtlabPro is a full-stack student companion platform for Sahrdaya ETLAB users. It combines a production-oriented FastAPI backend, ETLAB scraping workflows, Supabase persistence, and a Flutter mobile app with rich analytics across attendance, internal marks, semester results, monthly calendar view, and timetable.

<br clear="right" />

## What EtlabPro Does

- Authenticates with ETLAB and syncs academic data into normalized storage.
- Serves a secure API for mobile consumption.
- Provides mobile dashboards for:
  - Home insights (attendance + result summaries)
  - Attendance tracking and risk analysis
  - CAT result breakdown with projection analysis
  - University end-sem result history by semester
  - Day-wise timetable and monthly attendance calendar

## Architecture Overview

Backend responsibilities:

- FastAPI API surface for auth, sync, live comparison, and analytics reads.
- Scrapers for profile, attendance, marks, timetable, and university results.
- Service layer orchestration that controls refresh policies and sync lifecycle.
- Supabase persistence through dedicated DB modules.

Frontend responsibilities:

- Secure login/session handling.
- JWT-backed API calls to protected endpoints.
- Local cached state for resilience and faster UX.
- Light and dark themed UI for all major student workflows.

## Current Deployment (Self-Hosted)

EtlabPro is currently self-hosted in Bangalore on a Dokploy setup.

Current hosting posture:

- Containerized backend deployment (FastAPI/Uvicorn) managed via Dokploy.
- Environment-driven secret management for runtime configuration.
- Public API exposure through a controlled self-hosted infrastructure boundary.
- Security-oriented backend defaults (JWT auth, CORS allow-list, reduced logging, docs disabled in production mode).

This gives you direct infrastructure control while keeping the application safely self-hosted and maintainable.

## Security and Safety

EtlabPro is designed with a safe-by-default backend model when operated with correct deployment practices.

Implemented in code:

- JWT access/refresh token flow for authenticated access.
- Protected routes enforced via Bearer token dependency checks.
- CORS origin restrictions from environment configuration.
- Supabase service role key only used server-side.
- Mobile credentials/tokens stored with encrypted secure storage.
- Production docs disabled by default.
- Concise operational logging to reduce sensitive signal leakage.

Operational best practices to keep it safe over time:

- Keep all secrets in environment variables and rotate them periodically.
- Enforce HTTPS end-to-end in front of Dokploy-managed services.
- Restrict DB and admin access by network and role.
- Monitor auth failures, sync anomalies, and dependency updates.

## Repository Layout

```text
EtlabPro/
  Backend/
    app/
      api/        # FastAPI routes + auth deps
      scraper/    # ETLAB scraping modules
      db/         # Supabase read/write modules
      services/   # Sync orchestration
      models/     # Pydantic schemas
    docs/dbms/    # Canonical schema + migration plan
    requirements.txt
    Dockerfile
  frontend/
    lib/
      screens/
      services/
      core/
      widgets/
    assets/images/
    pubspec.yaml
```

## Setup

### Backend

```powershell
cd Backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
copy .env.example .env
uvicorn app.main:app --reload --port 8000
```

- Health endpoint: `GET /health`
- API base: `/api/v1`

### Frontend

Create `frontend/.env`:

```env
API_BASE_URL=http://10.0.2.2:8000
APP_VERSION=1.0.0
```

Run app:

```powershell
cd frontend
flutter pub get
flutter run
```

## Screenshot Gallery (Analyzed)

The following screenshots are arranged by feature, with Light and Dark mode shown side-by-side.

| Feature | Light | Dark |
|---|---|---|
| <sub>Home</sub> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.25%20AM.jpeg" alt="Light Home" width="260" /> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.27%20AM%20(2).jpeg" alt="Dark Home" width="260" /> |
| <sub>Attendance Analysis</sub> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.25%20AM%20(1).jpeg" alt="Light Attendance Analysis" width="260" /> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.28%20AM.jpeg" alt="Dark Attendance Analysis" width="260" /> |
| <sub>CAT Results</sub> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.26%20AM.jpeg" alt="Light CAT Results" width="260" /> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.28%20AM%20(2).jpeg" alt="Dark CAT Results" width="260" /> |
| <sub>End-Sem Results</sub> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.26%20AM%20(1).jpeg" alt="Light End Sem" width="260" /> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.29%20AM%20(1).jpeg" alt="Dark End Sem" width="260" /> |
| <sub>Monthly Calendar</sub> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.26%20AM%20(2).jpeg" alt="Light Monthly Calendar" width="260" /> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.28%20AM%20(1).jpeg" alt="Dark Monthly Calendar" width="260" /> |
| <sub>Grade Analysis</sub> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.27%20AM.jpeg" alt="Light Grade Analysis" width="260" /> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.29%20AM.jpeg" alt="Dark Grade Analysis" width="260" /> |
| <sub>Timetable</sub> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.27%20AM%20(1).jpeg" alt="Light Timetable" width="260" /> | <img src="frontend/assets/images/WhatsApp%20Image%202026-04-12%20at%209.03.29%20AM%20(2).jpeg" alt="Dark Timetable" width="260" /> |

## API Coverage Summary

Public endpoints:

- `POST /api/v1/auth/login`
- `POST /api/v1/auth/refresh`
- `GET /api/v1/meta/latest-version`
- `GET /health`

Protected endpoints include:

- full sync + attendance-only update
- live attendance/monthly/updates workflows
- profile, attendance, marks, timetable, university results, summary
- departments, programmes, years, semesters, teachers metadata

## Notes

- This repository is actively developed.
- Database normalization and migration strategy are documented in `Backend/docs/dbms`.

<!-- developer-handbook-20261028 -->
[Developer guide](docs/PROJECT_GUIDE.md) · [Source reference](docs/REFERENCE.md) · [Verification and operations](docs/OPERATIONS.md)
<!-- /developer-handbook-20261028 -->
