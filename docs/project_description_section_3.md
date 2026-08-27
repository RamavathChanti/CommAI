# 3. Project Description in Detail

Large-scale communication is often fragmented across different tools and channels. Organizations may prepare the same message repeatedly, translate it manually, send it through separate systems, and later struggle to determine whether recipients opened, clicked, responded to, or understood the communication. The project was designed to bring these activities into one coordinated workflow.

### Problem Addressed
* **Language barriers** reduce accessibility and reach for linguistically diverse audiences across regional demographics.
* **Manual content preparation** consumes time and can produce inconsistent wording across channels.
* **Generic messages** do not account for recipient language, location, occupation, department, or other audience characteristics.
* **Communication delivery and engagement data** are often scattered, making campaign effectiveness difficult to measure.
* **Emergency alerts and awareness campaigns** require faster creation, scheduling, distribution, governance, and tracking.

### Proposed Solution
The proposed platform—**CommAI**—combines audience management, AI-assisted content generation, multilingual translation, 23 Indic language neural speech synthesis, poster creation, Four-Eye Maker-Checker governance, campaign scheduling, multi-channel distribution, delivery tracking, sentiment analysis, feedback processing, and reporting. Instead of treating each activity as an isolated task, the platform connects them as stages of a single campaign lifecycle.

### Expected Real-World Impact
In real-world use, the platform can improve the speed and consistency of public communication while making messages more accessible to different language and literacy groups through voice bulletins and automated phone calls. Analytics and geospatial sentiment mapping help communication teams identify which campaigns are reaching people effectively and where content, timing, channel selection, or audience targeting needs improvement.

---

## Project Scope, Modules and Core Features

### Major Modules

| Module | Purpose |
| :--- | :--- |
| **Audience Management & Campaign Planning** | Manage recipients, dynamic segments, campaign details, reusable templates, and campaign state-machine workflows. |
| **AI Content Generation & Multilingual Communication** | Draft campaign content using Groq LLM & RAG, generate visual posters, translate content into 23 Indic languages, synthesize neural voice bulletins, and personalize messages. |
| **Multi-Channel Distribution & Engagement Analytics** | Support multi-channel delivery (Email, SMS, WhatsApp, Telegram, Push, Voice Calls), scheduling, delivery status tracking, feedback intake, and real-time geospatial sentiment analytics. |
| **System Governance, Integration & Finalization** | Enforce Four-Eye (Maker-Checker) administrative review for large broadcasts ($\ge 100$ recipients), connect backend/frontend services via WebSockets, test end-to-end workflows, and prepare audit logs. |

### Core Functional Features
* **User Registration, Authentication, & Role-Based Access Control (RBAC):** Secure JWT authorization with `admin`, `campaign_manager`, and `audience` roles.
* **Audience Selection & Segmentation:** Dynamic filtering by location, occupation, age, state, language, and natural-language criteria.
* **Campaign Creation & Governance:** Workflows for alerts, announcements, awareness drives, and emergency notices with Maker-Checker review gates.
* **AI-Assisted Content & Visual Poster Generation:** LLM-assisted copy generation (Groq Llama-3.3-70B), RAG policy QA, and server-side visual poster composition.
* **Multilingual Translation & 23 Indic Language Speech Synthesis:** Translation into 23 regional languages paired with neural audio bulletins (Edge-TTS / gTTS) and outbound voice calls (Twilio Voice).
* **Campaign Scheduling & Automated Dispatch:** Multi-channel distribution pipeline for Email, SMS, WhatsApp, Telegram Bot, FCM Push Notifications, and Voice.
* **Delivery Status Monitoring & Retry Support:** Real-time dispatch status tracking, error code handling, and retry support.
* **Engagement Tracking & Sentiment Analysis:** Opens, responses, feedback categorization, and regional public sentiment scoring.
* **Two-Way Feedback & Emergency SOS Loop:** Citizen proposal submission, feedback processing, Telegram SOS bot handling, and operator assist chat.
* **Dashboard Visualization:** Interactive Leaflet geospatial sentiment heatmaps, campaign reach metrics, and system analytics.

---

## System Architecture and Project Workflow

The project follows a layered full-stack architecture. The user-facing React dashboard provides campaign, voice studio, and analytics interfaces; backend FastAPI services handle authentication, campaign logic, AI workflows, speech synthesis, scheduling, and analytics; persistent storage maintains users, audiences, campaigns, and engagement records; external gateways provide AI, speech, and communication-channel capabilities.

### High-Level Architecture

| Layer | Key Responsibilities |
| :--- | :--- |
| **Presentation Layer** | Dashboard, campaign creation, 23-language voice studio, interactive sentiment map, responsive user interactions (React.js + Vite). |
| **Application/API Layer** | Authentication, RBAC, campaign state machine, content generation, translation, voice synthesis, scheduling, tracking, feedback processing (FastAPI). |
| **AI/NLP Layer** | LLM-assisted content generation (Groq Llama-3.3-70B), RAG Knowledge Base, NL segment builder, multilingual processing, tone assistance. |
| **Data Layer** | Users, recipient profiles, campaign records, message status, engagement events, feedback, emergency contacts, audit logs (SQLAlchemy / SQLite / PostgreSQL). |
| **Communication & Integration Layer** | Email (SMTP), SMS & Outbound Voice (Twilio API), WhatsApp (CallMeBot), Telegram Bot API (Broadcast & SOS), FCM Push, WebSockets. |

### End-to-End Workflow

| Step | Workflow Stage | Description |
| :--- | :--- | :--- |
| **1** | Campaign Creation | Operator defines title, topic, priority, and broadcast goals. |
| **2** | Audience Selection & Segmentation | Filter target audience by state, district, occupation, or natural language segment query. |
| **3** | AI Content & Poster Generation | Groq LLM drafts channel messages; Visual Studio renders customized poster banner with official seals. |
| **4** | Multilingual Translation & Voice Synthesis | Content translated into selected Indic languages; Edge-TTS / gTTS generates audio bulletins for voice calls/playback. |
| **5** | Governance & Channel Selection | Maker-Checker queue intercepts dispatches $\ge 100$ recipients for Admin sign-off; channels selected (Email, SMS, WhatsApp, Telegram, Push, Voice). |
| **6** | Automated Message Distribution | Asynchronous dispatcher broadcasts messages across selected communication channels. |
| **7** | Engagement Tracking & Feedback Collection | Delivery receipts recorded; citizen responses, proposals, and Telegram SOS alerts collected. |
| **8** | Analytics & Performance Dashboard | Real-time geospatial sentiment heatmap, campaign reach visualizers, and audit compliance metrics updated. |

---

## Technology Stack and Implementation Approach

The implementation uses a web-based full-stack approach in which the interface, backend APIs, AI services, database, and asynchronous communication components work together. The project utilizes FastAPI-based microservices, a React.js user dashboard, persistent relational database storage, and asynchronous background worker pipelines.

| Area | Technology / Approach | Use in Project |
| :--- | :--- | :--- |
| **Frontend** | React.js (Vite) + Vanilla CSS Design Tokens | Campaign management dashboard, 23-language voice player, sentiment analytics, and responsive views. |
| **Backend** | Python + FastAPI + Uvicorn | RESTful API endpoints for content, translation, voice synthesis, authentication, governance, and campaign workflows. |
| **Database** | SQLite / PostgreSQL (SQLAlchemy ORM) | Persistent storage for users, campaigns, recipient demographics, message status, feedback, and audit logs. |
| **AI / NLP** | Groq LLM API (`Llama-3.3-70B`) + RAG Engine | Automated alert drafting, RAG policy QA, natural language segment parsing, and content-quality assistance. |
| **Voice & Speech** | Edge-TTS + gTTS + Twilio Voice (TwiML) | 23 Indic language neural audio bulletin synthesis and automated emergency phone call alerts. |
| **Task Processing** | Asynchronous Workers & Background Tasks | Non-blocking background campaign dispatch, audio rendering, and notification workflows. |
| **Channels** | Email (SMTP), SMS, WhatsApp, Telegram, FCM, Voice | Omnichannel alert distribution, delivery monitoring, and two-way citizen response handling. |
| **Version Control** | Git + GitHub | Branch-based collaboration, code integration, and milestone submissions. |
| **Deployment** | Docker + Docker Compose + Vercel | Hosted containerized backend services and cloud web deployment. |

### Implementation Principles
* **Modular Development:** Features such as AI generation, voice synthesis, poster studio, and dispatch engines are built as decoupled, reusable services.
* **API-Based Separation:** Clean separation between React user interface, FastAPI application logic, AI models, and communication gateways.
* **Asynchronous Processing:** Long-running operations (multi-channel dispatch, audio rendering, translation) run asynchronously without blocking the UI.
* **Analytics-Driven Design:** Campaign dispatches are tracked via real-time delivery statuses, sentiment mapping, and citizen feedback loops.
* **Governance & Security First:** Role-aware JWT authorization, encrypted user credentials, and Maker-Checker safety controls for large-scale broadcasts.
