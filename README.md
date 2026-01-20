# Kiko - AI Study App (MVP / Working Prototype)

> **Note:** "Kiko" is a working title for this MVP. This repository showcases the development of a cross-platform AI study app, currently in the functional prototype phase.

**Kiko** is an AI-powered study assistant designed to reduce the friction between "consuming content" and "retaining knowledge." It transforms raw inputs—lectures, PDFs, and notes—into active recall study materials in under 60 seconds.

![Status](https://img.shields.io/badge/Status-Prototype-orange)
![Stack](https://img.shields.io/badge/Stack-Expo%20%7C%20React%20Native%20%7C%20Node.js-blue)
![Language](https://img.shields.io/badge/Language-TypeScript-3178C6)

---

## 📱 Project Overview

The core principle of this app is **TTFC < 60 seconds** (Time-To-First-Cards). The goal was to build an "offline-first" experience where users can instantly generate study materials from various sources without complex workflows.

### **Key Features**

* **⚡ Rapid Generation:** Imports text, PDFs, Images (OCR), or YouTube URLs and converts them into study decks using a server-side LLM pipeline.
* **🧠 Tinder-Style Flashcards:** Optimized for speed. Swipe Right for "Known", Left for "Missed". Includes "Star" functionality for hard concepts.
* **📝 Instant Quizzes:** Generates a 5-question multiple-choice quiz with immediate feedback and short explanations for every answer.
* **🔄 Retention Loops:**
    * **Review Mistakes:** A focused mode that only replays cards the user got wrong.
    * **Daily 8:** A spaced-repetition micro-mode mixing 6 recent mistakes with 2 new cards.
* **📂 Organization:** Folder systems, deck summaries (TL;DR), and simple notes.

---

## 🛠 Technical Stack

This project uses a full TypeScript stack (Frontend & Backend) to ensure type safety across the network boundary.

### **Mobile Client (Frontend)**
* **Framework:** React Native + Expo (Managed Workflow)
* **Navigation:** Expo Router (File-based routing)
* **State Management:** Zustand
* **Database:** Expo SQLite (Local-first architecture)
* **Architecture:** **Repository Pattern**
    * *The UI never touches the database directly. All data access is abstracted through repository classes, making the code testable and cleaner.*

### **Backend (API)**
* **Runtime:** Node.js
* **Framework:** Express.js (TypeScript)
* **AI Integration:** DeepSeek-R1 (Reasoner model) via API.
    * *Designed as a pluggable adapter pattern, allowing easy switching to OpenAI or Anthropic.*
* **Processing:**
    * `pdf-parse` for document ingestion.
    * `tesseract.js` for OCR (Optical Character Recognition).
    * Custom heuristics for YouTube transcript normalization.

---

## 🏗 Architecture & Highlights

### **1. The "Generator Seam"**
The app separates the heavy lifting from the client. The client sends raw input to the `/generate` endpoint. The server handles:
* Text extraction and normalization.
* Prompt engineering (JSON strict mode).
* **Validation:** The server enforces strict constraints (e.g., word limits per card, exactly 4 MCQ options). If the LLM output is malformed, the server rejects it before it ever reaches the client.

### **2. Offline-First Data**
Users can study, quiz, and review entirely offline. The app syncs with the local SQLite database. Network is only required for the initial generation of content.

### **3. Performance Optimizations**
* **Server-side Caching:** Implemented a `textHash` cache to prevent re-generating cards for the same content, saving API costs and reducing latency.
* **Optimistic UI:** UI handles list rendering and gesture recognition (debouncing) to ensure 60fps animations during swiping.

---

## 🚀 Roadmap & Future Improvements

**Currently Implemented:**
- [x] Full End-to-End Generation Pipeline (Text/PDF/Image/YouTube).
- [x] Core Study Modes (Flashcards, Quiz, Review).
- [x] Local Persistence (SQLite + Repositories).
- [x] Error Handling (Retries, Friendly Banners).

**Planned / To-Do:**
- [ ] **Audio Import:** Ingest voice notes or lecture recordings.
- [ ] **User Profile & Cloud Sync:** Moving beyond local-only storage.
- [ ] **Gamification:** Streaks and action-based animations.
- [ ] **Security Hardening:** Rate limiting and stricter input guardrails.
- [ ] **Monetization:** Integration with RevenueCat for generic paywalls.

---

## 👁️ App Demo / Preview
> **Note:** GIFs have reduced FPS, which is why they look a bit slow.

![swipe-demo](https://github.com/user-attachments/assets/bd8bed68-2ecd-47fd-8062-6a85e221454b)

![quiz-demo](https://github.com/user-attachments/assets/d24df104-121d-4864-a0c2-a4aa128eb043)

![swipe-finish](https://github.com/user-attachments/assets/e53128af-7d7d-47db-a986-f35748114713)

![import-content](https://github.com/user-attachments/assets/eeff550f-875f-4f71-b6d9-f3dcffd6da07)

![folder-decks](https://github.com/user-attachments/assets/02e25be4-4298-4d42-842e-d098469f4ecf)

![view-tldr-add-note](https://github.com/user-attachments/assets/70102df9-2fe6-4325-ad49-868794fcfb18)

---

## 📄 License

© [Aleksandr Kaiukov], 2026. All Rights Reserved.
This project is a personal portfolio showcase. Unauthorized copying, modification, or distribution of this code is strictly prohibited.
