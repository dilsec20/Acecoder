# 🎯 AceCoder — Project Presentation (7-Step Narrative Blueprint)

> **"Tell me about your project."**
>
> This document follows the **7-Step Narrative Blueprint** to present the AceCoder project in a structured, recruiter-ready format — covering Introduction, Problem Statement, Role & Responsibilities, Tech & Methodology, Challenges Faced, Results & Impact, and Learning & Future Scope.

---

## 📌 Phase 1: Foundation

---

### Step 1: Introduction

| Parameter       | Details                                                    |
| --------------- | ---------------------------------------------------------- |
| **Project Title** | **AceCoder** — A Full-Stack Placement Preparation Platform |
| **Domain**        | EdTech / Competitive Programming / Web Development         |
| **Duration**      | June 2025 — Present (Ongoing)                              |
| **Team Size**     | Solo Developer (Individual Project)                        |
| **Live URL**      | [https://acecoder.site](https://acecoder.site)             |

> *"AceCoder is a full-stack placement preparation platform I independently designed, built, and deployed. It serves 200+ active users across 5+ countries, combining DSA learning, real-time code execution, contest simulation, and aptitude preparation into one cohesive platform."*

---

### Step 2: Problem Statement

**The Gap I Identified:**

Students preparing for placement interviews face a **fragmented experience** — they use one platform for DSA problems, another for contests, a third for aptitude, and separate resources for CS fundamentals. There was no single, unified platform that brought everything together in a structured, gamified way.

**Core Problems Addressed:**

1. **Scattered Resources** — Students waste time switching between LeetCode, GFG, IndiaBix, and random YouTube playlists. There's no unified workflow.
2. **No Progress Visibility** — Most platforms don't give a holistic view of where a student stands across DSA, aptitude, and CS fundamentals.
3. **Lack of Contest Simulation** — Students don't get to practice under timed, competitive conditions unless they wait for live contests on major platforms.
4. **No Community & Collaboration** — Most prep tools are solitary. There's no social layer for sharing solutions, writing blogs, or learning from peers.

> *"The project aimed to solve the challenge of fragmented placement preparation — by building a one-stop platform where students can learn, practice, compete, and track their progress, all in one place."*

---

## 📌 Phase 2: Core Structure

---

### Step 3: Role & Responsibilities

> **Shift from "We" to "I" — Clearly define your individual contribution.**

As the **sole developer**, I was responsible for the **entire product lifecycle**:

| Area                        | My Contribution                                                                                                        |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **System Design**           | Designed the full-stack architecture — client-server model with REST API layer, PostgreSQL schema, and JWT auth flow    |
| **Backend Development**     | Built 19 RESTful API route modules (Auth, Problems, Submissions, Contests, Dashboard, Blogs, Courses, Gamification, etc.) |
| **Database Modelling**      | Designed and normalized the PostgreSQL schema — Users, Problems, Submissions, Test Cases, Contest Sessions, Blogs, Quizzes |
| **Frontend Development**    | Built 30+ React pages — Landing, Dashboard, Problem Solver, Contest Arena, Profile, Leaderboard, Blog, Admin Panel      |
| **Code Execution Engine**   | Integrated Piston API for real-time code execution with retry logic, SIGKILL handling, and multi-language support        |
| **Authentication & Security** | Implemented JWT-based auth with bcrypt password hashing, middleware-protected routes, and role-based access (Admin/User) |
| **Deployment & DevOps**     | Deployed on Render (backend) + Supabase (PostgreSQL) with connection pooling, crash protection, and auto-schema fixes   |
| **Data Seeding**            | Created SQL seed scripts for 254+ curated DSA problems (including Blind 75) and quiz questions                          |

---

### Step 4: Tech & Methodology

**Architecture: PERN Stack (PostgreSQL + Express.js + React.js + Node.js)**

```
┌─────────────────────────────────────────────────────────────┐
│                        CLIENT (Frontend)                     │
│  React.js (Vite) + Tailwind CSS + Monaco Editor + Recharts  │
└──────────────────────────┬──────────────────────────────────┘
                           │  HTTP / REST API
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                       SERVER (Backend)                        │
│  Node.js + Express.js (19 Route Modules)                     │
│  JWT Auth │ Middleware │ Piston API Integration               │
└──────────────────────────┬──────────────────────────────────┘
                           │  pg (node-postgres)
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                      DATABASE                                │
│  PostgreSQL (Supabase) — Supavisor Connection Pooling        │
│  Tables: Users, Problems, Submissions, Test Cases,           │
│          Contests, Blogs, Quizzes, Courses                   │
└─────────────────────────────────────────────────────────────┘
```

**Key Technologies & Why I Chose Them:**

| Technology               | Purpose                                                              |
| ------------------------ | -------------------------------------------------------------------- |
| **Node.js + Express.js** | Lightweight, non-blocking backend — ideal for I/O-heavy API server   |
| **PostgreSQL**           | Relational data with complex JOINs (submissions ↔ problems ↔ users) |
| **React.js (Vite)**      | Component-based UI with fast HMR for rapid development               |
| **JWT (jsonwebtoken)**   | Stateless authentication — scalable across distributed deployments   |
| **bcryptjs**             | Industry-standard password hashing with salting                      |
| **Piston API**           | Sandboxed code execution supporting C++, Java, Python, JavaScript    |
| **Monaco Editor**        | VS Code-like coding experience directly in the browser               |
| **Recharts**             | Interactive data visualization for user analytics dashboard          |
| **Tailwind CSS**         | Utility-first CSS for rapid, responsive UI development               |
| **Supabase (PostgreSQL)**| Managed database with Supavisor connection pooling for production    |
| **Render**               | PaaS for deploying both frontend (Static Site) and backend (Web Service) |
| **Cloudinary**           | Cloud-based image upload and storage for user profile pictures       |
| **Nodemailer / Resend**  | Email service for password reset and notifications                   |

**API Design (RESTful Architecture):**

The backend exposes **19 route modules** with clean RESTful endpoints:

```
/auth              → Register, Login, Verify, Forgot/Reset Password
/api/dashboard     → User stats, heatmap, difficulty breakdown, recommendations
/api/problems      → CRUD for 254+ curated DSA problems
/api/execute       → Run code & Submit solutions (Piston API integration)
/api/contests      → Start contest, submit, leaderboard, rating calculation
/api/quizzes       → Aptitude & CS fundamental quizzes
/api/blogs         → Community blog/discussion system
/api/courses       → Structured learning paths
/api/social        → Follow/unfollow, social feed
/api/gamification  → Streaks, achievements, XP system
/api/dsa           → DSA learning path progress tracking
/api/cp            → Competitive programming module
/api/admin         → Admin dashboard & content management
```

---

## 📌 Phase 3: Consolidation

---

### Step 5: Challenges Faced

#### Challenge 1: Real-Time Code Execution Reliability
- **Problem:** The Piston API (external service) would intermittently return `SIGKILL` signals, causing user submissions to fail silently.
- **Solution:** Implemented a **retry mechanism with exponential backoff** — if a SIGKILL is detected, the system retries up to 2 times with a 200ms delay before returning a graceful timeout message. This reduced user-facing execution failures by ~90%.

#### Challenge 2: Database Connection Pooling in Production
- **Problem:** Supabase uses **Supavisor (transaction-mode pooling)**, which breaks PostgreSQL prepared statements. Queries were failing randomly in production but worked perfectly locally.
- **Solution:** Overrode the `pool.query` method to **disable prepared statements** at the application level. Tuned pool size to 40 connections with aggressive idle timeouts (10s) to prevent Supavisor from dropping stale connections. Added pool-level error handlers to auto-reconnect without crashing.

#### Challenge 3: Server Crash Protection on Render
- **Problem:** Unhandled promise rejections and uncaught exceptions would crash the Node.js process on Render, causing downtime for all users.
- **Solution:** Added global `process.on('unhandledRejection')` and `process.on('uncaughtException')` handlers that log errors but **keep the server alive**. Combined with Express error middleware as a catch-all safety net.

#### Challenge 4: Parallel Dashboard Queries
- **Problem:** The user dashboard loads 11+ different statistics (problems solved, difficulty breakdown, topic progress, heatmap, streak, rating, recommendations, etc.). Sequential queries made the dashboard load in 3-4 seconds.
- **Solution:** Refactored all dashboard queries to execute in **parallel using `Promise.all()`**, reducing load time to under 800ms — a **4x performance improvement**.

#### Challenge 5: Contest Rating System
- **Problem:** Needed to build a fair, Elo-like rating system that rewards difficulty and penalizes time, similar to Codeforces/LeetCode contests.
- **Solution:** Designed a custom rating algorithm factoring in problem difficulty weights, solve time, and total problems solved per session. Ratings are categorized into tiers: Beginner → Achiever → Expert → Master.

---

### Step 6: Results & Impact

| Metric                    | Value                                       |
| ------------------------- | ------------------------------------------- |
| **Active Users**          | 200+ users across 5+ countries              |
| **Problems Curated**      | 254+ DSA problems (including Blind 75)      |
| **API Endpoints**         | 50+ RESTful endpoints across 19 modules     |
| **Frontend Pages**        | 30+ fully responsive React pages            |
| **Code Languages**        | 4 languages supported (C++, Java, Python, JS) |
| **Contest System**        | Elo-like rating with Leaderboard            |
| **Dashboard Load Time**   | < 800ms (4x improvement via parallel queries) |
| **Uptime**                | 99%+ on Render with crash protection        |
| **Platform Availability** | Live at [acecoder.site](https://acecoder.site) |

**Key Features Delivered:**
- ✅ 254+ curated DSA problems with real-time code execution
- ✅ Contest system with timer, rating, and leaderboard
- ✅ GitHub-style submission heatmap and analytics dashboard
- ✅ Interactive quizzes for Aptitude, OS, DBMS, CN
- ✅ Community blog/discussion system
- ✅ Public shareable profiles (`/profile/username`)
- ✅ Admin panel for content management
- ✅ Gamification system (streaks, XP, achievements)
- ✅ Study plans and structured learning paths
- ✅ Responsive design — works on all devices

---

### Step 7: Learning & Future Scope

#### 🎓 Key Learnings

1. **End-to-End System Design** — Gained deep understanding of designing and building a production-grade full-stack application from scratch — database schema design, API architecture, auth flows, and deployment pipelines.

2. **Database Optimization** — Learned to write performant SQL queries with JOINs, subqueries, window functions, and `DISTINCT ON` — and understood the real impact of query optimization when serving concurrent users.

3. **Production Debugging** — Learned to diagnose production-only bugs (like Supavisor breaking prepared statements) that don't reproduce locally. This taught me the importance of environment parity and defensive coding.

4. **API Design Principles** — Built clean RESTful APIs with proper status codes, middleware chains, input validation, and error handling — following industry conventions.

5. **Security Best Practices** — Implemented JWT authentication, bcrypt hashing, role-based access control, and input sanitization — understanding why each layer matters.

6. **DevOps & Deployment** — Gained hands-on experience with cloud deployment (Render), managed databases (Supabase), connection pooling, and crash-resilient server architectures.

#### 🚀 Future Scope

| Feature                         | Description                                                      |
| ------------------------------- | ---------------------------------------------------------------- |
| **WebSocket Integration**       | Real-time contest updates and live collaboration                 |
| **AI-Powered Hints**            | Use Gemini API (already integrated) for smart problem hints      |
| **Multi-Language Expansion**    | Add support for Go, Rust, and TypeScript in the code executor    |
| **Mobile App**                  | React Native version for on-the-go practice                      |
| **Mock Interview System**       | AI-driven mock technical interviews with feedback                |
| **Peer Code Review**            | Allow users to review and comment on each other's submissions    |
| **Advanced Analytics**          | Time-per-problem tracking, weak topic identification, and study recommendations |
| **Horizontal Scaling**          | Redis caching, load balancing, and containerization with Docker  |

---

## 🎤 Interview-Ready Summary (60-Second Pitch)

> *"I built **AceCoder**, a full-stack placement preparation platform that serves 200+ active users across 5+ countries. It's built on the PERN stack — React frontend, Node.js/Express backend, and PostgreSQL database. The platform features 254+ curated DSA problems with real-time code execution via the Piston API, a contest system with Elo-like ratings, community blogs, interactive quizzes, and a detailed analytics dashboard.*
>
> *As the sole developer, I designed the entire system — from database schema and RESTful API architecture to JWT authentication and deployment on Render. One of the key challenges I solved was production database connection pooling with Supavisor, where I had to disable prepared statements and tune pool configurations to prevent random query failures.*
>
> *I optimized the dashboard to load 11+ parallel queries in under 800ms, implemented retry logic for the code execution engine, and built crash-resilient server architecture. The project taught me end-to-end system design, production debugging, and the importance of writing defensive, scalable code."*

---

> **📎 Links:**
> - **Live:** [https://acecoder.site](https://acecoder.site)
> - **GitHub:** [Repository](https://github.com/dilsec20/CseWebsite)
