---
title: Realtime Speech-to-Speech API (WebSocket)
description: Full English documentation of Mentorify Kids live speech pipeline using Whisper Turbo, GPT-4o reasoning, and expressive speech synthesis.
version: 1.0
last_updated: 2025-10-19
---

# 🔊 Realtime Speech-to-Speech WebSocket API

**Development Endpoint:** `ws://localhost:4000/ws/ai/session`  
**Production Endpoint:** `wss://api.mentorifykids.app/ws/ai/session`  
**Auth:** `Authorization: Bearer <JWT>` or `?token=<JWT>` in the URL.  
**Purpose:** Full-duplex communication channel between child audio input and the therapeutic avatar output.

---

## 🎯 Goal

1. The client streams the child's voice.  
2. The server transcribes it (Whisper Turbo), sends it to **GPT-4o** for reasoning and therapeutic response generation.  
3. The response is synthesized back into expressive speech and streamed to the client along with subtitles.

---

## 🔁 Message Protocol (JSON Frames)

All frames are **JSON**. Audio data is **base64-encoded** within JSON for MVP simplicity.

### Client → Server

#### `start_session`
```json
{ "type": "start_session", "language": "en", "childId": "c_123", "sessionId": "s_abc" }
```

#### `audio_chunk`
```json
{ "type": "audio_chunk", "encoding": "webm/opus", "sampleRate": 48000, "data": "<base64>" }
```

#### `end_of_input`
```json
{ "type": "end_of_input" }
```

#### `cancel`
```json
{ "type": "cancel" }
```

### Server → Client

#### `partial_transcript`
```json
{ "type": "partial_transcript", "text": "Hel...", "language": "en", "confidence": 0.82 }
```

#### `final_transcript`
```json
{ "type": "final_transcript", "text": "Hello, how are you?", "language": "en", "confidence": 0.96 }
```

#### `assistant_text`
```json
{ "type": "assistant_text", "text": "Great! Let's practice saying 'banana' slowly.", "emotion": "encouraging", "language": "en" }
```

#### `assistant_audio_chunk`
```json
{ "type": "assistant_audio_chunk", "encoding": "mp3", "data": "<base64>" }
```

#### `assistant_audio_end`
```json
{ "type": "assistant_audio_end" }
```

#### `metrics`
```json
{ "type": "metrics", "latencyMs": 640, "tokensUsed": 214 }
```

#### `error`
```json
{ "type": "error", "code": "BAD_AUDIO", "message": "Invalid audio format" }
```

---

## 🌀 Typical Session Flow

1. Client sends `start_session`.  
2. Streams several `audio_chunk` → sends `end_of_input`.  
3. Server emits `partial_transcript` → `final_transcript`.  
4. Server generates LLM response → sends `assistant_text`.  
5. Streams `assistant_audio_chunk` until `assistant_audio_end`.  
6. Optionally emits `metrics`.  
7. Repeat steps 2–6 or close the socket.

---

## 🎙️ Audio Specifications

| Direction | Format | Sample Rate | Notes |
|------------|---------|--------------|-------|
| Input (child) | `webm/opus` | 48kHz | Browser default |
| Input (alt) | `pcm16` | 16kHz | For native apps |
| Output (avatar) | `mp3` | 22–44.1kHz | Expressive TTS |
| Chunk Duration | — | 20–60ms | Recommended |
| Max Frame Size | — | 256 KB | Limit |

---

## 🌐 Language Control

| Field | Values | Description |
|--------|----------|-------------|
| `language` | `"en"`, `"es"` | Language mode |
| Auto Mode | omit `language` | Server will detect using Whisper and include it in transcript frames |

---

## 💓 Keepalive and Reconnection

- **Ping/Pong** every 25s; close if no `pong` within 10s.  
- Use **exponential backoff** for retries: 250ms → 500ms → 1s → max 5s.  
- Resume by sending `start_session` with the same `sessionId`.

---

## 🔒 Security

- JWT required before accepting audio.  
- Drop frames without a valid `start_session`.  
- Rate limit: 50 messages/second/session.  
- Validate `encoding`, `sampleRate`, and chunk size.

---

## 🧩 Persistence & Logging

Each exchange stores:  
- `sessionId`, `inputLanguage`, `outputLanguage`, `tokensUsed`, `latencyMs`, `timestamp`.  
- Transcripts and LLM responses linked to `feedback` table.

---

## 🧠 Fallback REST Endpoints

| Route | Purpose |
|--------|----------|
| `POST /api/ai/transcribe` | Audio → Text (Whisper Turbo) |
| `POST /api/ai/respond` | Text → LLM Response (GPT-4o) |
| `POST /api/ai/speech` | Text → Avatar Voice (Speech-to-Speech) |

> WebSocket is the main live therapy channel. REST endpoints are used for testing, batch operations, or offline processing.

---

## 📈 Monitoring & Metrics

- Measure latency, token usage, and session duration.  
- Export Prometheus metrics: `ai_latency_seconds`, `speech_chunks_total`, `errors_total`.  
- Optional: integrate OpenTelemetry traces for reasoning flow debugging.

---

## 🚀 Future Enhancements

- Add emotion recognition from child input (audio sentiment).  
- Multi-avatar support with switchable personalities.  
- Live pronunciation scoring via `/api/ai/feedback`.  
- Fallback storage to S3 for long sessions.
