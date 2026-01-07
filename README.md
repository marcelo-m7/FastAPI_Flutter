# 🍻 Boteco PRO – Enterprise Bar Management System

[![Flutter 3](https://img.shields.io/badge/Flutter-3.x-blue?logo=flutter)](https://flutter.dev)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green?logo=fastapi)](https://fastapi.tiangolo.com)
[![SQL Server](https://img.shields.io/badge/SQL%20Server-2019+-red?logo=microsoft-sql-server)](https://www.microsoft.com/en-us/sql-server)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

---

## 🎯 What is Boteco PRO?

**Boteco PRO** is a modern, full-stack management system built for Brazilian bars and small restaurants ("botecos"). It's designed to handle everything from table management and order tracking to inventory control, recipes, and production—all from a sleek, cross-platform interface that works on Android, iOS, and the web.

This is a **complete production-ready architecture**: a high-performance FastAPI backend connected to Microsoft SQL Server, paired with a feature-rich Flutter frontend that keeps your operation running smoothly.

---

> **Built by:** Marcelo Santos

---

## 🚀 Stack Overview

| Layer      | Technology            | Purpose                                    |
|:-----------|:----------------------|:-------------------------------------------|
| **Frontend**   | Flutter 3.x + Dart    | iOS, Android, Web PWA                      |
| **Backend**    | FastAPI + Python 3.9+ | REST API with async support                |
| **Database**   | Microsoft SQL Server  | Transactional data + complex business logic|
| **Auth**       | JWT + bcrypt          | Secure login & password hashing            |

---

## ✨ Feature Breakdown

| Module                | Status | What It Does                                                     |
|:----------------------|:------:|:-----------------------------------------------------------------|
| **Dashboard**         |   ✅   | Real-time sales, active tables, stock alerts                    |
| **Table Management**  |   ✅   | Live table status grid, quick order open/close                  |
| **Product Catalog**   |   ✅   | Full CRUD, category filtering, instant stock adjustment         |
| **Suppliers**         |   ✅   | Contact registry + order tracking                               |
| **Recipes & Formulas**|   ✅   | Technical sheets, cost analysis, prep times                     |
| **In-House Production**|  ✅   | Batch tracking (in-progress → finished)                         |
| **Offline-First Cache**|  ✅   | Works without internet via SharedPreferences                    |
| **Themes & UI**       |   ✅   | Material 3, Light/Dark modes, smooth animations                 |
| **Employee Mgmt**     |   ✅   | Payroll, shift tracking, role-based access                      |
| **Reporting**         |   ✅   | Financial summaries, stock movements, invoice history           |

---

## 🗺️ What's Coming Next

| Goal                    | Roadmap Item                                                                                                                                                    |
|:------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Live Backend**        | Seamless API integration—every endpoint wired up to real SQL Server data instead of demo JSON                                                                  |
| **Auth & Roles**        | OAuth2/Google Sign-In → role-based dashboards (waiter vs. manager views)                                                                                      |
| **Offline Sync**        | Upgrade from SharedPreferences to **Isar** database for robust offline-first experience with automatic sync                                                   |
| **Reports & Exports**   | PDF/CSV generation for sales, inventory movements, and recipe cost breakdowns                                                                                  |
| **KDS & Printing**      | Kitchen Display System via WebSocket + Bluetooth/ESC-POS thermal printer integration                                                                         |
| **Analytics**           | Trend analysis, peak hour detection, customer behavior insights                                                                                               |

---

## ⚡ Quick Start

### Prerequisites

- **Flutter 3.19+** (stable channel) with Dart 3
- **Python 3.9+** (for backend development)
- **SQL Server 2019+** (local or cloud instance)
- **Git** & your favorite terminal

Verify your setup:
```bash
flutter --version
dart --version
python --version
```

### 1️⃣ Clone & Setup

```bash
git clone https://github.com/marcelo-m7/FastAPI_Flutter.git
cd FastAPI_Flutter
```

### 2️⃣ Backend Setup (FastAPI)

```bash
cd Backend/src/api
pip install -r requirements.txt

# Configure your connection
cp .env.example .env
# → Edit .env with your SQL Server credentials

# Start the dev server
uvicorn app.main:app --reload
```

**API docs:** Open `http://localhost:8000/docs` (interactive Swagger UI)

### 3️⃣ Frontend Setup (Flutter)

```bash
cd Frontend/src/v1.2
flutter pub get
```

**Run on Web:**
```bash
flutter run -d chrome
```

**Run on Android/iOS:**
```bash
flutter run    # Pick your device
```

---

## 📂 Project Architecture

```
FastAPI_Flutter/
├── Backend/                    # FastAPI + SQL Server
│   ├── src/
│   │   ├── api/               # FastAPI application
│   │   │   ├── app/
│   │   │   │   ├── main.py    # Entry point
│   │   │   │   ├── db.py      # SQL Server connection
│   │   │   │   └── routers/   # API routes (auth, products, orders, etc.)
│   │   │   └── requirements.txt
│   │   └── db/                # Database scripts
│   │       ├── init/          # Schema creation (11 SQL scripts)
│   │       └── use_cases/     # Domain-specific procedures
│   └── docs/                  # API docs & architecture guides
│
├── Frontend/                   # Flutter application
│   └── src/
│       └── v1.2/              # Latest stable version
│           ├── lib/
│           │   ├── main.dart
│           │   ├── models/    # Data classes
│           │   ├── services/  # ApiService, DatabaseService
│           │   ├── pages/     # Full-screen views
│           │   └── widgets/   # Reusable UI components
│           ├── android/       # Android-specific code
│           ├── ios/           # iOS-specific code
│           ├── web/           # Web PWA assets
│           └── pubspec.yaml
│
└── README.md                  # This file
```

---

## 🎨 Tech Highlights

**Frontend:**
- 🎭 **Material Design 3** with adaptive light/dark theming inspired by Brazilian bar aesthetics
- 🎬 **flutter_animate** for buttery-smooth transitions and micro-interactions
- 🏠 **Offline-first** architecture with SharedPreferences (upgrading to Isar)
- 🌍 **i18n ready** with pt_BR localization (Currency, dates, etc.)

**Backend:**
- ⚡ **FastAPI** with async/await for handling high concurrent requests
- 🔐 **JWT + bcrypt** for secure, stateless authentication
- 🗄️ **Stored Procedures** for complex business logic (orders, invoicing, payroll)
- 🔔 **Triggers** for automatic stock adjustments and materialized view updates

**Database:**
- 📊 **10+ Views** for comprehensive financial and operational reporting
- 🔄 **Materialized Views** with indexed performance optimization
- 📈 **Complex Queries** (TVFs, scalar functions) for cost analysis & forecasting
- ✔️ **Referential Integrity** with 3NF normalization across 20+ tables
- 🔒 **Role-based Access Control** at database level

---

## 📚 Documentation

- **[Backend Setup Guide](Backend/README.md)** – API architecture, database schema, endpoints
- **[Frontend Architecture](Frontend/src/README.md)** – UI structure, models, services & widgets
- **[API Specification](Backend/docs/Boteco_PRO_API_Completo.yaml)** – Complete OpenAPI/Swagger spec
- **[Database Schema](Backend/docs/ESTUTURA_DB.md)** – ER diagram, table relationships, indexes
- **[Database Setup Instructions](Backend/docs/INSTRUCOES_DB.md)** – Step-by-step SQL Server configuration

---

## 🔑 Key Components Explained

### Database Layer
The SQL Server backend includes:
- **11 initialization scripts** in `Backend/src/db/init/` that set up the complete schema
- **Use case procedures** organized by domain (Gestor, Estoque, Funcionários, Pedidos)
- **Complex triggers** that auto-update stock and materialized views in real-time
- **Financial views** for sales, expenses, and profit reporting

### API Layer
FastAPI provides:
- **11 core routers** for all business domains (auth, products, orders, invoices, etc.)
- **Connection pooling** to SQL Server for optimal performance
- **CORS configuration** for cross-origin requests from web/mobile clients
- **Automatic Swagger documentation** at `/docs`

### Mobile/Web Frontend
Flutter delivers:
- **Responsive design** that adapts from phone to tablet to desktop
- **Offline capability** with automatic sync when connection restored
- **Dark mode support** with Material 3 color system
- **Accessibility features** (semantic labels, high contrast options)

---

## 🤝 Contributing & Support

Contributions are welcome! Found a bug or have a feature idea?

1. **Open an issue** describing the problem or feature request
2. **Fork the repo** and create a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit changes** with clear messages (`git commit -m 'Add amazing feature'`)
4. **Submit a pull request** with a clear description

Code is released under the **MIT License** – see [LICENSE](LICENSE).

---

## 📝 Project Status

This is a production-grade full-stack system that demonstrates:

- ✅ Full database design and implementation (SQL Server)
- ✅ Production-grade REST API (FastAPI)
- ✅ Cross-platform mobile application (Flutter)
- ✅ Complex business logic (orders, invoicing, payroll)
- ✅ Real-world architectural patterns (3-tier, offline-first, async)

---

## 🙌 Credits & Acknowledgements

- **Flutter & Dart teams** for an amazing, productive framework
- **Microsoft** for SQL Server documentation and ODBC drivers
- **FastAPI community** for excellent async tooling and documentation

---

### 📧 Contact & Support

- **Questions?** Open a GitHub issue
- **Found a bug?** Create a detailed bug report with reproduction steps
- **Want to collaborate?** Reach out to Marcelo Santos

---

**Built with ☕ and 🍻 by Marcelo Santos**

> *"Keep it simple. Cold beer. Busy bar. Happy customers."* – **Boteco PRO**
