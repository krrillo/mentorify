---
title: System Architecture — Mentorify Kids
description: Technical architecture and system design for the Mentorify Kids bilingual speech therapy platform.
version: 1.0
last_updated: 2025-10-20
---

# 🧩 System Architecture

## 🧱 Overview
Mentorify Kids is an AI-driven, bilingual therapy system that integrates **Speech-to-Speech**, **Whisper Turbo transcription**, and **GPT-4o** reasoning into a secure, accessible web platform.

It’s composed of 3 main layers:
1. **Frontend (Next.js)** — user interface and avatar interaction.
2. **Backend (Express + Prisma)** — API, business logic, and database operations.
3. **AI Layer (OpenAI + Whisper Turbo)** — speech streaming, transcription, and feedback generation.

---

## 🏗️ High-Level Diagram
```
+----------------------------+
|        Frontend (Next.js)  |
|----------------------------|
|  AvatarSession Component   |
|  LanguageContext Provider  |
|  Therapy UI / Feedback UI  |
+--------------+-------------+
               |
               v
+--------------+-------------+
|        Backend (Express)   |
|----------------------------|
|  /api/auth                 |
|  /api/ai/speech            |
|  /api/ai/transcribe        |
|  /api/feedback             |
|                            |
| Prisma ORM  → PostgreSQL    |
+--------------+-------------+
               |
               v
+--------------+-------------+
|       AI Integrations      |
|----------------------------|
|  GPT-4o (dialogue logic)   |
|  Whisper Turbo (speech)    |
|  Speech-to-Speech Engine   |
+----------------------------+
```

---

## 🌐 Modules and Responsibilities

### 🧩 Frontend (Next.js + React)
| Module | Description |
|---------|-------------|
| `components/` | UI elements and therapy widgets |
| `hooks/` | Speech streaming, session control |
| `contexts/LanguageContext` | EN/ES switching |
| `services/` | API calls to backend |
| `pages/` | Routes (login, therapy, dashboard) |

### ⚙️ Backend (Node.js + Express)
| Module | Description |
|---------|-------------|
| `controllers/` | REST API endpoints |
| `services/` | AI logic and business operations |
| `models/` | Prisma ORM schema |
| `ai/` | GPT-4o, Whisper Turbo, Speech2Speech integrations |
| `utils/` | Validation, error handling, logging |

### 🧠 AI Layer
| Service | Function |
|----------|-----------|
| **Whisper Turbo** | Transcribes bilingual audio streams |
| **GPT-4o** | Contextual understanding and dialogue adaptation |
| **Speech-to-Speech** | Generates empathetic, natural therapist voice |

---

## 🧩 Database Schema (Conceptual)
| Table | Description |
|--------|-------------|
| `users` | Parents, children, and therapist accounts |
| `sessions` | Speech therapy sessions metadata |
| `feedback` | Pronunciation and progress scores |
| `languages` | EN/ES configurations |
| `logs` | AI call metadata (sessionId, tokensUsed, timestamp) |

---

## 🔐 Security and Compliance
- JWT authentication for all sessions.  
- API keys stored in environment variables (`process.env.OPENAI_API_KEY`).  
- Data encrypted in transit (HTTPS) and at rest (PostgreSQL encryption).  
- Full compliance with **GDPR** and **COPPA** (for children’s data).  

---

## 🚀 Deployment Architecture
| Layer | Environment |
|--------|--------------|
| Frontend | Next.js on Vercel or AWS Amplify |
| Backend | AWS EC2 / Docker |
| Database | AWS RDS (PostgreSQL) |
| Storage | AWS S3 (for audio & subtitles) |
| Automation | n8n (workflow orchestration & webhook processing) |

---

## 🧩 CI/CD Pipeline (Proposed)
| Step | Description |
|-------|-------------|
| **Lint & Test** | Run ESLint, Jest, and Playwright tests |
| **Build** | Compile frontend and backend |
| **Deploy** | Push Docker images to ECR, auto-deploy via EC2 |
| **Docs Sync** | Auto-suggest updates in `memory-bank` after merges |

---

## 🧠 AI Context Flow
```
User Speech → Whisper Turbo → Text
Text → GPT-4o → Therapeutic Response
Response → Speech-to-Speech → Voice Output
Voice Output + Subtitles → Frontend (Avatar)
```

---

## 📊 Observability
- **Logs:** Winston (backend), browser console (frontend).  
- **Metrics:** Prometheus / OpenTelemetry.  
- **Alerts:** Slack or email via n8n automation.  

---

## 🧩 Future Extensions
- Real-time emotion detection via OpenAI Vision.  
- Adaptive difficulty for exercises based on pronunciation accuracy.  
- Therapist dashboard for progress analytics.  

---

## 🧾 Review Log
| Date | Change | Author |
|------|---------|---------|
| 2025-10-20 | Created architecture base | Cursor AI |
| — | — | — |
