# 🫀 نبض | Nabd

### AI-Powered Hypertension Health Education & Monitoring Platform

**نبض (Nabd)** is an Arabic-first health education and blood pressure monitoring platform designed to help adults with hypertension better understand their condition, track their blood pressure readings, and access reliable educational information.

The platform combines **Artificial Intelligence, Retrieval-Augmented Generation (RAG)-style knowledge grounding, health tracking, authentication, and a REST API** into one simple and user-friendly application.

> ⚠️ **Medical Disclaimer:** Nabd is an educational and monitoring tool. It does not diagnose medical conditions, prescribe medications, or replace professional medical advice.

---

## 🎯 Project Overview

Hypertension is one of the most common chronic health conditions, yet many patients struggle with:

* Understanding their blood pressure readings.
* Knowing when a reading may require urgent attention.
* Finding reliable health information.
* Tracking their measurements over time.
* Understanding medications, lifestyle changes, and follow-up requirements.

**Nabd** addresses these challenges through an integrated digital platform that provides educational content, AI-powered assistance, and personal blood pressure tracking.

---

## ✨ Key Features

### 🤖 AI Health Assistant

An Arabic AI assistant designed specifically for hypertension education.

The assistant can provide information about:

* Blood pressure measurements.
* Treatment and follow-up.
* Lifestyle and nutrition.
* Medication-related questions.
* Possible side effects.
* Emergency warning signs.

The AI responses are grounded in a predefined medical knowledge base based on the **WHO 2021 guideline for the pharmacological treatment of hypertension in adults**.

The system also includes safety guardrails to prevent the assistant from:

* Diagnosing patients.
* Prescribing medication.
* Changing medication doses.
* Recommending stopping treatment.
* Providing unsupported medical advice.

---

### 📊 Blood Pressure Tracking

Users can record their blood pressure readings including:

* Systolic pressure.
* Diastolic pressure.
* Pulse.
* Optional notes.
* Measurement date.

The application automatically classifies readings into categories such as:

* ✅ Within acceptable range
* ⚠️ Elevated
* 🔴 High
* 🚨 Danger
* Low

Users can also view and delete their previous measurements.

---

### 📚 Health Education Library

The platform includes an educational library containing Arabic articles covering topics such as:

* Starting treatment.
* Tests and follow-up.
* Medication side effects.
* Lifestyle and nutrition.
* Blood pressure measurement.
* Emergency situations.

The content is designed to be short, understandable, and patient-friendly.

---

### 🔐 Authentication & Data Privacy

Nabd uses **Supabase Authentication** to manage user accounts and sessions.

User-specific health data is protected using **Row Level Security (RLS)** so that users can only access their own measurements and profile information.

Protected API endpoints require:

```text
Authorization: Bearer <access_token>
```

---

### 🌐 REST API

Nabd provides a public REST API under:

```text
/api/public/v1
```

Available endpoints include:

| Method | Endpoint          | Authentication | Description             |
| ------ | ----------------- | -------------- | ----------------------- |
| GET    | `/health`         | ❌              | Service health          |
| GET    | `/articles`       | ❌              | Educational articles    |
| GET    | `/articles/:slug` | ❌              | Specific article        |
| POST   | `/chat`           | ❌              | AI assistant            |
| GET    | `/profile`        | ✅              | User profile            |
| PATCH  | `/profile`        | ✅              | Update profile          |
| GET    | `/readings`       | ✅              | Blood pressure readings |
| POST   | `/readings`       | ✅              | Add reading             |
| GET    | `/readings/:id`   | ✅              | Get specific reading    |
| PATCH  | `/readings/:id`   | ✅              | Update reading          |
| DELETE | `/readings/:id`   | ✅              | Delete reading          |
| GET    | `/stats`          | ✅              | Reading statistics      |

Interactive API documentation is available inside the application at:

```text
/api-docs
```

---

## 🧠 AI & Knowledge Grounding

The AI assistant uses a server-side knowledge base containing medical educational content.

The knowledge base is divided into:

```text
src/data/kb/
│
├── 01-starting-treatment.md
├── 02-tests-and-followup.md
├── 03-side-effects.md
├── 04-lifestyle.md
└── 05-measurement-and-emergencies.md
```

These documents are combined into a grounded system prompt before generating the AI response.

### Knowledge Source

The medical knowledge base is based on:

**World Health Organization (WHO) 2021 – Guideline for the pharmacological treatment of hypertension in adults.**

This approach helps reduce unsupported AI responses and keeps the assistant focused on the project's defined medical knowledge domain.

---

## 🚨 Medical Safety Layer

Because the application deals with health-related information, the AI assistant contains explicit safety rules.

For example, if the user reports serious warning signs such as:

* Chest pain or pressure.
* Sudden weakness or numbness on one side.
* Sudden speech or vision problems.
* Severe shortness of breath.
* Loss of consciousness or confusion.
* Very high blood pressure readings.

The assistant prioritizes emergency guidance instead of continuing a normal educational conversation.

---

## 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │      User / Patient  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   React Web Client   │
                    │   Arabic RTL UI      │
                    └──────────┬───────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐        ┌─────────────────┐
        │   Health APIs   │        │    AI Chat      │
        │ Readings/Profile│        │     API         │
        └────────┬────────┘        └────────┬────────┘
                 │                          │
                 ▼                          ▼
        ┌─────────────────┐        ┌─────────────────┐
        │    Supabase     │        │ Lovable AI      │
        │ Auth + Database │        │ Gateway         │
        │      + RLS      │        └────────┬────────┘
        └─────────────────┘                 │
                                           ▼
                                  ┌──────────────────┐
                                  │ Knowledge Base   │
                                  │ WHO 2021 Content │
                                  └──────────────────┘
```

---

## 🛠️ Tech Stack

### Frontend

* React 19
* TypeScript
* TanStack Start
* TanStack Router
* Tailwind CSS
* Radix UI
* Lucide React
* Recharts

### Backend / Server

* TanStack Start
* Nitro
* TypeScript
* REST API

### Database & Authentication

* Supabase
* PostgreSQL
* Supabase Authentication
* Row Level Security (RLS)

### Artificial Intelligence

* AI SDK
* OpenAI-compatible AI provider
* Lovable AI Gateway
* Google Gemini model
* Knowledge-grounded prompting
* Medical safety guardrails

### Development Tools

* Vite
* ESLint
* Prettier
* npm
* Git
* GitHub

---

## 📁 Project Structure

```text
src/
│
├── assets/
│   └── nabd-logo.png
│
├── components/
│   ├── app-shell.tsx
│   ├── chat-panel.tsx
│   └── ui/
│
├── data/
│   └── kb/
│       ├── 01-starting-treatment.md
│       ├── 02-tests-and-followup.md
│       ├── 03-side-effects.md
│       ├── 04-lifestyle.md
│       └── 05-measurement-and-emergencies.md
│
├── integrations/
│   ├── lovable/
│   └── supabase/
│
├── lib/
│   ├── ai-gateway.server.ts
│   ├── api.server.ts
│   ├── articles.ts
│   ├── auth.tsx
│   ├── chat-store.ts
│   ├── health.ts
│   └── kb.server.ts
│
├── routes/
│   ├── api/
│   ├── api-docs.tsx
│   ├── auth.tsx
│   ├── chat.$threadId.tsx
│   ├── measurements.tsx
│   ├── library.index.tsx
│   ├── library.$slug.tsx
│   ├── settings.tsx
│   └── index.tsx
│
└── styles.css
```

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <PROJECT_FOLDER>
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file and provide the required configuration.

Example:

```env
SUPABASE_URL=your_supabase_url
SUPABASE_PUBLISHABLE_KEY=your_supabase_publishable_key
LOVABLE_API_KEY=your_lovable_api_key
```

> 🔐 Never commit real API keys or secrets to GitHub.

### 4. Start the development server

```bash
npm run dev
```

The application will be available through the local development URL shown by Vite.

---

## 📦 Available Scripts

| Command             | Description              |
| ------------------- | ------------------------ |
| `npm run dev`       | Start development server |
| `npm run build`     | Build production version |
| `npm run build:dev` | Development-mode build   |
| `npm run preview`   | Preview production build |
| `npm run lint`      | Run ESLint               |
| `npm run format`    | Format project files     |

---

## 🔒 Security Considerations

The project was designed with several security considerations:

* Authentication through Supabase.
* Row Level Security for user data.
* Server-side handling of AI API credentials.
* Protected authenticated API endpoints.
* Bearer token authentication.
* Separation of server-only AI modules.
* Medical safety guardrails.
* Input validation for blood pressure readings.
* CORS configuration for the REST API.

---

## 🎯 Project Goals

The main goals of Nabd are to:

1. Make hypertension information easier to understand.
2. Provide Arabic-first health education.
3. Help users maintain a personal record of blood pressure readings.
4. Provide an AI assistant grounded in trusted medical information.
5. Improve awareness of potentially dangerous readings.
6. Demonstrate how AI can be integrated responsibly into a health-focused application.

---

## 🔮 Future Improvements

Potential future improvements include:

* 📈 Advanced blood pressure trend visualization.
* 🔔 Medication and measurement reminders.
* 📊 Personalized health statistics.
* 🧠 More advanced RAG with vector embeddings and vector database.
* 🌍 Multi-language support.
* 📱 Progressive Web App / mobile version.
* 📄 Export health reports as PDF.
* 👨‍⚕️ Doctor-facing dashboard.
* 🔗 Integration with wearable devices.
* 🗓️ Appointment and follow-up reminders.
* 🧪 More comprehensive evaluation of AI responses.

---

## 👥 Project

**Nabd — AI-Powered Hypertension Health Education & Monitoring Platform**

Built with:

**React • TypeScript • TanStack Start • Supabase • AI SDK • Gemini • Tailwind CSS**

---

## ⚠️ Disclaimer

Nabd is designed for **health education and personal monitoring purposes only**.

The information provided by the platform and its AI assistant is not intended to:

* Diagnose diseases.
* Replace a physician.
* Prescribe medications.
* Change medication doses.
* Replace emergency medical care.

Always consult a qualified healthcare professional for diagnosis and treatment decisions.

---

## ⭐ Support

If you find this project useful, consider giving the repository a ⭐ on GitHub.
