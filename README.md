# Cura — Hospital Management Information System (HMIS)

[![TypeScript](https://img.shields.io/badge/TypeScript-Strict-blue.svg)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18-61DAFB.svg)](https://react.dev/)
[![NestJS](https://img.shields.io/badge/NestJS-10-E0234E.svg)](https://nestjs.com/)
[![Prisma](https://img.shields.io/badge/Prisma-5.22-2D3748.svg)](https://www.prisma.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791.svg)](https://www.postgresql.org/)

**Cura** is a full-stack, multi-tenant Hospital Management Information System (HMIS) built with React, TypeScript, NestJS, Prisma, and PostgreSQL. It streamlines hospital operations from patient registration and OPD consultation to surgery package billing and Indian health insurance claim settlement.

---

## Key Features

- **Authentication & RBAC**: JWT access/refresh token rotation, **Google OAuth 2.0 / Sign-In** with auto-provisioning, and hospital-scoped roles (`HOSPITAL_ADMIN`, `DOCTOR`, `RECEPTIONIST`, `CASHIER`).
- **Multi-Tenant Isolation**: Authoritative session-based tenant boundaries (`CURA-HOSP`) with PostgreSQL Row-Level Security (RLS) support.
- **Patient Management (MPI)**: Unique Medical Record Number (`MRN-YYYY-XXXXX`) generation, duplicate detection, demographics, medical history, and policy linkage.
- **Doctor Directory & Appointments**: Specialist schedules, consultation tariffs, real-time slot conflict prevention, and one-click OPD check-in.
- **Live OPD Queue & Consultations (EHR)**: Token dispensing, queue progression (`WAITING` → `IN_CONSULTATION` → `COMPLETED`), ICD diagnoses, and e-prescriptions.
- **Health Insurance & Surgery Billing Engine**:
  - Pre-loaded with **21 official Tamil Nadu State, Central Government, and IRDAI Private Insurance Schemes** (`CMCHIS & AB-PMJAY`, `TN-NHIS 2026`, `Innuyir Kappom NK-48`, `MoRTH Trauma`, `Ayushman Vay Vandana 70+`, `ESIC`, `CGHS`, `ECHS`, `MRMBS`, `RAN`, `Niramaya`, `Arogya Sanjeevani`, `Private/Corporate Floaters`, etc.) and **10 standard surgery packages**.
  - Automated eligibility checks, deductible & co-payment calculation, insurer pre-authorization, exact bill splitting (`Family Payable = Total Bill − Insurance Approved`), cashier payment receipts (Cash/Card/UPI/Bank Transfer), printable invoices, and TPA claim settlement tracking.
- **Reports & Audit Trails**: Live database dashboard metrics, revenue ledgers, insurance recovery reports with CSV export, and security audit logs.

---

## Tech Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 18, TypeScript, Vite 6, Tailwind CSS, React Router v6, TanStack Query v5, Lucide React |
| **Backend** | Node.js, NestJS 10, TypeScript, Swagger/OpenAPI, Passport/JWT, bcryptjs |
| **Database** | PostgreSQL 16, Prisma ORM 5.22 (with zero-config local disk-backed JSON persistence fallback for instant dev/demo) |
| **Testing** | Jest, Vitest, React Testing Library, `pg-mem` |

---

## Project Structure

```text
├── backend/
│   ├── prisma/          # Prisma schema, migrations, seed & master 21-scheme CSV
│   └── src/             # NestJS modules (auth, administration, patients, appointments, opd, consultations, billing, reports, tenants, database)
├── frontend/
│   ├── public/          # Static assets & downloadable master CSV
│   └── src/             # React app, layouts, providers, reusable UI components & feature pages
└── docs/                # Architecture, ER diagrams, API conventions & setup guides
```

---

## Quick Start

### Prerequisites
- **Node.js** `>= 18.0.0` & **npm** `>= 9.0.0`
- **PostgreSQL 16** *(optional — Cura automatically uses a local persistent database file `backend/prisma/local-db.json` if PostgreSQL is not running)*

### 1. Clone & Install
```bash
git clone <your-repo-url>
cd HMS
npm install
```

### 2. Configure Environment
```bash
cp .env.example .env
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env
```
*(Optional: Set `VITE_GOOGLE_CLIENT_ID` in `frontend/.env` to enable live Google Identity Services; without it, the built-in Google Account Chooser works out-of-the-box for local testing.)*

### 3. Generate Prisma Client & Run
```bash
npm run prisma:generate
npm run dev
```

### Live Endpoints
- **Frontend App**: [http://localhost:5173](http://localhost:5173)
- **Backend REST API**: [http://localhost:3000/api/v1](http://localhost:3000/api/v1)
- **Swagger API Docs**: [http://localhost:3000/api/docs](http://localhost:3000/api/docs)

---

## Demo Accounts

Sign in using **Continue with Google** or with email/password:

| Role | Email | Password |
|---|---|---|
| **Hospital Admin** | `demo.admin@indiahealthlink.com` | `Admin@123456` |
| **Doctor** | `demo.doctor@indiahealthlink.com` | `Admin@123456` |
| **Receptionist** | `demo.receptionist@indiahealthlink.com` | `Admin@123456` |
| **Billing Cashier** | `demo.cashier@indiahealthlink.com` | `Admin@123456` |

---

## Verification & Scripts

```bash
npm run typecheck   # Strict TypeScript check across frontend & backend
npm run test        # Run Vitest (frontend) & Jest (backend) test suites
npm run build       # Production build for both workspaces
```

---

## License

MIT License — see [LICENSE](LICENSE) for details.
