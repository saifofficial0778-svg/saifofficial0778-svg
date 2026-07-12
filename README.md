# Hi, I'm Mohd Saif 👋

**Full Stack Developer** · MCA 2025 · Open to Work

I build production-grade web applications — not just tutorials. Currently shipping a multi-tenant School ERP SaaS platform handling real authentication, data isolation, and live deployment challenges.

---

## 🏫 EduSuite — School ERP System (Production)

A full-stack, multi-tenant SaaS platform where multiple schools independently manage students, fees, and attendance — on a single shared database with complete data isolation between tenants.

**Live:** [school-erp-system-iota.vercel.app](https://school-erp-system-iota.vercel.app)

### What I actually built and why it matters:

**Multi-Tenant Architecture**
Each school's data is isolated at the database query level — `school_id` is extracted from the JWT payload, never from client input. Even if a user manipulates the request, they cannot access another school's data.

**JWT Authentication + bcrypt**
Login issues a signed token containing `{ userId, email, role, schoolId }`. Every protected route passes through a `verifyToken` middleware that decodes the token and attaches `req.user` — controllers never trust client-supplied identity.

**Role-Based Access Control (RBAC)**
Separate roles for Admin, Teacher, and Student. Middleware enforces role checks before sensitive operations like fee collection and student enrollment.

**Fee Module — Dual Table Design**
- `fee_summary` — one row per student, tracks `total_fee`, `total_paid`, `total_due` (auto-calculated as a MySQL GENERATED column)
- `fee_logs` — one row per payment, immutable history log

This means due amounts are always accurate and payment history is never overwritten — a pattern used in real fintech systems.

**DB Transactions (Atomic Operations)**
Student and teacher enrollment touches two tables (`users` + `students`/`teachers`). If either insert fails, the entire operation rolls back — no orphan records, no data corruption.

**Auto-Generated Credentials**
When admin enrolls a student or teacher, the system generates a cryptographically shuffled password, hashes it with bcrypt (salt rounds: 10), inserts into `users`, and returns the plain password once to display in a modal — never stored in plain text, never shown again.

**DRY Utilities**
`generatePassword`, `AppError`, `catchAsync` — shared utilities used across Student, Teacher, and Auth modules. No repeated logic.

**Production Debugging**
Resolved real deployment issues: cross-tenant data leak (schoolId from URL vs JWT), Railway env var misconfiguration, Vercel SPA routing 404s, bcrypt hash mismatch from manual DB inserts.

### Tech Stack
`React.js` `Node.js` `Express.js` `MySQL` `JWT` `bcrypt` `Tailwind CSS` `Recharts` `Axios` `Railway` `Vercel` `Git`

### Architecture
```
Frontend (Vercel)          Backend (Railway)         Database (Railway MySQL)
React.js                   Express.js MVC            8 normalized tables
AuthContext                verifyToken middleware     fee_summary + fee_logs
Protected Routes    →      Controllers               student_class_mapping
Guest Routes               Models                    Foreign key constraints
Recharts Dashboard         AppError + catchAsync      GENERATED columns
```

---

## 🛠️ Tech Stack

| Layer | Technologies |
|---|---|
| Frontend | React.js, Tailwind CSS, Recharts, Axios |
| Backend | Node.js, Express.js, REST API (MVC) |
| Database | MySQL, MongoDB |
| Auth | JWT, bcrypt |
| Deployment | Railway, Vercel |
| Tools | Git, GitHub, Postman, VS Code, MySQL Workbench |

---

## 📂 Other Projects

**MERN Learning Repository**
Daily practice — JavaScript, Node.js, Express, MongoDB, React. Documented to track real progress, not just store code.

**Result Analysis Tool**
Student result processing and performance reporting application.

---

## 📈 GitHub Stats

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=saifofficial0778-svg&show_icons=true&theme=default)
![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=saifofficial0778-svg&layout=compact)

---

## 📫 Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Mohd%20Saif-blue?logo=linkedin)](https://linkedin.com/in/mohd-saif-svg)

---

*MCA 2025 · Open to full-stack roles · Available immediately*
