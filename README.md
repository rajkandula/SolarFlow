# ☀️ SolarFlow — Solar Installation Management Platform

> A full-stack project management platform for solar installation companies. Customers order solar panels, sales reps approve & assign jobs, construction crews execute installs, and managers oversee everything end-to-end.

---

## 🚀 Project Name

**SolarFlow** — *From order to installation, seamlessly.*

---




## 🧑‍🤝‍🧑 User Roles

| Role | Access Level | Key Actions |
|------|-------------|-------------|
| **Customer** | Limited | Submit solar installation orders, track order status |
| **Sales Rep** | Moderate | Review & approve orders, assign crews, manage quotes |
| **Construction Crew** | Task-based | View assigned jobs, update install progress, mark complete |
| **Manager** | Full Access | All of the above + resource management, analytics, reporting |

---


<img width="554" height="604" alt="Screenshot 2026-04-18 at 2 57 46 AM" src="https://github.com/user-attachments/assets/89321f4f-97c3-4627-9d38-f470a9cfb765" />


## 🛠️ Tech Stack

### Frontend
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS + shadcn/ui
- **State Management**: Zustand
- **Data Fetching**: TanStack Query (React Query)
- **Forms**: React Hook Form + Zod validation
- **Maps**: Google Maps API (for installation addresses)
- **Charts**: Recharts (manager dashboard analytics)

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js (REST API)
- **Language**: TypeScript
- **Auth**: JWT + Role-Based Access Control (RBAC)
- **File Uploads**: Multer + AWS S3 (photos of completed installs)

### Database
- **Primary DB**: PostgreSQL (relational — orders, users, assignments)
- **ORM**: Prisma
- **Cache**: Redis (session management, real-time job queue)

### DevOps & Infrastructure
- **Containerization**: Docker + Docker Compose
- **CI/CD**: GitHub Actions
- **Hosting**: GCP Cloud Run (backend) + Vercel (frontend)
- **Storage**: GCP Cloud Storage (install photos, documents)
- **Monitoring**: GCP Cloud Logging + Sentry

---

## 📁 Project Structure

```
solarflow/
├── README.md
├── docker-compose.yml
├── .env.example
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── deploy.yml
│
├── frontend/                          # Next.js App
│   ├── package.json
│   ├── tailwind.config.ts
│   ├── next.config.ts
│   ├── tsconfig.json
│   ├── public/
│   │   └── assets/
│   └── src/
│       ├── app/                       # Next.js App Router
│       │   ├── layout.tsx
│       │   ├── page.tsx               # Landing / redirect
│       │   ├── (auth)/
│       │   │   ├── login/page.tsx
│       │   │   └── register/page.tsx
│       │   ├── (dashboard)/
│       │   │   ├── layout.tsx         # Shared dashboard shell
│       │   │   ├── customer/
│       │   │   │   ├── page.tsx       # Customer home
│       │   │   │   ├── orders/
│       │   │   │   │   ├── page.tsx   # My orders list
│       │   │   │   │   ├── new/page.tsx # New order form
│       │   │   │   │   └── [id]/page.tsx # Order detail + status
│       │   │   │   └── profile/page.tsx
│       │   │   ├── sales/
│       │   │   │   ├── page.tsx       # Sales dashboard
│       │   │   │   ├── orders/
│       │   │   │   │   ├── page.tsx   # Pending approval queue
│       │   │   │   │   └── [id]/page.tsx # Review & approve order
│       │   │   │   ├── assignments/
│       │   │   │   │   └── page.tsx   # Assign crew to jobs
│       │   │   │   └── quotes/page.tsx
│       │   │   ├── crew/
│       │   │   │   ├── page.tsx       # Crew task board
│       │   │   │   ├── jobs/
│       │   │   │   │   ├── page.tsx   # My assigned jobs
│       │   │   │   │   └── [id]/page.tsx # Job detail + update status
│       │   │   │   └── schedule/page.tsx
│       │   │   └── manager/
│       │   │       ├── page.tsx       # Manager overview
│       │   │       ├── orders/page.tsx
│       │   │       ├── crews/
│       │   │       │   ├── page.tsx   # All crews + availability
│       │   │       │   └── [id]/page.tsx
│       │   │       ├── resources/
│       │   │       │   ├── page.tsx   # Inventory (panels, inverters, etc.)
│       │   │       │   └── order/page.tsx # Order more resources
│       │   │       ├── analytics/page.tsx
│       │   │       └── settings/page.tsx
│       ├── components/
│       │   ├── ui/                    # shadcn/ui base components
│       │   ├── layout/
│       │   │   ├── Sidebar.tsx
│       │   │   ├── Topbar.tsx
│       │   │   └── RoleGuard.tsx      # Route protection by role
│       │   ├── orders/
│       │   │   ├── OrderCard.tsx
│       │   │   ├── OrderForm.tsx
│       │   │   ├── OrderStatusBadge.tsx
│       │   │   └── OrderTimeline.tsx
│       │   ├── jobs/
│       │   │   ├── JobCard.tsx
│       │   │   ├── JobStatusUpdater.tsx
│       │   │   └── InstallPhotoUpload.tsx
│       │   ├── crew/
│       │   │   ├── CrewSelector.tsx
│       │   │   └── CrewAvailabilityCard.tsx
│       │   ├── resources/
│       │   │   ├── InventoryTable.tsx
│       │   │   └── ResourceOrderForm.tsx
│       │   └── analytics/
│       │       ├── KPICards.tsx
│       │       ├── InstallationsChart.tsx
│       │       └── RevenueChart.tsx
│       ├── hooks/
│       │   ├── useAuth.ts
│       │   ├── useOrders.ts
│       │   ├── useJobs.ts
│       │   └── useResources.ts
│       ├── lib/
│       │   ├── api.ts                 # Axios instance + interceptors
│       │   ├── auth.ts
│       │   └── utils.ts
│       ├── store/
│       │   ├── authStore.ts           # Zustand auth state
│       │   └── notificationStore.ts
│       └── types/
│           ├── order.ts
│           ├── job.ts
│           ├── user.ts
│           └── resource.ts
│
├── backend/                           # Express.js API
│   ├── package.json
│   ├── tsconfig.json
│   ├── Dockerfile
│   └── src/
│       ├── server.ts                  # Entry point
│       ├── app.ts                     # Express setup, middleware
│       ├── config/
│       │   ├── database.ts            # Prisma client
│       │   ├── redis.ts
│       │   └── gcp.ts                 # GCP Storage client
│       ├── middleware/
│       │   ├── auth.middleware.ts     # JWT verification
│       │   ├── role.middleware.ts     # RBAC guard
│       │   ├── upload.middleware.ts   # Multer config
│       │   └── error.middleware.ts
│       ├── modules/
│       │   ├── auth/
│       │   │   ├── auth.router.ts
│       │   │   ├── auth.controller.ts
│       │   │   └── auth.service.ts
│       │   ├── orders/
│       │   │   ├── orders.router.ts
│       │   │   ├── orders.controller.ts
│       │   │   └── orders.service.ts
│       │   ├── jobs/
│       │   │   ├── jobs.router.ts
│       │   │   ├── jobs.controller.ts
│       │   │   └── jobs.service.ts
│       │   ├── crews/
│       │   │   ├── crews.router.ts
│       │   │   ├── crews.controller.ts
│       │   │   └── crews.service.ts
│       │   ├── resources/
│       │   │   ├── resources.router.ts
│       │   │   ├── resources.controller.ts
│       │   │   └── resources.service.ts
│       │   ├── notifications/
│       │   │   ├── notifications.router.ts
│       │   │   └── notifications.service.ts
│       │   └── analytics/
│       │       ├── analytics.router.ts
│       │       └── analytics.service.ts
│       └── utils/
│           ├── jwt.ts
│           ├── email.ts               # Nodemailer (status notifications)
│           └── logger.ts
│
└── database/                          # DB schema & migrations
    ├── schema.prisma
    ├── migrations/
    │   ├── 001_init.sql
    │   ├── 002_add_resources.sql
    │   └── 003_add_notifications.sql
    └── seed/
        └── seed.ts                    # Dev seed data (roles, demo users)
```

---

## 🗺️ Data Flow

```
Customer submits order
    ↓
Order lands in Sales queue (status: PENDING)
    ↓
Sales Rep reviews → Approves + assigns Construction Crew (status: APPROVED)
    ↓
Crew sees job on their dashboard → Travels to site → Updates status (IN_PROGRESS)
    ↓
Install complete → Crew uploads photo evidence → Marks COMPLETED
    ↓
Manager sees real-time analytics, can order more inventory resources
```

---

## 🔐 Role Permissions Matrix

| Feature | Customer | Sales | Crew | Manager |
|---------|----------|-------|------|---------|
| Submit order | ✅ | ✅ | ❌ | ✅ |
| View own orders | ✅ | ✅ | ❌ | ✅ |
| Approve/reject orders | ❌ | ✅ | ❌ | ✅ |
| Assign crew to job | ❌ | ✅ | ❌ | ✅ |
| View assigned jobs | ❌ | ❌ | ✅ | ✅ |
| Update job status | ❌ | ❌ | ✅ | ✅ |
| Upload install photos | ❌ | ❌ | ✅ | ✅ |
| Manage resources/inventory | ❌ | ❌ | ❌ | ✅ |
| Order new resources | ❌ | ❌ | ❌ | ✅ |
| View analytics | ❌ | 🔸 Own | ❌ | ✅ Full |
| Manage users | ❌ | ❌ | ❌ | ✅ |

---

## 📦 Order Status Lifecycle

```
DRAFT → PENDING → APPROVED → ASSIGNED → IN_PROGRESS → COMPLETED
                ↘ REJECTED
```

---

## 🏁 Getting Started

### Prerequisites
- Node.js 20+
- Docker & Docker Compose
- PostgreSQL 15+

### Installation

```bash
# Clone the repo
git clone https://github.com/your-org/solarflow.git
cd solarflow

# Copy env files
cp .env.example .env
cp frontend/.env.example frontend/.env.local
cp backend/.env.example backend/.env

# Start services with Docker
docker-compose up -d

# Install dependencies
cd frontend && npm install
cd ../backend && npm install

# Run DB migrations + seed
cd backend
npx prisma migrate dev
npx ts-node src/database/seed/seed.ts

# Start dev servers (in separate terminals)
# Terminal 1 - Backend
cd backend && npm run dev        # http://localhost:4000

# Terminal 2 - Frontend
cd frontend && npm run dev       # http://localhost:3000
```

### Demo Accounts (after seeding)

| Role | Email | Password |
|------|-------|----------|
| Customer | customer@demo.com | demo1234 |
| Sales | sales@demo.com | demo1234 |
| Crew | crew@demo.com | demo1234 |
| Manager | manager@demo.com | demo1234 |

---

## 🌱 Environment Variables

```env
# Backend (.env)
DATABASE_URL=postgresql://user:password@localhost:5432/solarflow
REDIS_URL=redis://localhost:6379
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRES_IN=7d
GCP_PROJECT_ID=your-gcp-project
GCP_BUCKET_NAME=solarflow-uploads
AWS_REGION=us-east-1
SMTP_HOST=smtp.sendgrid.net
SMTP_USER=apikey
SMTP_PASS=your_sendgrid_key
PORT=4000

# Frontend (.env.local)
NEXT_PUBLIC_API_URL=http://localhost:4000/api
NEXT_PUBLIC_GOOGLE_MAPS_KEY=your_maps_key
```

---

## 📡 API Endpoints (Key Routes)

```
POST   /api/auth/login
POST   /api/auth/register

GET    /api/orders              → List orders (filtered by role)
POST   /api/orders              → Create new order (customer)
PATCH  /api/orders/:id/approve  → Approve order (sales/manager)
PATCH  /api/orders/:id/reject   → Reject order (sales/manager)
PATCH  /api/orders/:id/assign   → Assign crew (sales/manager)

GET    /api/jobs                → My jobs (crew) / all jobs (manager)
PATCH  /api/jobs/:id/status     → Update job status (crew)
POST   /api/jobs/:id/photos     → Upload install photos (crew)

GET    /api/resources           → Inventory list (manager)
POST   /api/resources/order     → Order new resources (manager)

GET    /api/analytics/overview  → KPI summary (manager)
GET    /api/analytics/installs  → Install trends (manager)
```

---

## 🤝 Contributing

1. Fork the repo
2. Create feature branch: `git checkout -b feature/your-feature`
3. Commit changes: `git commit -m 'feat: add your feature'`
4. Push to branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

MIT License — see [LICENSE](./LICENSE) for details.

---

*Built with ☀️ to make solar accessible for everyone.*
