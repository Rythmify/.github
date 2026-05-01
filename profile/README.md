# 🎵 Rythmify

> A SoundCloud-inspired social music streaming platform — built as a full-stack university Software Engineering project.

![Platform](https://img.shields.io/badge/platform-Web%20%7C%20Mobile-orange)
![Backend](https://img.shields.io/badge/backend-Node.js%20%2B%20Express.js-green)
![Frontend](https://img.shields.io/badge/frontend-React%2018%20%2B%20TypeScript-blue)
![Mobile](https://img.shields.io/badge/mobile-Flutter%20%2B%20Dart-cyan)
![Database](https://img.shields.io/badge/database-PostgreSQL%2016-336791)
![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-black)
![Cloud](https://img.shields.io/badge/cloud-Azure-0078D4)

---

## 📖 About

Rythmify is a full-featured music streaming platform supporting audio upload, social interaction, real-time messaging, playback, and premium subscriptions. It is developed across five parallel sub-teams — Backend, Frontend, Cross-Platform, Testing, and DevOps — following a structured phased delivery model.

The platform targets feature parity with SoundCloud, covering artist and listener roles, social graphs, waveform-timestamped comments, notifications, playlists, and an admin moderation dashboard.

---

## 🏗️ Repositories

| Repository | Description | Tech |
|---|---|---|
| [`backend`](https://github.com/Rythmify/backend) | RESTful API + Socket.IO server | Node.js, Express.js, PostgreSQL |
| [`frontend`](https://github.com/Rythmify/frontend) | Web application | React 18, TypeScript, Tailwind CSS, Zustand |
| [`cross`](https://github.com/Rythmify/cross) | iOS & Android app | Flutter, Dart, Riverpod |
| [`testing`](https://github.com/Rythmify/testing) | E2E, mobile, and performance test suites | Cypress, Appium, k6 |
| [`devops`](https://github.com/Rythmify/devops) | Infrastructure, CI/CD pipelines, Docker configs | GitHub Actions, Docker, Azure |

---

## 🧱 System Architecture

Rythmify follows a layered, service-oriented architecture across three client surfaces:

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                            │
│   React 18 (Web)       Flutter (iOS/Android)                    │
└───────────────────────────┬─────────────────────────────────────┘
                            │ REST + Socket.IO
┌───────────────────────────▼─────────────────────────────────────┐
│                      APPLICATION LAYER                          │
│   Node.js + Express.js API · Socket.IO (notifications, chat)    │
│   Layered: Routes → Controllers → Services → Models             │
└───────┬──────────────────────────────────────┬──────────────────┘
        │                                      │
┌───────▼──────────┐                  ┌────────▼─────────────────┐
│   DATA LAYER     │                  │   STORAGE LAYER          │
│   PostgreSQL 16  │                  │   Azure Blob Storage     │
│   (primary DB)   │                  │   (audio + media files)  │
└──────────────────┘                  └──────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                        DEVOPS LAYER                             │
│   GitHub Actions CI/CD · Docker · Azure Container Apps          │
│   Azure Static Web Apps · Azure PostgreSQL · Monitoring         │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Tech Stack

### Backend
- **Runtime:** Node.js + Express.js
- **Database:** PostgreSQL 16 (full-text search via `tsvector`, JSONB metadata)
- **Auth:** JWT (15-min access tokens) + refresh token rotation in `httpOnly` cookies
- **Real-Time:** Socket.IO (live notifications, 1-to-1 messaging)
- **File Storage:** Azure Blob Storage (audio + cover art; URLs stored in DB)
- **Payments:** Stripe SDK (mocked checkout flow)
- **API Spec:** OpenAPI 3.0 (`openapi.yaml` — shared contract across all teams)

### Frontend
- **Framework:** React 18 + TypeScript
- **Styling:** Tailwind CSS + CSS Variables
- **State:** Zustand (`auth`, `player`, `notifications` stores)
- **HTTP:** Axios (shared interceptors for auth headers + error handling)
- **Forms:** React Hook Form + Zod
- **Build:** Vite

### Cross-Platform
- **Framework:** Flutter + Dart
- **Architecture:** Clean Architecture (Data / Domain / Presentation)
- **State:** Riverpod
- **HTTP:** Dio (interceptors, retry logic)
- **Navigation:** GoRouter
- **Local Storage:** Hive / SharedPreferences

### Testing
- **Web E2E:** Cypress (Page Object Model, selector abstraction)
- **Mobile E2E:** Appium (Android + iOS automation)
- **Performance:** k6 (load, stress, and API throughput)
- **Task Tracking:** ClickUp

### DevOps
- **CI/CD:** GitHub Actions
- **Containerisation:** Docker + Docker Compose
- **Cloud:** Azure (Container Apps, Static Web Apps, ACR, Blob Storage, PostgreSQL)
- **Monitoring:** Grafana + internal resource monitoring

---

## 🗂️ Feature Modules

| # | Module |
|---|---|
| 1 | Authentication & User Management |
| 2 | User Profile & Social Identity |
| 3 | Followers & Social Graph |
| 4 | Audio Upload & Track Management |
| 5 | Playback & Streaming |
| 6 | Engagement & Social Interactions |
| 7 | Playlists & Sets |
| 8 | Feed, Search & Discovery |
| 9 | Messaging & Track Sharing |
| 10 | Real-Time Notifications |
| 11 | Moderation & Admin Dashboard |
| 12 | Premium Subscription |

---

## 👥 Team

**Team Leader & DevOps Engineer:** Mohamed Alabasy

| Sub-Team | Leader | Members |
|---|---|---|
| Backend | Omar Hamza | Saja Aboulmagd, Omar Hamdy, Beshoy Maher, Alyaa Mohamed |
| Frontend | Nour | Mariam, Gamila, Shahd, Farah, Rowida |
| Cross-Platform | Bassel Alaa | Sohaila, Hana, Rana, Karim |
| Testing | Ahmed Attay Kamal | Yomna Eweida |
| DevOps | Mohamed Alabasy | — |

---

## 📡 API

The full API is documented as an OpenAPI 3.0.3 specification (`openapi.yaml`) in `rythmify-backend`.

| Environment | Base URL |
|---|---|
| Development | `https://rythmify-backend-dev.livelypebble-6b7965ef.uaenorth.azurecontainerapps.io/health` |
| Production | `https://rythmify-back.duckdns.org/health` |

**Rate Limits**
- General API: 100 requests / 15 min
- Auth endpoints: 5 requests / 15 min
- File uploads: 20 requests / hour

**File Upload Limits**
- Audio: 100 MB max (MP3, WAV, FLAC, AAC)
- Avatar / Cover Photo: 5 MB (JPG, PNG, WEBP)

---

## 🔄 Development Phases

| Phase | Description | Status |
|---|---|---|
| Phase 0 | Tools, languages, team structure, repo/task setup | ✅ Complete |
| Phase 1 | Task division, code styles, system design, API docs, ERD | ✅ Complete |
| Phase 2 | 20% implementation milestone | ✅ Complete |
| Phase 3 | 50% completion + deployed prototype | ✅ Complete |
| Phase 4 | 100% completion + final deliverables | ✅ Complete |

---

## 🛠️ Local Development

Each repo contains its own setup guide. The DevOps repo provides a unified Docker Compose environment for local development.

```bash
# Clone the DevOps repo for local environment setup
git clone https://github.com/Rythmify/devops
cd devops

# Start all services (backend, frontend, database, Azurite blob emulator)
docker compose up
```

See [`devops/README.md`](https://github.com/Rythmify/devops) for full local setup instructions, environment variable templates, and service port mappings.

---

## 📋 Branching & Contribution

- `main` — production-ready code only; protected branch
- `dev` — integration branch for all feature work
- Feature branches follow the pattern: `feature-<short-description>`
  - Example: `feature-trending-feed`, `feature-player-controls`

All PRs require review before merging into `dev`. Huge commits are forbidden — keep changes focused and atomic.

---

## 📄 License

This project is developed for academic purposes as part of a university Software Engineering course.

---

*Rythmify · Phase 4 Complete · Built with ❤️ by a team of 19*
