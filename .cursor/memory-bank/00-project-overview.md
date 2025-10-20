---
title: Project Overview — Mentorify Kids
description: Global vision, objectives, and MVP scope for the AI-powered bilingual speech therapy app.
version: 1.0
last_updated: 2025-10-19
---

# 🧩 Mentorify Kids — Project Overview

## 🎯 Purpose
Mentorify Kids is an **AI-powered speech therapy platform** designed to assist children with hearing impairments (hipoacusia) in improving language and pronunciation through interactive **speech-to-speech sessions** guided by a friendly virtual **fonoaudióloga avatar**.

The system combines:
- **OpenAI Speech-to-Speech** (real-time voice interaction)
- **Whisper Turbo** (accurate bilingual transcription)
- **GPT-4o** (contextual understanding and personalized dialogue)

Mentorify can operate in **English** and **Spanish**, allowing bilingual therapy sessions for different learning contexts.

---

## 🧠 Core Problem
Children with hipoacusia require frequent, engaging, and personalized speech therapy. Access to human therapists is limited, especially in rural or bilingual environments.  
Mentorify bridges that gap by offering an empathetic, responsive, and pedagogically guided AI experience.

---

## 🧰 Key Features (MVP)
1. 🗣️ **Interactive Avatar Therapy**  
   - Conversational sessions guided by a virtual fonoaudióloga.  
   - Real-time feedback and subtitle synchronization.  

2. 🎧 **Speech-to-Speech AI Engine**  
   - Natural voice synthesis.  
   - Whisper Turbo transcription for bilingual recognition.  

3. 🌐 **Dual Language Support (EN/ES)**  
   - Language selector and adaptive responses.  

4. 📊 **Session Feedback Dashboard**  
   - Visual indicators for pronunciation accuracy and progress.  

5. 🧾 **Secure User Accounts**  
   - Child profiles with guardian access.  
   - Data stored following **GDPR** and **COPPA** compliance.  

---

## 🧪 MVP Scope
### Must-Have (Core Flow)
1. Register / Login (Parent + Child)
2. Start therapy session (speech-to-speech)
3. View subtitles synchronized with voice
4. Receive pronunciation feedback
5. End session and save report

### Should-Have (Optional)
1. Language switching in real-time (EN/ES)
2. Reward system for completed exercises

---

## 🧭 Vision for v2.0
- Emotion recognition to adapt tone and pacing.  
- Multi-avatar personalization (therapist personas).  
- Integration with external devices (hearing aids, AR glasses).  
- Data analytics for therapists and parents.  

---

## 🧑‍💻 Tech Summary
| Layer | Stack |
|-------|--------|
| Frontend | Next.js + React + TailwindCSS |
| Backend | Node.js + Express + Prisma ORM |
| Database | PostgreSQL |
| AI Services | OpenAI Whisper Turbo + GPT-4o |
| Infra | AWS EC2 + S3 + n8n Webhooks |
| Auth | JWT + OAuth2 |

---

## 🧩 Alignment with AI for Devs Master
This project demonstrates a **full E2E AI-assisted pipeline**, including:
- Ideation and design generation via AI prompts.
- Code co-creation in Cursor with context rules.
- Documentation synchronization using the memory-bank.
- Human-AI iterative improvement workflow.

---

## 🧾 Review Log
| Date | Change | Author |
|------|---------|---------|
| 2025-10-19 | Initial structure created | Cursor AI |
| — | — | — |
