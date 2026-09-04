# LIFELINK — Agentic AI Emergency Response & Coordination Platform
*Production-oriented emergency coordination infrastructure localized for Pune Metropolitan Area, Maharashtra, India.*

---

## 🚀 Live Localhost Access Links

The platform is currently running live on your system:

| Service / Interface | Direct Localhost Link | Description |
| :--- | :--- | :--- |
| **Operational Dispatch Console** | [http://localhost:8000](http://localhost:8000) | Main clinical UI (Emergency intake, Pune digital twin grid, 108 fleet radar, ICU loss injection) |
| **Interactive API Documentation** | [http://localhost:8000/docs](http://localhost:8000/docs) | Swagger UI for interactive testing of all REST endpoints |
| **Alternative API Reference** | [http://localhost:8000/redoc](http://localhost:8000/redoc) | ReDoc API specification viewer |
| **Platform Health Check** | [http://localhost:8000/health](http://localhost:8000/health) | System health, active maps provider, simulation loop state |
| **Pune Hospitals Digital Twin** | [http://localhost:8000/api/v1/hospitals](http://localhost:8000/api/v1/hospitals) | Live JSON feed of all 14 Pune hospitals with bed availability |
| **Pune EMS Fleet Telematics** | [http://localhost:8000/api/v1/ambulances](http://localhost:8000/api/v1/ambulances) | Live JSON feed of 12 active Pune ambulances (8 BLS, 4 ALS) |
| **Emergencies Intake & Log** | [http://localhost:8000/api/v1/emergencies](http://localhost:8000/api/v1/emergencies) | Active incident records and chronological audit timelines |
| **Demo JWT Auth Tokens** | [http://localhost:8000/api/v1/auth/demo-tokens](http://localhost:8000/api/v1/auth/demo-tokens) | Instant JWT tokens for all 5 roles (Caller, Paramedic, Dispatcher, ED Nurse, Admin) |
| **Real-time Telemetry Stream** | `ws://localhost:8000/ws` | WebSocket pub/sub channel for live GPS, bed changes, and alerts |

---

## 🚨 India & Pune Emergency Numbers (Always Active)

- **112**: India's Unified National Emergency Helpline
- **108**: Maharashtra Free Emergency Ambulance Service (EMRI-operated)
- **102**: Free Maternal & Infant Transport Helpline
- **100**: Police | **101**: Fire

---

## ⚡ How to Start the Server

To launch or restart the platform at any time:
```powershell
cd C:\Users\PARTH\.gemini\antigravity\scratch\lifelink
python run.py
```
Open [http://localhost:8000](http://localhost:8000) in your web browser.

---

## 🧪 How to Run Automated Tests

To run the complete automated test suite:
```powershell
cd C:\Users\PARTH\.gemini\antigravity\scratch\lifelink
python -m pytest backend/tests -v
```

---

## 📂 Master File Directory & Project Architecture

The architecture enforces strict layering:
```
UI -> API -> Orchestrator -> Agents -> Tools -> External Integration Adapters -> Database
```

### 1. Root Configuration & Project Standards
- [`AGENTS.md`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/AGENTS.md) — Non-negotiable safety guardrails (no autonomous medical diagnosis), UTC storage with IST display, Indian EMS rules.
- [`PROJECT_INDEX.md`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/PROJECT_INDEX.md) — Comprehensive technical file catalog with line counts and export signatures.
- [`run.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/run.py) — Root application bootstrapper and Uvicorn server launcher.
- [`requirements.txt`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/requirements.txt) — Production Python package dependencies.
- [`.env.example`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/.env.example) — Environment configuration template.

### 2. Backend Application Core
- [`backend/app/main.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/main.py) — FastAPI application entrypoint, lifespan startup/shutdown, CORS, and static file mount.
- [`backend/app/core/config.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/core/config.py) — Pydantic Settings, Pune center coordinates (`18.5204`, `73.8567`), maps provider configs.
- [`backend/app/core/database.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/core/database.py) — Async SQLAlchemy database engine, session factory, UTC timestamp mixin.
- [`backend/app/core/security.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/core/security.py) — RBAC (5 roles), bcrypt hashing, JWT access token issuance and validation.

### 3. Database Models (Async SQLAlchemy)
- [`backend/app/models/user.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/models/user.py) — User account table for role-based authorization.
- [`backend/app/models/hospital.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/models/hospital.py) — Hospital digital twin table (real lat/lng, specialties, ICU and ED beds).
- [`backend/app/models/ambulance.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/models/ambulance.py) — Ambulance fleet telematics table (BLS vs ALS, coordinates, heading, speed).
- [`backend/app/models/emergency.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/models/emergency.py) — Emergency incident case table and chronological `TimelineEvent` table.
- [`backend/app/models/audit.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/models/audit.py) — Immutable `AuditLog` table capturing every agent action and tool call.

### 4. Pydantic Validation Schemas
- [`backend/app/schemas/auth.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/schemas/auth.py) — Login, token, and user profile schemas.
- [`backend/app/schemas/hospital.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/schemas/hospital.py) — Hospital telemetry and capacity mutation schemas.
- [`backend/app/schemas/ambulance.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/schemas/ambulance.py) — Fleet telemetry and status update schemas.
- [`backend/app/schemas/emergency.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/schemas/emergency.py) — Emergency intake, timeline, and human confirmation gate schemas.
- [`backend/app/schemas/audit.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/schemas/audit.py) — Immutable audit log recording schemas.

### 5. Pluggable Integration Adapters Layer
- [`backend/app/adapters/base.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/adapters/base.py) — Abstract Base Classes (`MapsAdapter`, `HospitalAdapter`, `FleetAdapter`).
- [`backend/app/adapters/maps_adapter.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/adapters/maps_adapter.py) — Real geography integration: OSM Nominatim geocoding and OSRM road routing engine.
- [`backend/app/adapters/hospital_adapter.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/adapters/hospital_adapter.py) — Hospital telemetry integration with staleness tracking.
- [`backend/app/adapters/fleet_adapter.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/adapters/fleet_adapter.py) — Fleet AVL / CAD telematics integration.

### 6. Pune Digital Twin & City Simulation Engine
- [`backend/app/simulation/seed_data.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/simulation/seed_data.py) — 14 real Pune hospitals (Sassoon, Ruby Hall, Jehangir, Deenanath, KEM, Sahyadri, etc.) and 12 ambulances (8 BLS, 4 ALS).
- [`backend/app/simulation/engine.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/simulation/engine.py) — Asynchronous background loop (3.0s tick) and dynamic event injection engine.

### 7. REST & WebSocket API (v1)
- [`backend/app/api/v1/auth.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/api/v1/auth.py) — `/login`, `/me`, and `/demo-tokens` endpoints.
- [`backend/app/api/v1/hospitals.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/api/v1/hospitals.py) — Hospital queries and bed capacity updates.
- [`backend/app/api/v1/ambulances.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/api/v1/ambulances.py) — Fleet queries and telematics updates.
- [`backend/app/api/v1/emergencies.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/api/v1/emergencies.py) — Emergency intake, timeline queries, and human confirmation gate.
- [`backend/app/api/v1/simulation.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/api/v1/simulation.py) — Scenario injection endpoints (e.g. ICU drop, traffic delay).
- [`backend/app/api/v1/ws.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/api/v1/ws.py) — Centralized WebSocket connection manager and event broadcaster.

### 8. User Interface (High-Contrast Operational Console)
- [`backend/app/static/index.html`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/app/static/index.html) — Trilingual clinical console (English, Marathi, Hindi), live Pune hospital grid, 108 ambulance radar, and Section 10 scenario triggers.

### 9. Automated Test Suite
- [`backend/tests/test_foundation.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/tests/test_foundation.py) — Tests security hashing, JWT, and Pune database seeding.
- [`backend/tests/test_adapters.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/tests/test_adapters.py) — Tests real Pune geocoding, OSRM routing, and hospital/fleet adapters.
- [`backend/tests/test_emergency_flow.py`](file:///C:/Users/PARTH/.gemini/antigravity/scratch/lifelink/backend/tests/test_emergency_flow.py) — Tests emergency intake, audit log creation, human confirmation, and ICU drop injection.
