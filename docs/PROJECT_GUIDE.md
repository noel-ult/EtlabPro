# EtlabPro development guide

A Flutter student app backed by FastAPI, ETLAB scraping, and Supabase persistence. The server synchronizes attendance, marks, profile, timetable, and university results for Sahrdaya ETLAB accounts.

## Backend setup

Use Python 3.12 to match the Docker image. Copy `Backend/.env.example` to `Backend/.env` and set `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`, and a stable random `JWT_SECRET`. The fallback JWT secret is generated at process import, so restarting without a fixed secret invalidates tokens and can make multiple workers disagree.

Review `Backend/docs/dbms/README.md` and the canonical schema/migration notes before initializing a disposable Supabase project. Keep the service-role key exclusively on the backend.

```sh
cd Backend
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/uvicorn app.main:app --reload --port 8000
```

Set `ENV=development` in `Backend/.env` to enable `/docs`, `/redoc`, and `/openapi.json`. `/health` is public; application routes mount at `/api/v1`.

## Flutter setup

Use Flutter with a Dart SDK satisfying `^3.11.0` from `frontend/pubspec.yaml`. Create `frontend/.env` because it is declared as a bundled asset:

```dotenv
API_BASE_URL=http://localhost:8000
APP_VERSION=1.0.0
```

```sh
cd frontend
flutter pub get
flutter run
```

Use the backend origin without `/api/v1`; `AppConstants.apiV1` appends that path. Android replaces localhost with emulator host `10.0.2.2`; physical devices need the host's LAN address. Build-time `API_BASE_URL` and `APP_VERSION` defines are fallbacks behind values in `.env`.

## Architecture and operation

`Backend/app/api/routes.py` defines the HTTP contract, `services/sync.py` coordinates refreshes, `scraper/` handles ETLAB pages, and `db/` stores normalized data. The Flutter client has API/auth services, cached student data, screen-specific analytics, and a version gate. Login/refresh issue JWTs; protected student requests require Bearer tokens and route-specific ownership checks.

Refresh-age settings in `Backend/app/config.py` independently control data categories; attendance defaults to two hours and several others to seven days. `LATEST_FRONTEND_VERSION` can enforce a client version. Changing ETLAB HTML may require scraper updates even when your API has not changed.

## Checks and deployment

Use `flutter analyze` and inspect the tracked widget test before `flutter test`; no backend automated test directory is tracked. Test login, sync, cached/offline rendering, and token refresh with an authorized test account. Never publish student exports or credentials as fixtures.

`Backend/Dockerfile` packages the API and exposes port 8000 with a `/health` check. It does not deploy the Flutter app or create database tables. Existing API references and DB diagrams are linked from the source reference; compare historical endpoint lists with the current router when they differ.

## More documentation

- [Source, command, and configuration reference](REFERENCE.md)
- [Contributing](../CONTRIBUTING.md)
