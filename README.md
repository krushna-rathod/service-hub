# Service Hub

[![React](https://img.shields.io/badge/Frontend-React%2019-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Bundler-Vite%208-646CFF?logo=vite&logoColor=white)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Styling-Tailwind%20CSS%20v4-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Node.js](https://img.shields.io/badge/Backend-Node.js%20(ESM)-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Framework-Express%204-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/Database-MongoDB%20Mongoose-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Socket.IO](https://img.shields.io/badge/Real--Time-Socket.IO%204-010101?logo=socket.io&logoColor=white)](https://socket.io/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Service Hub** is a full-stack, enterprise-grade on-demand service marketplace connecting customers with verified local service professionals. The platform streamlines service discovery, instant booking, live GPS tracking, provider estimation, secure digital payments, and multi-channel customer communications.

Developed with high performance, scalability, and modern software design patterns, Service Hub delivers a production-ready solution tailored for urban home and commercial services.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [System Architecture](#-system-architecture)
- [Key Features](#-key-features)
- [Technologies Used](#-technologies-used)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Backend Setup](#backend-setup)
  - [Frontend Setup](#frontend-setup)
- [Environment Variables](#-environment-variables)
- [Database Configuration](#-database-configuration)
- [Running the Application](#-running-the-application)
- [API Architecture & Endpoints](#-api-architecture--endpoints)
- [Author & Contact](#-author--contact)

---

## 🌟 Overview

Finding trusted, punctual, and skilled service professionals (electricians, plumbers, carpenters, AC mechanics, home cleaners, painters) is often fragmented and unreliable. **Service Hub** solves this by offering an end-to-end digital lifecycle:

1. **Discovery & Selection**: Customers explore services with transparent pricing, verified provider ratings, and location-based availability.
2. **Real-Time Booking & Estimation**: Customers book appointments, and service professionals provide structured cost estimates prior to work.
3. **Live GPS Tracking**: Real-time geolocation tracking using Socket.IO, OSRM routing, and interactive Leaflet maps.
4. **Frictionless Payment**: Integrated Razorpay checkout with webhook-driven verification and provider earnings management via RazorpayX.
5. **Multi-Channel Notifications**: Real-time SMS and WhatsApp OTP verification alongside automated email confirmations via Brevo SMTP.

---

## 🏛️ System Architecture

```text
┌───────────────────────────────────────────────────────────┐
│                      Client Layer                         │
│   React 19 + Vite SPA | Tailwind CSS v4 | Framer Motion   │
│   Leaflet Maps | Lucide Icons | Multi-language (EN/HI/MR) │
└─────────────────────────────┬─────────────────────────────┘
                              │ HTTPS / WSS
                              ▼
┌───────────────────────────────────────────────────────────┐
│                     API & Socket Gateway                  │
│       Node.js / Express.js (ES Modules) Server            │
│       Rate Limiting | CORS Policy | Compression           │
└──────────────┬────────────────────────────┬───────────────┘
               │                            │
      REST API │                   WebSocket│ (Socket.IO + Redis)
               ▼                            ▼
┌──────────────────────────────┐   ┌────────────────────────┐
│      Application Services    │   │  Real-Time Tracking    │
│  - Auth (JWT, Bcrypt)        │   │  - GPS broadcast       │
│  - Bookings & Estimates      │   │  - Live provider route │
│  - Razorpay Payments         │   │  - OSRM route metrics  │
│  - Brevo / Twilio Messaging  │   │  - Socket room events  │
└──────────────┬───────────────┘   └───────────┬────────────┘
               │                               │
               ▼                               ▼
┌───────────────────────────────────────────────────────────┐
│                       Data Layer                          │
│     MongoDB (Mongoose ODM)      |     Redis Cache         │
│     - Users & Providers         |     - Catalog Warmup    │
│     - Bookings & Ledger         |     - Tracking State    │
│     - Tickets & Reviews         |     - Pub/Sub Adapter   │
└───────────────────────────────────────────────────────────┘
```

---

## 🚀 Key Features

### 👤 Customer Experience
- **Interactive Service Catalog**: Browse service categories with detailed sub-service cards, turnaround time, and pricing transparency.
- **Location-Based Search**: Proximity detection and city-focused service hubs (Pune, Mumbai, Nashik, Baramati, etc.).
- **Live Provider Tracking**: Follow service providers in real-time as they travel to your destination on an interactive map.
- **Estimate Approval Workflow**: Review detailed itemized quotes from providers and approve or reject with custom feedback before payment.
- **Multi-Lingual Interface**: Instant toggle between English, Hindi (हिंदी), and Marathi (मराठी).
- **Integrated Help & Support**: In-app ticketing system with real-time support message threads.

### 👷 Provider Experience
- **Provider Dashboard**: Real-time booking alerts, status toggle (online/offline), and route navigation.
- **Digital Estimation Tool**: Generate custom itemized service estimates directly from the field.
- **Earnings & Ledger Management**: Track completed jobs, pending payouts, and balance statements with withdrawal requests.
- **Live Geolocation Broadcasting**: Background GPS synchronization with automated route recalculation.

### 🛡️ Admin & Operational Capabilities
- **Unified Control Center**: Metrics overview covering gross transaction value, active bookings, completed jobs, and provider density.
- **Provider Verification & Onboarding**: Review KYC, qualifications, service categories, and account status.
- **Catalog & Content Management**: Dynamically update services, categories, promotional banners, and SEO metadata.
- **Dispute & Support Desk**: Resolve customer inquiries, manage ticket assignments, and oversee communication logs.

### 🔒 Enterprise Security & Performance
- **Zero-Trust Auth & Role Guards**: JWT authentication with cryptographically hashed passwords (`bcryptjs`).
- **OTP Verification**: Dual verification channels via Twilio Verify (SMS) and WhatsApp Cloud API / Twilio WhatsApp.
- **Rate Limiting & Abuse Prevention**: Strict rate-limiting on sensitive authentication and recovery endpoints.
- **Database Connection Pooling**: Optimized MongoDB connection lifecycle with SRV DNS resolution and query pooling.
- **Smart Cache Layer**: Redis caching for frequently accessed catalogs with automatic graceful fallback to memory cache.

---

## 🛠️ Technologies Used

### Frontend
- **Framework**: [React 19](https://react.dev/)
- **Bundler & Tooling**: [Vite 8](https://vitejs.dev/) with Fast Refresh
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/)
- **State & UI Motion**: [Framer Motion](https://www.framer.com/motion/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **Mapping & Geolocation**: [Leaflet](https://leafletjs.com/)
- **Charts & Data Visualization**: [Recharts](https://recharts.org/)
- **Client Networking**: Native Fetch API & [Socket.IO Client](https://socket.io/)
- **SEO & Head Management**: [`@dr.pogodin/react-helmet`](https://github.com/dr-pogodin/react-helmet)

### Backend
- **Runtime**: [Node.js](https://nodejs.org/) (ES Modules)
- **Web Framework**: [Express.js 4](https://expressjs.com/)
- **Database & ODM**: [MongoDB](https://www.mongodb.com/) via [Mongoose 8](https://mongoosejs.com/)
- **Real-Time Communication**: [Socket.IO 4](https://socket.io/) with [`@socket.io/redis-adapter`](https://socket.io/docs/v4/redis-adapter/)
- **Cache & Message Broker**: [Redis](https://redis.io/)
- **Payment Processing**: [Razorpay](https://razorpay.com/) & RazorpayX
- **Communications**: [Twilio Verify](https://www.twilio.com/verify), [Twilio WhatsApp](https://www.twilio.com/whatsapp), [Meta WhatsApp Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api), [Nodemailer](https://nodemailer.com/) & [Brevo](https://www.brevo.com/)
- **Routing & Geodesics**: Haversine Formula & Open Source Routing Machine (OSRM)

---

## 📂 Repository Structure

```text
service-hub/
├── api/
│   └── proxy.js                # Serverless edge proxy for production deployment
├── backend/
│   ├── server.js               # Express application entry point & HTTP server
│   ├── package.json            # Backend dependencies & lifecycle scripts
│   ├── .env.example            # Backend environment variables template
│   └── src/
│       ├── config/             # Third-party configurations (JWT, Brevo, Razorpay)
│       ├── data/               # Default catalog and seed datasets
│       ├── database/           # MongoDB connection & maintenance logic
│       ├── emails/             # HTML email templates
│       ├── middleware/         # Auth verification, rate limits, performance loggers
│       ├── models/             # Mongoose schemas (User, Provider, Booking, Payment, etc.)
│       ├── routes/             # RESTful API route definitions
│       ├── services/           # External service integrations (Twilio, WhatsApp, Mail)
│       ├── socket/             # Real-time tracking WebSocket handlers
│       └── utils/              # Redis client, geo distance, and OSRM helpers
├── frontend/
│   ├── index.html              # HTML5 application template
│   ├── vite.config.js          # Vite configuration with Tailwind integration
│   ├── package.json            # Frontend dependencies & scripts
│   ├── .env.example            # Frontend environment variables template
│   ├── public/                 # Static assets, logos, icons, sitemap, robots.txt
│   └── src/
│       ├── api/                # API communication clients (payments, tracking)
│       ├── components/         # Reusable UI components
│       │   ├── admin/          # Admin management panels
│       │   ├── authModal/      # Authentication & OTP verification modals
│       │   ├── payments/       # Payment summaries, estimate badges, status cards
│       │   ├── redesign/       # Modern responsive hero, navbar, service sections
│       │   ├── serviceCard/    # Service category and booking modal components
│       │   ├── support/        # Customer help desk and ticket center
│       │   └── tracking/       # Real-time Leaflet map & provider route panels
│       ├── config/             # Client environment API endpoints
│       ├── data/               # Static services catalog definitions
│       ├── pages/              # Primary route views (Home, Service, SEO, Legal)
│       ├── seo/                # Dynamic meta tags & JSON-LD structured schemas
│       ├── App.jsx             # Main React route router
│       ├── main.jsx            # React root mount
│       └── index.css           # Global Tailwind CSS definitions
├── .gitignore                  # Git ignore rules for node_modules, build, and env files
├── vercel.json                 # Production routing and build configuration
└── README.md                   # Project documentation
```

---

## ⚡ Getting Started

Follow the steps below to configure and run the project locally on your workstation.

### Prerequisites

- [Node.js](https://nodejs.org/) (version `v18.0.0` or higher recommended)
- [npm](https://www.npmjs.com/) (version `9.0.0` or higher)
- [MongoDB](https://www.mongodb.com/try/download/community) installed locally or a free [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) cluster URI.
- *(Optional)* [Redis](https://redis.io/) server for clustered Socket.IO adapters and catalog caching (falls back to memory cache if unavailable).

---

### Backend Setup

1. **Navigate to the backend directory:**
   ```bash
   cd backend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure environment variables:**
   ```bash
   cp .env.example .env
   ```
   Open `.env` in your editor and configure your MongoDB connection string and JWT secret (see [Environment Variables](#-environment-variables) below).

4. **Start the backend server:**
   ```bash
   # Development mode with automatic watch
   npm run dev

   # Standard production start
   npm start
   ```
   The backend will start at `http://localhost:5000`.

---

### Frontend Setup

1. **Navigate to the frontend directory:**
   ```bash
   cd frontend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure environment variables:**
   ```bash
   cp .env.example .env
   ```

4. **Start the Vite development server:**
   ```bash
   npm run dev
   ```
   The frontend application will be accessible at `http://localhost:5173`.

---

## 🔐 Environment Variables

### Backend Configuration (`backend/.env`)

| Variable | Description | Default / Example |
| :--- | :--- | :--- |
| `PORT` | Backend HTTP listening port | `5000` |
| `NODE_ENV` | Application environment (`development` / `production`) | `development` |
| `CLIENT_URL` | Frontend origin for CORS permissions | `http://localhost:5173` |
| `MONGO_URI` | MongoDB connection connection URI | `mongodb://localhost:27017/` |
| `MONGO_DB_NAME` | Target MongoDB database name | `service_hub` |
| `JWT_SECRET` | Secret key for signing JSON Web Tokens | `your_secret_key_at_least_32_chars` |
| `RAZORPAY_KEY_ID` | Razorpay public key ID | `rzp_test_your_key` |
| `RAZORPAY_KEY_SECRET` | Razorpay private secret key | `your_razorpay_secret` |
| `TWILIO_ACCOUNT_SID` | Twilio Account SID (for SMS OTP) | `ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX` |
| `TWILIO_AUTH_TOKEN` | Twilio Auth Token | `your_twilio_auth_token` |
| `TWILIO_VERIFY_SERVICE_SID` | Twilio Verify Service SID | `VAXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX` |
| `BREVO_SMTP_USER` | Brevo / Sendinblue SMTP username | `your_brevo_smtp_user` |
| `BREVO_SMTP_KEY` | Brevo / Sendinblue SMTP API password | `your_brevo_smtp_key` |
| `REDIS_URL` | Redis connection URL (optional) | `redis://localhost:6379` |

### Frontend Configuration (`frontend/.env`)

| Variable | Description | Example |
| :--- | :--- | :--- |
| `VITE_API_URL` | REST API base endpoint | `http://localhost:5000/api` |
| `VITE_SOCKET_API_URL` | WebSocket server URL for real-time tracking | `http://localhost:5000` |

---

## 🗄️ Database Configuration

Service Hub uses MongoDB with Mongoose schemas designed for ACID-compliant consistency across bookings, earnings, and user data:

- **Automatic Indexing**: Development environments build indexes automatically; production skips manual re-indexing on cold starts for maximum speed.
- **Built-in Resilience**: Configured with automated reconnect logic, configurable connection pools (`maxPoolSize`, `minPoolSize`), and custom DNS server resolution support for MongoDB Atlas clusters.
- **Database Seeding**: The server performs startup checks and creates default service categories, catalog services, and system content automatically if the collection is fresh.

---

## 🌐 API Architecture & Endpoints

| Resource | Method | Endpoint | Description |
| :--- | :--- | :--- | :--- |
| **Auth** | `POST` | `/api/auth/register` | Register customer or service provider |
| | `POST` | `/api/auth/login` | Authenticate and obtain JWT session |
| | `POST` | `/api/auth/send-sms-otp` | Dispatch SMS OTP via Twilio Verify |
| | `POST` | `/api/auth/verify-sms-otp` | Validate SMS OTP |
| **Catalog** | `GET` | `/api/catalog` | Retrieve active services and providers |
| **Bookings** | `POST` | `/api/bookings` | Create a new service appointment |
| | `GET` | `/api/bookings/:id` | Fetch booking details & status |
| | `PATCH` | `/api/bookings/:id/status`| Update job status (accept, start, complete) |
| **Payments** | `POST` | `/api/payments/create-order` | Generate Razorpay order token |
| | `POST` | `/api/payments/verify` | Verify payment signature and book |
| | `POST` | `/api/payments/estimate` | Submit provider estimate |
| **Tracking** | `WS` | `/tracking` | Socket.IO event stream for real-time GPS |
| **Support** | `POST` | `/api/support/tickets` | Open customer support inquiry |
| **Health** | `GET` | `/api/health` | Service uptime and database health check |

---

## 👨‍💻 Author & Contact

**Krushna Rathod**  
- **GitHub Profile**: [@krushna-rathod](https://github.com/krushna-rathod)  
- **Repository**: [https://github.com/krushna-rathod/service-hub](https://github.com/krushna-rathod/service-hub)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
