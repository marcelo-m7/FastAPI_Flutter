# ⚡ Boteco PRO API – FastAPI REST Backend

[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green?logo=fastapi)](https://fastapi.tiangolo.com)
[![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python)](https://www.python.org/)
[![SQL Server](https://img.shields.io/badge/SQL%20Server-2019+-red?logo=microsoft-sql-server)](https://www.microsoft.com/en-us/sql-server)

---

## 🎯 Overview

**Boteco PRO API** is a high-performance REST API built with FastAPI that powers the entire Boteco PRO system. It connects to Microsoft SQL Server and serves the Flutter mobile/web clients with a clean, intuitive API interface.

The API handles all business logic: orders, invoicing, inventory management, employee payroll, and analytics. Built for speed with async/await support and automatic OpenAPI documentation.

---

> **Built by:** Marcelo Santos

---

## 🚀 Core Features

✅ **Secure Authentication** – JWT tokens + bcrypt password hashing  
✅ **Complete CRUD Operations** – Products, orders, employees, invoices  
✅ **Complex Business Logic** – Stored procedures for orders, invoicing, payroll  
✅ **Real-time Data** – Async endpoints for high concurrency  
✅ **Automatic Documentation** – Interactive Swagger UI at `/docs`  
✅ **CORS Enabled** – Works with web & mobile clients  
✅ **Error Handling** – Comprehensive validation & error messages  

---

## 🏗️ Architecture

```
┌─────────────────────────────────┐
│   FastAPI Application           │
│  (main.py)                      │
├─────────────────────────────────┤
│   Routers (Business Domains)    │
│  ├─ auth.py (Login)             │
│  ├─ produtos.py (Products)      │
│  ├─ pedidos.py (Orders)         │
│  ├─ faturas.py (Invoices)       │
│  ├─ estoque.py (Inventory)      │
│  ├─ funcionarios.py (Employees) │
│  └─ ... (10+ routers)           │
├─────────────────────────────────┤
│   Database Layer                │
│  (db.py - pyodbc connection)    │
├─────────────────────────────────┤
│   SQL Server Database           │
│  (Tables, Views, Procedures)    │
└─────────────────────────────────┘
```

---

## 🔌 Prerequisites

**System Requirements:**
- Python 3.9 or higher
- SQL Server 2019+ (local or remote)
- ODBC Driver 17 for SQL Server
- 512 MB RAM minimum (1 GB recommended)

**Optional:**
- Docker (for containerized deployment)
- Postman (for API testing)

**Check your setup:**
```bash
python --version      # Should be 3.9+
pip --version         # Should be 21+
```

---

## ⚙️ Quick Start

### Step 1: Install Dependencies

```bash
cd Backend/src/api

# Create virtual environment
python -m venv venv

# Activate it
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install requirements
pip install -r requirements.txt
```

### Step 2: Configure Environment

```bash
# Copy template
cp .env.example .env

# Edit .env with your SQL Server connection
# Example:
#   SQL_SERVER=localhost\SQLEXPRESS
#   SQL_USER=boteco_user
#   SQL_PASSWORD=YourSecurePassword123
#   SQL_DATABASE=BotecoPRO
#   JWT_SECRET=your-secret-key-here
```

### Step 3: Run the Server

```bash
# Development mode (with auto-reload)
uvicorn app.main:app --reload

# Production mode
uvicorn app.main:app --host 0.0.0.0 --port 8000 --workers 4
```

**Server is live at:**
- 🔗 API Root: http://localhost:8000/
- 📚 Swagger UI: http://localhost:8000/docs
- 📖 ReDoc: http://localhost:8000/redoc
- 🔍 OpenAPI JSON: http://localhost:8000/openapi.json

---

## 📚 API Documentation

### Complete Endpoint List

**Authentication:**
- `POST /auth/login` – Login with username/password → get JWT token
- `POST /auth/logout` – Invalidate token
- `POST /auth/refresh` – Refresh expired token

**Products:**
- `GET /produtos/` – List all products (paginated)
- `GET /produtos/{id}` – Get product details
- `POST /produtos/` – Create new product
- `PUT /produtos/{id}` – Update product
- `DELETE /produtos/{id}` – Delete product
- `GET /produtos/categoria/{cat_id}` – Products by category

**Orders:**
- `POST /pedidos/` – Create new order
- `GET /pedidos/{id}` – Get order & items
- `GET /pedidos/mesa/{mesa_id}` – Orders for a table
- `PUT /pedidos/{id}` – Update order status
- `DELETE /pedidos/{id}` – Cancel order

**Inventory:**
- `GET /estoque/` – Current stock snapshot
- `GET /estoque/produto/{prod_id}` – Single product stock
- `POST /estoque/ajuste` – Manual stock adjustment
- `GET /estoque/movimentos` – Stock movement history

**Invoices:**
- `POST /faturas/mesa/{mesa_id}` – Close table & generate invoice
- `GET /faturas/{id}` – Get invoice details
- `GET /faturas/` – List recent invoices
- `POST /faturas/{id}/pdf` – Download as PDF

**Employees:**
- `GET /funcionarios/` – List employees
- `GET /funcionarios/{id}` – Employee details
- `POST /funcionarios/` – Add employee
- `PUT /funcionarios/{id}` – Update employee
- `GET /funcionarios/{id}/horas` – Time tracking

**Recipes:**
- `GET /receitas/` – List all recipes
- `GET /receitas/{id}` – Recipe with ingredients
- `POST /receitas/` – Create recipe
- `PUT /receitas/{id}` – Update recipe

**Reports:**
- `GET /relatorios/vendas` – Sales by period
- `GET /relatorios/estoque` – Stock analysis
- `GET /relatorios/vencimentos` – Payroll data
- `GET /relatorios/top-produtos` – Best sellers

**[See full OpenAPI spec →](../../docs/Boteco_PRO_API_Completo.yaml)**

---

## 🔐 Authentication & Security

### Login Flow

```
1. POST /auth/login with username & password
         ↓
2. Server validates against database (bcrypt compare)
         ↓
3. Generate JWT token (valid 24 hours)
         ↓
4. Return token + user info to client
         ↓
5. Client includes Authorization: Bearer <token> in headers
```

**Example Login Request:**
```bash
curl -X POST "http://localhost:8000/auth/login" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "gerente@boteco.pro",
    "password": "senha_segura_123"
  }'
```

**Response:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "bearer",
  "user": {
    "id": 1,
    "username": "gerente@boteco.pro",
    "nome": "João da Silva",
    "cargo": "Gerente"
  }
}
```

### Protected Endpoints

All endpoints except `/auth/login` require the token:

```bash
curl -X GET "http://localhost:8000/produtos/" \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIs..."
```

**Security Features:**
- ✅ JWT tokens with expiration
- ✅ bcrypt password hashing (cost factor 12)
- ✅ CORS validation
- ✅ Request rate limiting (optional)
- ✅ SQL injection prevention (parameterized queries)

---

## 🧪 Testing the API

### Using Swagger UI (Interactive)

1. Start the server: `uvicorn app.main:app --reload`
2. Open http://localhost:8000/docs
3. Click "Authorize" button
4. Login with test credentials
5. Click any endpoint to expand
6. Click "Try it out" → enter parameters
7. Click "Execute" to send request
8. View response below

### Using cURL (Command Line)

**List Products:**
```bash
curl -X GET "http://localhost:8000/produtos/" \
  -H "Authorization: Bearer YOUR_TOKEN_HERE"
```

**Create Order:**
```bash
curl -X POST "http://localhost:8000/pedidos/" \
  -H "Authorization: Bearer YOUR_TOKEN_HERE" \
  -H "Content-Type: application/json" \
  -d '{
    "mesa_id": 1,
    "itens": [
      {"produto_id": 5, "quantidade": 2},
      {"produto_id": 12, "quantidade": 1}
    ]
  }'
```

### Using Postman

1. Import OpenAPI spec: `Backend/docs/Boteco_PRO_API_Completo.yaml`
2. Create environment with `BASE_URL` and `TOKEN` variables
3. Execute requests using environment variables

---

## 📁 Code Organization

```
api/
├── app/
│   ├── __init__.py
│   ├── main.py                    # FastAPI app setup
│   ├── db.py                      # SQL Server connection
│   ├── senha_hash.py              # Password hashing utilities
│   ├── models.py                  # Pydantic request/response models
│   └── routers/
│       ├── __init__.py
│       ├── auth.py                # Login & auth endpoints
│       ├── produtos.py            # Product CRUD
│       ├── pedidos.py             # Order management
│       ├── faturas.py             # Invoice operations
│       ├── estoque.py             # Inventory management
│       ├── funcionarios.py        # Employee endpoints
│       ├── receitas.py            # Recipe endpoints
│       └── ... (more routers)
├── requirements.txt               # Python dependencies
├── .env.example                   # Environment template
├── teste.py                       # Testing utilities
└── README_API.md                  # This file
```

### Key Files Explained

**main.py** – FastAPI application setup
- Creates FastAPI instance
- Registers all routers
- Configures CORS
- Sets up error handlers

**db.py** – Database connectivity
- pyodbc connection manager
- Connection pooling
- Error handling for DB operations

**routers/** – API endpoints organized by domain
- Each file handles one business domain
- Consistent response formats
- Input validation with Pydantic
- Error status codes

---

## 🚀 Deployment

### Development
```bash
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

### Production (Linux/macOS)
```bash
# Using Gunicorn (production WSGI server)
pip install gunicorn
gunicorn -w 4 -k uvicorn.workers.UvicornWorker app.main:app --bind 0.0.0.0:8000
```

### Docker Deployment
```bash
docker build -t boteco-api .
docker run -p 8000:8000 --env-file .env boteco-api
```

### Environment Variables for Production
```bash
SQL_SERVER=your-sql-server.database.windows.net
SQL_USER=boteco_user
SQL_PASSWORD=YourSecurePassword!@#
SQL_DATABASE=BotecoPRO
JWT_SECRET=use-a-strong-random-secret
API_HOST=0.0.0.0
API_PORT=8000
DEBUG=False
```

---

## 📊 Performance Optimization

**Connection Pooling:**
```python
# db.py auto-manages connection pool
# Max 10 concurrent connections by default
# Configurable in db.py
```

**Async Endpoints:**
- All endpoints use async/await
- Non-blocking I/O for database queries
- Handles 100+ concurrent requests efficiently

**Query Optimization:**
- Stored procedures for complex operations
- Indexed queries on high-traffic endpoints
- Caching for frequently-accessed data

---

## 📈 Monitoring & Logging

**View Request Logs:**
```bash
# Run with verbose output
uvicorn app.main:app --reload --log-level debug
```

**API Health Check:**
```bash
curl http://localhost:8000/
# Returns 200 OK if running
```

---

## 🤝 Troubleshooting

| Issue | Solution |
|:------|:---------|
| "Can't connect to SQL Server" | Check connection string in .env, verify SQL Server is running |
| "Authentication failed" | Verify credentials in database, check JWT_SECRET |
| "CORS error in browser" | CORS is configured in main.py, verify origin is allowed |
| "Port 8000 already in use" | Use different port: `--port 8001` |
| "Module not found" | Run `pip install -r requirements.txt` again |

---

## 📚 Additional Documentation

- **[Backend Architecture](../../../Backend/README.md)** – Full system overview
- **[Database Schema](../../docs/ESTUTURA_DB.md)** – Tables & relationships
- **[Setup Instructions](../../docs/INSTRUCOES_DB.md)** – Database initialization
- **[Frontend Integration](../../../Frontend/src/README.md)** – How Flutter consumes API

---

## 👨‍💻 Development Tips

1. **Use Swagger for quick testing** – No need for Postman initially
2. **Check database directly** – Use SQL Server Management Studio to verify data
3. **Enable SQL logging** – See actual queries being executed
4. **Test with sample data** – Use seed scripts to populate test data
5. **Mock endpoints** – Test frontend while backend is in development

---

**Built with precision by Marcelo Santos**

> *"A clean API is a happy API. A happy API makes happy users."* – **Boteco PRO API**
