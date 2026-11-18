# Cortex AI — Intelligent Personal Money-Balancing & Financial Decision-Support System

A full-stack, AI-powered personal finance and lifestyle decision-support system connecting:

```
Existing Cortex AI Frontend (Single-Page PWA)
                     ↓
         FastAPI High-Performance Backend
                     ↓
        MySQL 8.0 Relational Database
                     ↓
       Cortex AI Recommendation Engine
                     ↓
        OMDb Movie API (Entertainment)
                     ↓
         Smart Shopping & Products
```

---

## 🌟 Key Highlights & Integrations

1. **Original Frontend Preserved & Enhanced**:
   - Preserves 100% of the UI design, dark/light/OLED/midnight themes, card styles, and animations.
   - Connected all previously mocked interfaces (Auth, Budgets, Expenses, Goals, Allocations, History) to real backend REST endpoints.
2. **Database Engine**:
   - Built to run on the 33-table MySQL 8.0 relational schema with complete referential integrity.
   - Includes automatic zero-configuration fallback to local SQLite for instant out-of-the-box local testing.
3. **Cortex AI Recommendation Engine**:
   - Dynamically analyzes user persona (Student vs. Employee), monthly disposable income, risk tolerance, active goals (e.g., high-priority debt clearance or emergency fund), and lifestyle percentages.
   - Computes weighted allocations across 9 standard buckets (*Savings, Fixed Deposit, Recurring Deposit, Stocks, Crypto, Chits, Entertainment, Shopping, Others*).
   - Generates contextual rationales, factor impact scores, and proactive insight cards.
4. **OMDb Movie API Integration (Secure Server-Side)**:
   - Queries the OMDb API securely on the backend; the API key is kept strictly in server `.env` and is **never** exposed to client-side code.
   - Recommends movie titles, posters, ratings, runtimes, and plot synopses matched to the user's allocated Entertainment budget bucket.
   - Includes interactive search for lookup of any movie in the OMDb database.
5. **Smart Shopping & Product Integration**:
   - Suggests high-utility, discipline-conscious products matched to user interests (Tech, Lifestyle, Books, Personal Care).
   - Flags whether items fit within the user's monthly shopping budget cap.

---

## 🚀 How to Run the Project

### 1. Requirements
- Python 3.10+
- (Optional) MySQL Server 8.0+

### 2. Configure Environment (`backend/.env`)
Copy `.env.example` to `.env`:
```ini
PORT=8000
HOST=127.0.0.1
SECRET_KEY=cortex-ai-super-secret-jwt-key-change-in-production-2026

# MySQL Configuration
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASSWORD=
MYSQL_DATABASE=cortex_ai

# OMDb Movie API Key (kept private on backend)
OMDB_API_KEY=b9a5c88c
```

### 3. Start the Backend Server
From the project folder:
```powershell
cd backend
python run.py
```

Open your browser at:
👉 **`http://localhost:8000`**

The server serves both the FastAPI REST API (`/api/*`) and the Cortex AI frontend interface directly!

---

## 🔐 Demo Credentials

Pre-seeded accounts ready for immediate testing:

| Persona | Email | Password | Role |
| :--- | :--- | :--- | :--- |
| **Employee** | `employee@cortex.app` | `Employee@123` | Employee |
| **Student** | `student@cortex.app` | `Student@123` | Student |

*You can also click **"Fill Demo Credentials"** on the login page, or create a brand new account using the **"Create Account"** tab.*

---

## 📁 Project Directory Structure

```text
cortex-ai/
├── backend/
│   ├── app/
│   │   ├── config.py                 # Env vars, OMDb API key, DB settings
│   │   ├── database.py               # SQLAlchemy engine & MySQL/SQLite fallback
│   │   ├── models.py                 # 33 ORM database tables
│   │   ├── schemas.py                # Pydantic request/response models
│   │   ├── auth.py                   # Secure password hashing & JWT tokens
│   │   ├── init_db.py                # Seed categories, buckets, strategies, accounts
│   │   ├── routers/
│   │   │   ├── auth_router.py        # /api/auth/register, login, me
│   │   │   ├── budget_router.py      # /api/budget/current, save, summary
│   │   │   ├── goals_router.py       # /api/goals (goals, risk, lifestyle %)
│   │   │   ├── recommendation_router.py # /api/recommendations/generate
│   │   │   ├── plans_router.py       # /api/plans/lock, history, analysis
│   │   │   └── lifestyle_router.py   # /api/lifestyle/movies, shopping
│   │   ├── services/
│   │   │   ├── recommendation_engine.py # Cortex AI Recommendation Engine
│   │   │   ├── omdb_service.py       # Server-side OMDb API integration
│   │   │   └── shopping_service.py   # Lifestyle & product recommendation catalog
│   │   └── main.py                   # FastAPI app, CORS, static frontend mount
│   ├── .env                          # Server environment settings
│   ├── .env.example
│   ├── requirements.txt
│   └── run.py                        # Single-command server starter
├── database/
│   └── cortex-ai-database/           # Original SQL schema, seed, test, and docs
└── frontend/
    ├── index.html                    # Frontend SPA with live backend API & OMDb UI
    ├── sw.js
    ├── manifest.json
    ├── icon-192.png
    └── icon-512.png
```
