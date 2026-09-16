<h1 align="center">
  <br>
  🤖 FresherAI
  <br>
</h1>

<h4 align="center">Your AI-Powered Career Launchpad for Freshers</h4>

<p align="center">
  <img src="https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black" />
  <img src="https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=node.js&logoColor=white" />
  <img src="https://img.shields.io/badge/LangChain-LangGraph-FF6B6B?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Groq-AI-F55036?style=for-the-badge" />
  <img src="https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white" />
  <img src="https://img.shields.io/badge/Firebase-Auth-FFCA28?style=for-the-badge&logo=firebase&logoColor=black" />
  <img src="https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
</p>

<p align="center">
  <a href="#-features">Features</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-tech-stack">Tech Stack</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-environment-variables">Environment Variables</a> •
  <a href="#-api-routes">API Routes</a>
</p>

---

## ✨ Features

FresherAI is an all-in-one AI-powered career platform built specifically for freshers and students entering the job market.

| Feature | Description |
|---|---|
| 🎤 **AI Mock Interviews** | Dynamic, LangGraph-powered interview sessions with real-time AI evaluation |
| 📊 **Interview Reports** | Detailed post-interview analysis with scores and improvement tips |
| 📄 **Resume Scorer** | Upload your resume and get an AI-driven ATS compatibility score |
| 🏗️ **Resume Builder** | Build and download a professional resume directly in the browser |
| 🗺️ **Career Roadmap** | Personalized AI-generated learning roadmaps based on your goals |
| 💳 **Billing & Plans** | Razorpay-integrated subscription plans with usage controls |
| 🔐 **Authentication** | Secure Firebase-based Google OAuth login |

---

## 🏛️ Architecture

FresherAI is built using a **microservices architecture** with an API Gateway at the core, routing traffic to five independent backend services.

```
                        ┌─────────────────┐
                        │   React Frontend │
                        │   (Vite + Redux) │
                        └────────┬─────────┘
                                 │
                        ┌────────▼─────────┐
                        │   API Gateway    │  ← Port 6000
                        │  (Express Proxy) │
                        └──┬──┬──┬──┬──┬──┘
                           │  │  │  │  │
          ┌────────────────┘  │  │  │  └────────────────┐
          │         ┌─────────┘  └──────────┐            │
          ▼         ▼                        ▼            ▼
    ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
    │   Auth   │ │  Resume  │ │Interview │ │ Roadmap  │ │ Billing  │
    │ Service  │ │ Service  │ │ Service  │ │ Service  │ │ Service  │
    └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘
          │             │           │             │
          └─────────────┴───────────┴─────────────┘
                              │
                    ┌─────────▼──────────┐
                    │  MongoDB + Redis   │
                    └────────────────────┘
```

---

## 🛠️ Tech Stack

### Frontend

| Technology | Purpose |
|---|---|
| **React 19** | UI Framework |
| **Vite** | Build tool & dev server |
| **Redux Toolkit** | Global state management |
| **React Router v7** | Client-side routing |
| **TailwindCSS v4** | Styling |
| **Framer Motion** | Animations |
| **Recharts** | Data visualization for reports |
| **Monaco Editor** | Code editor in interview sessions |
| **Firebase** | Google OAuth authentication |
| **Axios** | HTTP client |

### Backend (Microservices)

| Service | Technology | Description |
|---|---|---|
| **API Gateway** | Express + `express-http-proxy` | Routes all incoming requests, handles auth middleware |
| **Auth Service** | Express + Firebase Admin + MongoDB | User management, token verification |
| **Interview Service** | Express + LangChain + LangGraph + Groq | AI interview sessions with agentic graph flows |
| **Resume Service** | Express + LangChain + Groq + `pdf-parse` | Resume upload, parsing and AI scoring |
| **Roadmap Service** | Express + LangChain + LangGraph + Groq | Generates personalized career roadmaps |
| **Billing Service** | Express + Razorpay + MongoDB | Subscription plans, payment processing |

### Infrastructure

- **Redis** — Caching and session management (via Docker)
- **MongoDB** — Primary database for each service
- **Docker Compose** — Containerized Redis setup
- **Firebase Admin SDK** — Server-side token verification

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:
- [Node.js](https://nodejs.org/) v18+
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Git](https://git-scm.com/)
- A [MongoDB Atlas](https://www.mongodb.com/atlas) account
- A [Firebase](https://console.firebase.google.com/) project (for Auth)
- A [Groq API Key](https://console.groq.com/) (for AI features)
- A [Razorpay](https://razorpay.com/) account (for Billing)

### 1. Clone the Repository

```bash
git clone https://github.com/namanindoria/FresherAi.git
cd FresherAi
```

### 2. Start Redis (via Docker)

```bash
cd backend
docker-compose up -d
```

### 3. Set Up Backend Services

Each microservice needs to be started individually. First, configure the `.env` files for each service (see [Environment Variables](#-environment-variables)).

```bash
# Start API Gateway
cd backend/gateway
npm install && npm run dev

# Start Auth Service (new terminal)
cd backend/services/auth
npm install && npm run dev

# Start Interview Service (new terminal)
cd backend/services/interview
npm install && npm run dev

# Start Resume Service (new terminal)
cd backend/services/resume
npm install && npm run dev

# Start Roadmap Service (new terminal)
cd backend/services/roadmap
npm install && npm run dev

# Start Billing Service (new terminal)
cd backend/services/billing
npm install && npm run dev
```

### 4. Set Up Frontend

```bash
cd frontend
npm install
npm run dev
```

The app will be available at `http://localhost:5173`

---

## 🔑 Environment Variables

### `backend/gateway/.env`

```env
PORT=6000
FRONTEND_URL=http://localhost:5173
AUTH_SERVICE_URL=http://localhost:5001
RESUME_SERVICE_URL=http://localhost:5002
INTERVIEW_SERVICE_URL=http://localhost:5003
ROADMAP_SERVICE_URL=http://localhost:5004
BILLING_SERVICE_URL=http://localhost:5005
FIREBASE_PROJECT_ID=your_firebase_project_id
```

### `backend/services/auth/.env`

```env
PORT=5001
MONGO_URI=your_mongodb_connection_string
FIREBASE_PROJECT_ID=your_firebase_project_id
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
```

### `backend/services/interview/.env`

```env
PORT=5003
MONGO_URI=your_mongodb_connection_string
GROQ_API_KEY=your_groq_api_key
```

### `backend/services/resume/.env`

```env
PORT=5002
MONGO_URI=your_mongodb_connection_string
GROQ_API_KEY=your_groq_api_key
```

### `backend/services/roadmap/.env`

```env
PORT=5004
MONGO_URI=your_mongodb_connection_string
GROQ_API_KEY=your_groq_api_key
```

### `backend/services/billing/.env`

```env
PORT=5005
MONGO_URI=your_mongodb_connection_string
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
```

### `frontend/.env`

```env
VITE_API_BASE_URL=http://localhost:6000
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_firebase_project_id
```

---

## 🔌 API Routes

All requests go through the **API Gateway** at `http://localhost:6000`.

| Method | Route | Service | Auth Required | Description |
|---|---|---|---|---|
| `GET` | `/api/me` | Gateway | ✅ | Get current user info |
| `POST` | `/api/auth/login` | Auth | ❌ | Firebase token login / signup |
| `GET` | `/api/resume` | Resume | ✅ | Get user resume data |
| `POST` | `/api/resume/upload` | Resume | ✅ | Upload & parse PDF resume |
| `GET` | `/api/resume/score` | Resume | ✅ | Get AI resume score |
| `POST` | `/api/interview/start` | Interview | ✅ | Start a new interview session |
| `POST` | `/api/interview/:id/answer` | Interview | ✅ | Submit answer during interview |
| `GET` | `/api/interview/:id/report` | Interview | ✅ | Get interview report |
| `POST` | `/api/roadmap/generate` | Roadmap | ✅ | Generate a career roadmap |
| `GET` | `/api/billing/plans` | Billing | ✅ | List subscription plans |
| `POST` | `/api/billing/order` | Billing | ✅ | Create Razorpay order |

---

## 📁 Project Structure

```
FresherAi/
├── frontend/                  # React + Vite frontend
│   ├── src/
│   │   ├── pages/             # Route-level page components
│   │   │   ├── Home.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Scorer.jsx
│   │   │   ├── ResumeBuilder.jsx
│   │   │   ├── InterviewStart.jsx
│   │   │   ├── InterviewPage.jsx
│   │   │   ├── InterviewReport.jsx
│   │   │   ├── Roadmap.jsx
│   │   │   └── Billing.jsx
│   │   ├── components/        # Reusable UI components
│   │   ├── apis/              # Axios API call functions
│   │   ├── redux/             # Redux slices and store
│   │   └── utils/             # Utility helpers
│   └── package.json
│
└── backend/
    ├── docker-compose.yml     # Redis container
    ├── gateway/               # API Gateway (Port 6000)
    └── services/
        ├── auth/              # Authentication Service (Port 5001)
        ├── resume/            # Resume Service (Port 5002)
        ├── interview/         # Interview AI Service (Port 5003)
        ├── roadmap/           # Roadmap AI Service (Port 5004)
        └── billing/           # Billing Service (Port 5005)
```

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/AmazingFeature`
3. Commit your changes: `git commit -m 'Add some AmazingFeature'`
4. Push to the branch: `git push origin feature/AmazingFeature`
5. Open a Pull Request

---

## 📜 License

This project is licensed under the ISC License.

---

<p align="center">Made with ❤️ by <a href="https://github.com/namanindoria">namanindoria</a></p>
