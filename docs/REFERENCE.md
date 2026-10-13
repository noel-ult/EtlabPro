# EtlabPro source reference


Source reviewed: [`e91627720cc8`](https://github.com/noel-ult/EtlabPro/commit/e91627720cc8f7d6136295f2af4f5e5adbd327b7).

This reference records the checked-in source, scripts, configuration names, and route declarations. It is a navigation aid; service availability and successful test execution require separate verification.

## Configuration names

Names below are declared by source or example files. Example-only entries may be stale; consult the linked reader and project guide before relying on them. Secret values are intentionally omitted.

| Name | Declared/read in |
| --- | --- |
| `API_BASE_URL` | [Backend/scrape_all_to_txt.py](../Backend/scrape_all_to_txt.py) |
| `API_KEY` | [Backend/.env.example](../Backend/.env.example) |
| `ATTENDANCE_MAX_AGE_SECONDS` | [Backend/app/config.py](../Backend/app/config.py) |
| `ENV` | [Backend/.env.example](../Backend/.env.example), [Backend/app/main.py](../Backend/app/main.py) |
| `ETLAB_PASSWORD` | [Backend/.env.example](../Backend/.env.example), [Backend/scrape_all_to_txt.py](../Backend/scrape_all_to_txt.py) |
| `ETLAB_USERNAME` | [Backend/.env.example](../Backend/.env.example), [Backend/scrape_all_to_txt.py](../Backend/scrape_all_to_txt.py) |
| `FRONTEND_ORIGINS` | [Backend/.env.example](../Backend/.env.example), [Backend/app/config.py](../Backend/app/config.py) |
| `JWT_ACCESS_HOURS` | [Backend/app/config.py](../Backend/app/config.py) |
| `JWT_REFRESH_DAYS` | [Backend/app/config.py](../Backend/app/config.py) |
| `JWT_SECRET` | [Backend/app/config.py](../Backend/app/config.py) |
| `LATEST_FRONTEND_VERSION` | [Backend/app/config.py](../Backend/app/config.py) |
| `MARKS_MAX_AGE_SECONDS` | [Backend/app/config.py](../Backend/app/config.py) |
| `PROFILE_MAX_AGE_SECONDS` | [Backend/app/config.py](../Backend/app/config.py) |
| `REQUEST_TIMEOUT` | [Backend/app/config.py](../Backend/app/config.py) |
| `SUPABASE_SERVICE_ROLE_KEY` | [Backend/.env.example](../Backend/.env.example), [Backend/app/config.py](../Backend/app/config.py) |
| `SUPABASE_URL` | [Backend/.env.example](../Backend/.env.example), [Backend/app/config.py](../Backend/app/config.py) |
| `TIMETABLE_MAX_AGE_SECONDS` | [Backend/app/config.py](../Backend/app/config.py) |
| `UNI_RESULTS_MAX_AGE_SECONDS` | [Backend/app/config.py](../Backend/app/config.py) |

## HTTP route declarations

Paths are **as declared in each source file**. Router/blueprint mount prefixes from the entry point must be prepended; the project guide describes the active entry point and common prefixes. Alternate entry points (such as SQLite) are listed separately by file. Authentication, request bodies, and response schemas live in the linked handlers/models.

| Source | Method | Declared path | Handler |
| --- | --- | --- | --- |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/meta/latest-version` | `get_latest_version` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/auth/login` | `auth_login` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/auth/refresh` | `auth_refresh` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/sync-all` | `sync_all` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/update-attendance` | `update_attendance` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/live/attendance-duty-leave` | `get_live_attendance_with_duty_leave` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/live/attendance` | `get_live_attendance` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/live/monthly-attendance` | `get_live_monthly_attendance` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/live/attendance-metadata` | `get_attendance_metadata` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/live/monthly-attendance-simple` | `get_live_monthly_attendance_simple` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/live/monthly-attendance-advanced` | `get_live_monthly_attendance_advanced` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/live/monthly-attendance-all` | `get_live_monthly_attendance_all` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | POST | `/live/updates` | `get_live_updates` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/profile/{roll}` | `get_profile` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/internal-results/{roll}` | `get_internal_results` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/university-results/{roll}` | `get_university_results` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/timetable/{roll}` | `get_timetable` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/attendance/{roll}` | `get_attendance` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/subjects` | `get_subjects` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/summary/{roll}` | `get_summary` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/departments` | `get_departments` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/programmes` | `get_programmes` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/academic-years` | `get_academic_years` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/semesters` | `get_semesters` |
| [Backend/app/api/routes.py](../Backend/app/api/routes.py) | GET | `/teachers` | `get_teachers` |
| [Backend/app/main.py](../Backend/app/main.py) | GET | `/health` | `health` |

## Existing documentation

Historical plans/reports describe their own revision; use current source when they disagree.

- [Backend/docs/API_COMPLETE_REFERENCE.txt](../Backend/docs/API_COMPLETE_REFERENCE.txt)
- [Backend/docs/API_ENDPOINTS_REFERENCE.txt](../Backend/docs/API_ENDPOINTS_REFERENCE.txt)
- [Backend/docs/dbms/02_migration_plan.md](../Backend/docs/dbms/02_migration_plan.md)
- [Backend/docs/dbms/03_relationships.md](../Backend/docs/dbms/03_relationships.md)
- [Backend/docs/dbms/04_triggers_catalog.md](../Backend/docs/dbms/04_triggers_catalog.md)
- [Backend/docs/dbms/05_erd_mermaid.md](../Backend/docs/dbms/05_erd_mermaid.md)
- [Backend/docs/dbms/07_data_dictionary.md](../Backend/docs/dbms/07_data_dictionary.md)
- [Backend/docs/dbms/README.md](../Backend/docs/dbms/README.md)
- [Backend/requirements.txt](../Backend/requirements.txt)
- [README.md](../README.md)
- [frontend/README.md](../frontend/README.md)

## Source and configuration map

Generated lockfiles, binary assets, compiled output, vendored dependencies, and cached bytecode are omitted. Test files remain listed so coverage can be located.

- [Backend/.env.example](../Backend/.env.example)
- [Backend/Dockerfile](../Backend/Dockerfile)
- [Backend/app/__init__.py](../Backend/app/__init__.py)
- [Backend/app/api/__init__.py](../Backend/app/api/__init__.py)
- [Backend/app/api/deps.py](../Backend/app/api/deps.py)
- [Backend/app/api/routes.py](../Backend/app/api/routes.py)
- [Backend/app/config.py](../Backend/app/config.py)
- [Backend/app/db/__init__.py](../Backend/app/db/__init__.py)
- [Backend/app/db/attendance.py](../Backend/app/db/attendance.py)
- [Backend/app/db/client.py](../Backend/app/db/client.py)
- [Backend/app/db/marks.py](../Backend/app/db/marks.py)
- [Backend/app/db/profile.py](../Backend/app/db/profile.py)
- [Backend/app/db/reference_tables.py](../Backend/app/db/reference_tables.py)
- [Backend/app/db/students.py](../Backend/app/db/students.py)
- [Backend/app/db/sync_meta.py](../Backend/app/db/sync_meta.py)
- [Backend/app/db/timetable.py](../Backend/app/db/timetable.py)
- [Backend/app/db/university_results.py](../Backend/app/db/university_results.py)
- [Backend/app/etlab_sync_scraper.py](../Backend/app/etlab_sync_scraper.py)
- [Backend/app/main.py](../Backend/app/main.py)
- [Backend/app/models/__init__.py](../Backend/app/models/__init__.py)
- [Backend/app/models/schemas.py](../Backend/app/models/schemas.py)
- [Backend/app/scraper/__init__.py](../Backend/app/scraper/__init__.py)
- [Backend/app/scraper/attendance.py](../Backend/app/scraper/attendance.py)
- [Backend/app/scraper/marks.py](../Backend/app/scraper/marks.py)
- [Backend/app/scraper/profile.py](../Backend/app/scraper/profile.py)
- [Backend/app/scraper/session.py](../Backend/app/scraper/session.py)
- [Backend/app/scraper/timetable.py](../Backend/app/scraper/timetable.py)
- [Backend/app/scraper/university_results.py](../Backend/app/scraper/university_results.py)
- [Backend/app/services/__init__.py](../Backend/app/services/__init__.py)
- [Backend/app/services/sync.py](../Backend/app/services/sync.py)
- [Backend/docs/API_ENDPOINTS_REFERENCE.json](../Backend/docs/API_ENDPOINTS_REFERENCE.json)
- [Backend/docs/API_REFERENCE.json](../Backend/docs/API_REFERENCE.json)
- [Backend/docs/dbms/01_canonical_schema.sql](../Backend/docs/dbms/01_canonical_schema.sql)
- [Backend/docs/dbms/fix_cgpa_view.sql](../Backend/docs/dbms/fix_cgpa_view.sql)
- [Backend/docs/dbms/migration.sql](../Backend/docs/dbms/migration.sql)
- [Backend/docs/dbms/migration_v2_profile.sql](../Backend/docs/dbms/migration_v2_profile.sql)
- [Backend/requirements.txt](../Backend/requirements.txt)
- [Backend/scrape_all_to_txt.py](../Backend/scrape_all_to_txt.py)
- [frontend/analysis_options.yaml](../frontend/analysis_options.yaml)
- [frontend/lib/core/api_client.dart](../frontend/lib/core/api_client.dart)
- [frontend/lib/core/constants.dart](../frontend/lib/core/constants.dart)
- [frontend/lib/core/router.dart](../frontend/lib/core/router.dart)
- [frontend/lib/core/theme.dart](../frontend/lib/core/theme.dart)
- [frontend/lib/main.dart](../frontend/lib/main.dart)
- [frontend/lib/screens/app_shell.dart](../frontend/lib/screens/app_shell.dart)
- [frontend/lib/screens/attendance/widgets/analysis_tab.dart](../frontend/lib/screens/attendance/widgets/analysis_tab.dart)
- [frontend/lib/screens/attendance/widgets/attendance_tab.dart](../frontend/lib/screens/attendance/widgets/attendance_tab.dart)
- [frontend/lib/screens/attendance/widgets/duty_leave_tab.dart](../frontend/lib/screens/attendance/widgets/duty_leave_tab.dart)
- [frontend/lib/screens/attendance_screen.dart](../frontend/lib/screens/attendance_screen.dart)
- [frontend/lib/screens/home/widgets/attendance_summary_card.dart](../frontend/lib/screens/home/widgets/attendance_summary_card.dart)
- [frontend/lib/screens/home/widgets/data_loading_card.dart](../frontend/lib/screens/home/widgets/data_loading_card.dart)
- [frontend/lib/screens/home/widgets/error_view.dart](../frontend/lib/screens/home/widgets/error_view.dart)
- [frontend/lib/screens/home/widgets/next_class_card.dart](../frontend/lib/screens/home/widgets/next_class_card.dart)
- [frontend/lib/screens/home/widgets/profile_info_card.dart](../frontend/lib/screens/home/widgets/profile_info_card.dart)
- [frontend/lib/screens/home/widgets/purple_card.dart](../frontend/lib/screens/home/widgets/purple_card.dart)
- [frontend/lib/screens/home/widgets/results_overview_card.dart](../frontend/lib/screens/home/widgets/results_overview_card.dart)
- [frontend/lib/screens/home/widgets/shimmer_placeholder.dart](../frontend/lib/screens/home/widgets/shimmer_placeholder.dart)
- [frontend/lib/screens/home/widgets/sync_time.dart](../frontend/lib/screens/home/widgets/sync_time.dart)
- [frontend/lib/screens/home_screen.dart](../frontend/lib/screens/home_screen.dart)
- [frontend/lib/screens/login_screen.dart](../frontend/lib/screens/login_screen.dart)
- [frontend/lib/screens/marks/widgets/analysis_tab.dart](../frontend/lib/screens/marks/widgets/analysis_tab.dart)
- [frontend/lib/screens/marks/widgets/results_tab.dart](../frontend/lib/screens/marks/widgets/results_tab.dart)
- [frontend/lib/screens/marks_screen.dart](../frontend/lib/screens/marks_screen.dart)
- [frontend/lib/screens/monthly/widgets/monthly_sections.dart](../frontend/lib/screens/monthly/widgets/monthly_sections.dart)
- [frontend/lib/screens/monthly_attendance_screen.dart](../frontend/lib/screens/monthly_attendance_screen.dart)
- [frontend/lib/screens/profile_screen.dart](../frontend/lib/screens/profile_screen.dart)
- [frontend/lib/screens/timetable/widgets/analysis_tab.dart](../frontend/lib/screens/timetable/widgets/analysis_tab.dart)
- [frontend/lib/screens/timetable/widgets/timetable_tab.dart](../frontend/lib/screens/timetable/widgets/timetable_tab.dart)
- [frontend/lib/screens/timetable_screen.dart](../frontend/lib/screens/timetable_screen.dart)
- [frontend/lib/screens/uni_results/widgets/semester_page.dart](../frontend/lib/screens/uni_results/widgets/semester_page.dart)
- [frontend/lib/screens/uni_results_screen.dart](../frontend/lib/screens/uni_results_screen.dart)
- [frontend/lib/screens/updates/widgets/updates_sections.dart](../frontend/lib/screens/updates/widgets/updates_sections.dart)
- [frontend/lib/screens/updates_screen.dart](../frontend/lib/screens/updates_screen.dart)
- [frontend/lib/services/auth_service.dart](../frontend/lib/services/auth_service.dart)
- [frontend/lib/services/connectivity_service.dart](../frontend/lib/services/connectivity_service.dart)
- [frontend/lib/services/lock_service.dart](../frontend/lib/services/lock_service.dart)
- [frontend/lib/services/student_data.dart](../frontend/lib/services/student_data.dart)
- [frontend/lib/services/theme_notifier.dart](../frontend/lib/services/theme_notifier.dart)
- [frontend/lib/services/version_check_service.dart](../frontend/lib/services/version_check_service.dart)
- [frontend/lib/utils/attendance_analysis.dart](../frontend/lib/utils/attendance_analysis.dart)
- [frontend/lib/utils/next_class_analysis.dart](../frontend/lib/utils/next_class_analysis.dart)
- [frontend/lib/utils/results_analysis.dart](../frontend/lib/utils/results_analysis.dart)
- [frontend/lib/utils/timetable_analysis.dart](../frontend/lib/utils/timetable_analysis.dart)
- [frontend/lib/widgets/latest_version_guard.dart](../frontend/lib/widgets/latest_version_guard.dart)
- [frontend/lib/widgets/screen_parts.dart](../frontend/lib/widgets/screen_parts.dart)
- [frontend/pubspec.yaml](../frontend/pubspec.yaml)
- [frontend/test/widget_test.dart](../frontend/test/widget_test.dart)
