# 🧠 Mentorify Kids
### Fonoaudióloga Virtual Multilingüe para Terapia de Lenguaje Infantil

---

## 🎯 Propósito
**Mentorify Kids** es una plataforma de terapia de lenguaje asistida por IA diseñada para **niños y niñas con hipoacusia** o dificultades en la pronunciación.  
A través de un **avatar fonoaudiólogo virtual** que **habla y escucha en tiempo real** (español o inglés), el sistema guía ejercicios de pronunciación, comprensión auditiva y lectura labial con retroalimentación inmediata.

El objetivo es crear una experiencia **educativa, inclusiva y emocionalmente cálida**, combinando voz, texto y gestos visuales para acompañar el aprendizaje del lenguaje.

---

## 💡 Alcance del MVP
Desarrollar un flujo E2E completo que permita:
1. Registro del tutor y del niño/a.
2. Selección del idioma de la sesión (**Español o Inglés**).
3. Interacción por voz con el avatar (Speech-to-Speech).
4. Transcripción automática en tiempo real (Whisper Turbo).
5. Evaluación de pronunciación y retroalimentación empática.
6. Registro del progreso y visualización del avance por sesión.

---

## 🧩 Flujo E2E Prioritario

1. **Inicio de sesión / Registro del tutor**  
   - El tutor crea una cuenta, registra al niño/a y selecciona idioma (ES/EN).
2. **Sesión de práctica con el avatar IA**  
   - El niño habla al avatar.  
   - **Whisper Turbo** transcribe en tiempo real y genera subtítulos.  
   - **Speech-to-Speech (OpenAI Realtime API)** produce la respuesta oral natural del avatar.  
3. **Evaluación instantánea de pronunciación**  
   - IA analiza fonemas, ritmo y claridad.  
   - Se genera retroalimentación empática (“¡Muy bien! Intenta una vez más el sonido de la R”).  
4. **Feedback visual y auditivo**  
   - El avatar responde con gestos, expresiones y subtítulos.  
5. **Panel de progreso**  
   - Se guardan métricas por sesión: fonemas dominados, palabras practicadas y tiempo activo.  

---

## 💬 Historias de Usuario

### 🧱 Must-Have
1. **Registro del niño/a**  
   Como tutor, quiero registrar al niño/a y elegir idioma para iniciar las sesiones.  
2. **Interacción por voz con el avatar**  
   Como niño/a, quiero hablar con la fonoaudióloga virtual y recibir respuesta por voz natural.  
3. **Subtítulos automáticos**  
   Como usuario, quiero ver subtítulos sincronizados en pantalla mientras hablo.  
4. **Evaluación de pronunciación**  
   Como tutor, quiero que el sistema evalúe la pronunciación del niño y guarde su progreso.  
5. **Feedback visual y auditivo**  
   Como niño/a, quiero que el avatar me motive con gestos y voz cuando mejoro.

### 🧩 Should-Have
1. Cambiar de idioma (ES ↔ EN) sin reiniciar la sesión.  
2. Mini-juegos o stickers como recompensa al completar ejercicios.  
3. Traducción en subtítulos (modo bilingüe para aprendizaje cruzado).  

---

## 🤖 Tecnologías de IA

| Componente | Tecnología | Función |
|-------------|-------------|----------|
| **Speech-to-Speech** | OpenAI Realtime API | Comunicación bidireccional por voz natural (niño ↔ avatar). |
| **Speech-to-Text** | Whisper Turbo (OpenAI) | Transcripción ultra rápida para subtítulos y análisis fonético. |
| **LLM Conversacional** | GPT-4o / Claude Sonnet | Generación de respuestas empáticas y educativas. |
| **Avatar Engine** | WebGL / D-ID / HeyGen API | Renderizado facial, sincronización labial y expresiones. |
| **TTS Fallback (opcional)** | OpenAI / ElevenLabs | Soporte alternativo de voz si no hay conexión estable. |

---

## 🌐 Funcionalidad Multilingüe

| Modo | Características |
|------|------------------|
| 🇪🇸 **Español** | Pronunciación guiada, fonemas hispánicos, subtítulos en español. |
| 🇺🇸 **Inglés** | Pronunciación adaptada a fonética inglesa, subtítulos en inglés. |
| 🌍 **Bilingüe (Should-Have)** | Traducción en subtítulos y práctica cruzada. |

---

## 🧠 Valor Educativo y Social
- **Inclusivo:** pensado para niños con hipoacusia o dificultades del habla.  
- **Emocionalmente cálido:** voz, expresiones y lenguaje adaptados a la edad.  
- **IA con propósito:** combina modelos de voz, texto y visión.  
- **Multilingüe real:** permite practicar terapia en español e inglés.  

---

## 📊 Entregables MVP

| Entregable | Descripción |
|-------------|-------------|
| **Documentación del producto** | README completo, objetivos y funcionalidades. |
| **Historias de usuario y criterios** | Must-Have y Should-Have definidos. |
| **Arquitectura y modelo de datos** | Diagrama y estructura para usuarios, sesiones y progreso. |
| **Backend funcional** | API con Speech-to-Speech y Whisper Turbo integrados. |
| **Frontend interactivo** | Interfaz con avatar, subtítulos y selector de idioma. |
| **Suite de tests** | Unitarios, integración y un test E2E del flujo principal. |
| **CI/CD básico** | Pipeline, gestión de secretos y URL pública desplegada. |
| **Registro de IA** | Prompts, herramientas usadas, ajustes y comparativas. |

---

## 🧩 Stack sugerido
- **Frontend:** React / Next.js + Tailwind + WebGL (avatar 3D)  
- **Backend:** Node.js / Express o Python / FastAPI  
- **IA APIs:** OpenAI Realtime (Speech-to-Speech), Whisper Turbo, GPT-4o  
- **DB:** PostgreSQL / Supabase  
- **Infra:** Docker + GitHub Actions + Render / AWS EC2  
- **Gestión de secretos:** GitHub Secrets / Doppler  

---

## 📅 Cronograma de Entregas

| Entrega | Fecha límite | Contenido |
|----------|---------------|-----------|
| **Documentación técnica** | 17 de diciembre | README, flujo E2E, historias y diseño inicial. |
| **Código funcional (prototipo)** | 21 de enero | Backend + frontend conectados y flujo principal funcional. |
| **Entrega final** | 3 de febrero | Producto completo desplegado con CI/CD y video demo. |

---

## ✨ Próximos pasos
1. Implementar el selector de idioma y flujo de sesión base.  
2. Integrar Whisper Turbo para subtítulos en tiempo real.  
3. Configurar Speech-to-Speech (OpenAI Realtime API).  
4. Diseñar el avatar virtual básico (D-ID o WebGL).  
5. Conectar la base de datos para registro de sesiones y progreso.  

---

### 🚀 Autor
Proyecto final de **AI for Devs** – líder.co  
Desarrollado con amor, propósito e inteligencia artificial. ❤️  