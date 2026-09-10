<div align="center">

# 🚀 BAS Onboard AI Assistant — SIH 2026 (`SIH26174`)

**An edge-ready, real-time computer vision & deterministic FSM system for microgravity human-activity monitoring.**

[![Smart India Hackathon 2026](https://img.shields.io/badge/SIH-2026-orange.svg?style=for-the-badge)](https://sih.gov.in/)
[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-yellow.svg?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)

[Key Features](#key-features) • [System Architecture](#system-architecture) • [Getting Started](#getting-started) • [API Reference](#api-reference) • [Team](#team-members)

</div>

---

## 📌 Project Overview

The **BAS Onboard AI Assistant** is a full-stack MVP designed for onboard human-activity recognition (HAR) and deterministic experiment-sequence verification in microgravity environments (e.g., Space Stations, Orbital Laboratories).

By pairing **temporal computer vision heuristics** with a **strict Finite State Machine (FSM)**, the system ensures non-intrusive safety monitoring, procedure compliance, and real-time guidance for astronauts—all running completely offline with zero dependency on external cloud AI APIs..

---

## ✨ Key Features

* **🎥 Real-Time Human Activity Recognition (HAR):** Simulated pipeline combining object detection, pose estimation, and hand/object interaction tracking.
* **⚡ Deterministic FSM Engine:** Zero-hallucination sequence validation acting as the single source of truth for experiment protocol integrity.
* **📡 Real-Time Telemetry & Monitoring:** WebSockets push live frame metadata, confidence scores, state transitions, and safety metrics directly to the dashboard.
* **🛡️ Smart Safety Routing:** Automated trigger mechanisms for `CORRECT`, `WARNING`, and `SEQUENCE_VIOLATION` alerts with interactive operator acknowledgment.
* **🤖 Grounded Guidance Assistant:** Context-aware assistance constrained strictly to current state packets to eliminate AI hallucinations.
* **📊 Mission Control Dashboard:** Production-grade UI built with React, Vite, and Tailwind, featuring telemetry graphs, active alerts, and immutable audit logs.

---

## 🏗️ System Architecture
```

[ Camera / Video Feed ]
│
▼
[ Object Detection + Pose + Hand Tracking ]
│
▼
[ Temporal Frame Buffer & HAR Heuristics ]
│
▼
[ Deterministic Experiment FSM Engine ] ──(State Packet)──► [ Grounded Guidance ]
│                                                       │
▼                                                       ▼
[ Validation & Persistence (SQLite/PostgreSQL) ] ──────► [ FastAPI WebSocket Feed ]
│
▼
[ React Mission Control Dashboard ]
```
---

### Technical Workflow
1. **Perception:** Visual streams feed spatial coordinates into a multi-frame buffer.
2. **State Evaluation:** The FSM validates transitions against pre-defined mission execution graphs.
3. **Alert Dispatch:** Out-of-order execution instantly triggers localized alerts and populates audit logs.
4. **Interactive Dashboard:** Websocket connections maintain high-frequency telemetry updates on the frontend.

---

## 🖼️ Interface & Architecture Preview

### Architecture Pipeline
<p align="center">
  <img src="https://github.com/user-attachments/assets/68ac6aa1-2f98-4a06-a7b4-9c2336635c02" width="100%" alt="System Architecture Diagram" />
</p>

### Mission Control UI
<p align="center">
  <img src="https://github.com/user-attachments/assets/6b8e9ec8-4531-497e-b8b0-59c77cb7a109" width="48%" />
  <img src="https://github.com/user-attachments/assets/98d21dc3-fca8-4a4a-a0b9-3377f80fb59c" width="48%" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/367db155-76c4-4215-a6fc-b1bd6727194d" width="48%" />
  <img src="https://github.com/user-attachments/assets/79fb4439-ae61-482d-858a-0a5ac9cf1561" width="48%" />
</p>

---

## 🚀 Getting Started

> **Note:** Hardware accelerators and external AI API keys are **not required**. `DEMO_MODE` is enabled by default.

### Prerequisites
* **Python:** `v3.10+`
* **Node.js:** `v18+` & `npm`

---

### 1️⃣ Backend Setup

Clone the repository and navigate to the project directory:

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

Create and activate a Python virtual environment:

**Windows**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the backend dependencies:

```bash
pip install -r backend/requirements.txt
```

Start the FastAPI backend:

```bash
cd backend
uvicorn main:app --reload --port 8000
```

**Backend URLs**

* API: `http://127.0.0.1:8000`
* Interactive API Documentation: `http://127.0.0.1:8000/docs`

---

### 2. Frontend Setup

Open a **new terminal window** and navigate to the frontend directory:

```bash
cd frontend
npm install
npm run dev
```

The frontend will be available at:

```text
http://localhost:5173
```

The Vite development server automatically proxies the following requests to the backend running on port `8000`:

* `/api`
* `/health`
* `/ws`

---

## 🧪 Demo Scenarios

The Operations Dashboard includes three pre-seeded scenarios for testing the monitoring system.

Navigate to:

**Operations Dashboard → Live Monitoring**

Select one of the following scenarios:

| Scenario           | Description                                                                                   |
| ------------------ | --------------------------------------------------------------------------------------------- |
| **Nominal**        | Simulates normal protocol progression and automatically completes the `BAS-EXP-001` workflow. |
| **Low Confidence** | Simulates low detection certainty and triggers soft system warnings.                          |
| **Violation**      | Simulates protocol sequence violations and generates high-priority safety alerts.             |

Click **START SESSION** to explore:

* Real-time bounding-box overlays
* Dynamic guidance messages
* Activity detection events
* Live telemetry
* Event streaming logs
* Safety alerts

---

## ⚙️ Configuration

Create a `.env` file in the project root using `.env.example` as a template:

```bash
cp .env.example .env
```

### Environment Variables

| Variable                | Default                                 | Description                                                  |
| ----------------------- | --------------------------------------- | ------------------------------------------------------------ |
| `DATABASE_URL`          | `sqlite:///storage/space_monitoring.db` | Database connection URI. PostgreSQL is also supported.       |
| `DEMO_MODE`             | `True`                                  | Enables deterministic activity simulations.                  |
| `CONFIDENCE_THRESHOLD`  | `0.70`                                  | Minimum confidence threshold used by the FSM.                |
| `FRAME_BUFFER_SIZE`     | `16`                                    | Sliding-window size used for temporal inference.             |
| `INFERENCE_INTERVAL_MS` | `1000`                                  | Interval between simulated inference frames in milliseconds. |
| `SECRET_KEY`            | `development-key`                       | Secret key used for session encryption.                      |

> **Note:** For production deployments, replace development credentials and secrets with secure values.

---

## 🔌 API Reference

| Method | Endpoint                          | Description                                                        |
| ------ | --------------------------------- | ------------------------------------------------------------------ |
| `GET`  | `/health`                         | Returns the system health status.                                  |
| `GET`  | `/api/v1/dashboard`               | Returns aggregated mission-control statistics.                     |
| `GET`  | `/api/v1/experiments`             | Fetches active experiment catalogs.                                |
| `POST` | `/api/v1/monitoring/start`        | Initializes a Human Activity Recognition (HAR) monitoring session. |
| `POST` | `/api/v1/monitoring/stop/{id}`    | Terminates an active monitoring session.                           |
| `GET`  | `/api/v1/alerts/summary`          | Returns consolidated alert counts and severity levels.             |
| `POST` | `/api/v1/alerts/{id}/acknowledge` | Acknowledges an active safety alert.                               |
| `POST` | `/api/v1/assistant/chat`          | Sends a query to the grounded protocol assistant.                  |
| `WS`   | `/ws/monitoring`                  | Provides real-time monitoring telemetry through WebSocket.         |

---

## 🐳 Docker Deployment

Docker support is pre-configured for containerized deployments.

Build and start the complete system using Docker Compose:

```bash
docker-compose up --build
```

The deployment configuration includes:

* Backend Dockerfile
* Frontend Dockerfile
* Nginx-based frontend serving
* Production database configuration
* Database schema at `database/schema.sql`

---

## 👥 Development Team

Developed with ❤️ for **Smart India Hackathon 2026** (`SIH26174`).

| Team Member | Role / Focus Area | GitHub / Profile |
| :--- | :--- | :---: |
| **Prajusha Dhar** | Team Lead / AI & Computer Vision | [@github](https://github.com) |
| **Rudranil Goswami** | Backend Engineer & Systems Architecture | [@github](https://github.com) |
| **Soubhagya Kabiraj** | Full-Stack & UI/UX Development | [@github](https://github.com) |
| **Sahana Basu** | Data Engineering & FSM Logic | [@github](https://github.com) |
| **Sougata Nandi** | DevOps & Embedded Systems Integration | [@github](https://github.com) |
| **Subhodip Sinha** | Quality Assurance & System Validation | [@github](https://github.com) |

---

## 📜 License

This project is distributed under the **MIT License**.

See the [`LICENSE`](LICENSE) file for more information.
