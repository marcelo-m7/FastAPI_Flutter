# 🍻 Boteco PRO – Bar Management System

[![Flutter 3](https://img.shields.io/badge/Flutter-3.x-blue?logo=flutter)](https://flutter.dev)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green?logo=fastapi)](https://fastapi.tiangolo.com)
[![SQL Server](https://img.shields.io/badge/SQL%20Server-2019+-red?logo=microsoft-sql-server)](https://www.microsoft.com/en-us/sql-server)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

---

## 🎯 What is Boteco PRO?

**Boteco PRO** is a modern, full-stack management system built for Brazilian bars and small restaurants ("botecos"). It's designed to handle everything from table management and order tracking to inventory control, recipes, and production—all from a sleek, cross-platform interface that works on Android, iOS, and the web.

This is a **complete production-ready architecture**: a high-performance FastAPI backend connected to Microsoft SQL Server, paired with a feature-rich Flutter frontend that keeps your operation running smoothly.

---

> **Built by:** Marcelo Santos – [a79433@ualg.pt](mailto:a79433@ualg.pt)  
> **Academic Track:** *LESTI* – Universidade do Algarve  
> **Semester:** 2024/2025 (Final Project)

---

## � Stack Overview

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
- 🎭 **Material Design 3** with adaptive light/dark theming
- 🎬 **flutter_animate** for buttery-smooth transitions
- 🏠 **Offline-first** with SharedPreferences (upgrading to Isar)
- 🌍 **i18n ready** with pt_BR localization (Currency, dates, etc.)

**Backend:**
- ⚡ **FastAPI** with async/await for high concurrency
- 🔐 **JWT + bcrypt** for secure authentication
- 🗄️ **Stored Procedures** for complex business logic (orders, invoicing, payroll)
- 🔔 **Triggers** for automatic stock adjustments and materialized view updates

**Database:**
- 📊 **10+ Views** for financial and operational reporting
- 🔄 **Materialized Views** for performance optimization
- 📈 **Complex Queries** (TVFs, scalar functions) for cost analysis
- ✔️ **Referential Integrity** & 3NF normalization across 20+ tables

---

## 🚀 Getting Started

### 1. Prerequisites

* Flutter 3.19 + (channel *stable*)
* Dart 3
* A recent Chrome / Edge (for web) or Android/iOS device / emulator

```bash
flutter --version
```

### 2. Clone

```bash
git clone https://github.com/marcelo-m7/Boteco_PRO.git
cd boteco_pro
```

### 3. Run as Web App

```bash
flutter run -d chrome        # or edge
```

### 4. Run on Android/iOS

```bash
flutter run                  # picks a connected phone/emulator
```

> **Quick test:** An already-built **`boteco_pro.apk`** sits in the project root – just sideload it on Android (`adb install boteco_pro.apk`).

---

## 🗃️ Project Structure `/lib`

```
lib/
 ├─ models/         domain DTOs & enums
 ├─ services/       ApiService + DatabaseService (offline cache)
 ├─ pages/          UI for each module
 └─ widgets/        reusable components (AppBar, Badge, QuantitySelector…)
```

Platform wrappers live in `android/`, `ios/` and `web/`.
Everything business-related stays in Dart under `lib/`.

---

## 📝 Tech Highlights

* **Material 3** theming with adaptive light/dark palettes inspired by Brazilian “boteco” colours (yellow, burgundy, beige).
* **flutter\_animate** for smooth card & FAB transitions.
* **SharedPreferences** seed data on first launch → instant demo.
* **Intl** fully configured (`initializeDateFormatting('pt_BR')`) for currency and dates in Portuguese (Brazil).

---

## 🤝 Contributing & License

This is an academic project but pull-requests are welcome for educational purposes.
Code released under the **MIT License** – see [LICENSE](LICENSE).

---

### 🙌 Acknowledgements

* Open-source Flutter community for awesome packages

---

> *“Gestão simples, cerveja gelada e boteco lotado.”* – **Boteco PRO**
