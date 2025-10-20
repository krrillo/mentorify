---
title: AI Usage — Mentorify Kids
description: Documentation of all AI features, models, and workflows used across the Mentorify Kids system.
version: 1.0
last_updated: 2025-10-19
---

# 🤖 AI Usage — Mentorify Kids

## 🧠 Overview
This document tracks how artificial intelligence is integrated into the Mentorify Kids platform.  
It includes speech recognition, reasoning, expressive speech generation, emotion modeling, and data-driven feedback.

---

## 🗣️ 1. Whisper Turbo (Speech-to-Text)
**Purpose:** Real-time transcription of children’s speech during therapy sessions.

**Capabilities:**
- Detects spoken words and phonetic accuracy.
- Automatically identifies the spoken language (`en` / `es`).
- Provides confidence scores per phrase and per phoneme.
- Generates subtitles in synchronization with the child’s audio.

**Integration Points:**
- `/api/ai/transcribe`
- WebSocket stream: partial and final transcript frames.

**Models:** `gpt-4o-transcribe-turbo` (or `whisper-large-v3-turbo`)
**Fallback:** Whisper OpenAI API.

---

## 💬 2. GPT-4o (Reasoning + Response Generation)
**Purpose:** Generate context-aware, emotionally tuned, therapeutic responses.

**Capabilities:**
- Understands the intent and emotion of the child’s speech.
- Maintains therapy context (goal, session progress, child’s name, difficulty level).
- Produces short, positive, and educationally sound responses.
- Automatically adapts tone and language (`en` / `es`).

**Integration Points:**
- `/api/ai/respond`
- WebSocket live reasoning (`assistant_text` frames).

**Model:** `gpt-4o` (multi-modal)
**Fallback:** `gpt-4o-mini` for lightweight deployments.

---

## 🔊 3. Speech-to-Speech (Expressive Voice Synthesis)
**Purpose:** Converts the avatar’s LLM text response into a natural, expressive voice.

**Capabilities:**
- Bi-directional audio conversation with emotion control.
- Emotion parameters: `cheerful`, `calm`, `encouraging`, `neutral`.
- Supports two languages: English and Spanish.
- Streams audio back to the client in `assistant_audio_chunk` frames.

**Integration Points:**
- `/api/ai/speech`
- WebSocket stream output.

**Model:** `gpt-4o-realtime-preview` (Speech-to-Speech enabled)

---

## ❤️ 4. Emotion Detection & Adaptive Feedback
**Purpose:** Analyze tone, pacing, and emotional state from the child’s speech.

**Process:**
1. Whisper Turbo extracts low-level vocal features.
2. GPT-4o evaluates emotional tone and engagement.
3. The system adjusts the avatar’s emotional tone and speed in real time.

**Outputs:**
- Detected emotion label (`happy`, `tired`, `nervous`, etc.)
- Engagement score (0–1)
- Adaptive response suggestion

---

## 📈 5. Progress Tracking and Analytics
**Purpose:** Quantify and visualize therapy improvement using AI metrics.

**Metrics:**
- Pronunciation accuracy
- Consistency across sessions
- Time to respond
- Emotional engagement
- AI reasoning latency and token usage

**Integration:**
- Stored in database `feedback` table.
- Displayed on therapist dashboard via `/api/feedback/:childId`.

---

## 🧩 6. Language Context Management
**Purpose:** Maintain and switch between English and Spanish seamlessly.

**Implementation:**
- React Context `LanguageContext` on frontend.
- API headers include `language` for all requests.
- Backend validates and normalizes language fields.

**Modes:**
| Mode | Input | Output | Example |
|------|--------|---------|----------|
| `auto` | Detect | Match detected | Child says “hola” → Spanish session |
| `manual` | Forced | Forced | Therapist sets language to “en” |

---

## ⚙️ 7. Model Governance and Audit Trail
**Purpose:** Track and log AI model usage for compliance and reproducibility.

**Logs Include:**
- Model name and version.
- Tokens consumed (input/output).
- Latency (ms).
- Session ID, user role, and language.
- Emotion and context metadata.

**Stored In:** `ai_logs` table with automatic indexing by timestamp.

**Tools Used:** Pino structured logs → PostgreSQL → Grafana dashboards.

---

## 🧮 8. Prompt Engineering Framework
**Purpose:** Maintain consistent and auditable prompts for all AI components.

**Prompt Types:**
| Type | Description |
|------|--------------|
| `system` | Defines the avatar’s identity and rules (therapist persona). |
| `contextual` | Contains session state, goals, and previous messages. |
| `instructional` | Explains the therapy exercise (e.g., vowel repetition). |
| `reflection` | Used post-session for AI analysis and recommendations. |

**Storage:** `/prompts/system/` and `/prompts/therapy/` folders in repo.

---

## 🧾 9. Example AI Session Lifecycle
1. User starts WebSocket session → `start_session` frame.  
2. Child speaks → audio streamed → Whisper Turbo transcribes.  
3. GPT-4o receives transcript + session context → reasons and replies.  
4. Avatar voice generated via Speech-to-Speech model.  
5. Subtitles + emotion feedback displayed.  
6. Session metrics stored and visualized.

---

## 🛡️ 10. Ethical and Privacy Considerations
- All audio data processed **in memory only**, not persisted by AI models.  
- Parental consent required for all sessions.  
- No personal identifiers are used in prompts.  
- Logs and analytics anonymized.  
- GDPR, SOC2, and ISO27001 compliance required.

---

## 🧾 Revision Log
| Date | Change | Author |
|------|---------|---------|
| 2025-10-19 | Initial AI usage documentation | Cursor AI |
| — | — | — |
