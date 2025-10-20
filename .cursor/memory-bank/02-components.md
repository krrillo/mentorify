---
title: Components Overview — Mentorify Kids
description: Detailed breakdown of the main software components (frontend, backend, AI integrations) for Mentorify Kids.
version: 1.0
last_updated: 2025-10-20
---

# 🧩 Components Overview

## 🎨 Frontend (Next.js + React)

### Core Responsibilities
- Provide a **bilingual user interface** (English/Spanish).
- Stream real-time audio input and output using WebRTC or WebSocket.
- Manage therapy session states and visualization of progress.
- Display animated **therapist avatar** with synchronized subtitles.
- Allow users (children or parents) to switch between **English and Spanish**.

### Folder Structure
```
frontend/
 ├── components/
 │    ├── AvatarSession.tsx
 │    ├── FeedbackPanel.tsx
 │    ├── ProgressChart.tsx
 │    └── LanguageSelector.tsx
 ├── hooks/
 │    ├── useSpeechStream.ts
 │    ├── useSession.ts
 │    └── useFeedback.ts
 ├── contexts/
 │    └── LanguageContext.tsx
 ├── services/
 │    └── api.ts
 ├── pages/
 │    ├── index.tsx
 │    ├── therapy.tsx
 │    └── dashboard.tsx
 └── styles/
      └── globals.css
```

### UI/UX Principles
- **Accessible Design (WCAG 2.1)** for children with language challenges.
- Responsive layout with playful but calm visuals.
- Use of **Lottie animations** for avatar emotion syncing.
- Each therapy session must end with **positive reinforcement messages**.

---

## ⚙️ Backend (Express + Prisma)

### Core Responsibilities
- Expose REST endpoints for the AI and session data.
- Log and validate all user and AI interactions.
- Handle secure WebSocket streaming for real-time communication.
- Manage user authentication and session tokens.
- Support multi-language settings for each child profile.

### Folder Structure
```
backend/
 ├── controllers/
 │    ├── aiController.ts
 │    ├── authController.ts
 │    └── feedbackController.ts
 ├── services/
 │    ├── aiService.ts
 │    ├── userService.ts
 │    └── feedbackService.ts
 ├── ai/
 │    ├── gpt4o.ts
 │    ├── whisperTurbo.ts
 │    └── speechToSpeech.ts
 ├── models/
 │    └── schema.prisma
 ├── utils/
 │    ├── errorHandler.ts
 │    ├── logger.ts
 │    └── validator.ts
 ├── tests/
 │    ├── ai.test.ts
 │    ├── feedback.test.ts
 │    └── integration.test.ts
 └── app.ts
```

### Endpoint Conventions
| Endpoint | Description | Method |
|-----------|-------------|--------|
| `/api/ai/speech` | Stream speech-to-speech response | `POST` |
| `/api/ai/transcribe` | Transcribe audio to text | `POST` |
| `/api/feedback` | Retrieve or store therapy feedback | `GET/POST` |
| `/api/auth/login` | Authenticate user | `POST` |

---

## 🧠 AI Integrations

### Core Responsibilities
- Process, transcribe, and analyze speech in real time.
- Generate **empathetic voice feedback** using speech synthesis.
- Detect language (EN/ES) automatically.
- Adapt tone and word choice to age group.

### Integration Structure
```
ai/
 ├── gpt4o.ts              # Dialogue generation logic
 ├── whisperTurbo.ts       # Fast bilingual transcription
 ├── speechToSpeech.ts     # Emotional speech synthesis
 └── promptTemplates/
      ├── therapySession.en.txt
      ├── therapySession.es.txt
      └── reinforcementPhrases.txt
```

### Processing Flow
```
Input Speech → Whisper Turbo (Transcription)
Text → GPT-4o (Context Understanding + Response)
Response → Speech-to-Speech Engine (Voice Output)
Output Voice + Subtitles → Frontend Avatar
```

---

## 🧩 Shared Libraries

| Folder | Purpose |
|---------|----------|
| `/utils` | Common helpers for validation, logging, and formatting |
| `/contexts` | Global app state (language, session, feedback) |
| `/types` | Shared TypeScript types (interfaces and DTOs) |

---

## 🧪 Testing & Quality

| Type | Tool | Description |
|------|------|-------------|
| Unit Tests | Jest | Logic-level tests for services and AI modules |
| Integration Tests | Supertest | End-to-end API validation |
| UI Tests | Playwright | Frontend interaction tests |
| Static Analysis | ESLint + Prettier | Code linting and formatting enforcement |

---

## 🧩 Future Component Plans
- Implement a **Therapist Dashboard** for real-time monitoring.  
- Add **Emotion Detection** through facial expression analysis.  
- Integrate **voice tone analytics** for emotional mapping.  
- Expand to other languages (Portuguese, French).  

---

## 🧾 Review Log
| Date | Change | Author |
|------|---------|---------|
| 2025-10-20 | Created components overview | Cursor AI |
| — | — | — |
