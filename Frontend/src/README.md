# 📱 Boteco PRO Frontend – Flutter Application

[![Flutter 3](https://img.shields.io/badge/Flutter-3.x-blue?logo=flutter)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-3+-blue?logo=dart)](https://dart.dev/)
[![Material Design 3](https://img.shields.io/badge/Material-Design%203-green)](https://m3.material.io/)

---

## 🎨 Overview

**Boteco PRO Frontend** is a production-grade Flutter application that delivers a seamless bar management experience across iOS, Android, and the web. It features a beautiful Material Design 3 interface, offline-first data handling, and real-time sync with the FastAPI backend.

The app is designed with hospitality workflows in mind: fast access to critical functions (tables, orders, stock) with minimal taps, and powerful reporting for managers.

---

> **Built by:** Marcelo Santos – [a79433@ualg.pt](mailto:a79433@ualg.pt)  
> **Part of:** Boteco PRO (LESTI Final Project, UAlg 2024/2025)

---

## 📊 Feature Set

| Feature | Status | Details |
|:--------|:------:|:--------|
| **Dashboard** | ✅ | Sales summary, active tables, stock alerts |
| **Table Management** | ✅ | Grid view, drag-to-reorder, quick order open/close |
| **Orders** | ✅ | Create, edit, finalize with quantity selection |
| **Products** | ✅ | Browse, filter by category, view stock & pricing |
| **Inventory** | ✅ | Check levels, adjust stock, track movements |
| **Recipes** | ✅ | View technical sheets, ingredient costs, prep times |
| **In-House Production** | ✅ | Create batches, track ingredients, mark complete |
| **Employees** | ✅ | Staff directory, shift tracking, payroll info |
| **Invoices** | ✅ | View past invoices, PDF export, reprint |
| **Reports** | ✅ | Sales by period, top products, expense analysis |
| **Offline Mode** | ✅ | Works without internet, syncs when reconnected |
| **Dark Theme** | ✅ | Material 3 light/dark with custom palettes |

---

## 🏗️ Project Structure

```
Frontend/
└── src/
    └── v1.2/                          # Latest stable release
        ├── lib/
        │   ├── main.dart              # App entry point
        │   ├── theme.dart             # Material 3 theming
        │   ├── models/                # Data classes (DTOs)
        │   │   ├── produto.dart
        │   │   ├── pedido.dart
        │   │   ├── mesa.dart
        │   │   ├── fornecedor.dart
        │   │   ├── receita.dart
        │   │   └── ... (10+ models)
        │   ├── services/              # Business logic layer
        │   │   ├── api_service.dart   # HTTP client to FastAPI
        │   │   ├── database_service.dart  # Local storage
        │   │   └── auth_service.dart  # Token management
        │   ├── pages/                 # Full-screen views
        │   │   ├── dashboard_page.dart
        │   │   ├── tables_page.dart
        │   │   ├── orders_page.dart
        │   │   ├── products_page.dart
        │   │   ├── inventory_page.dart
        │   │   └── ... (10+ pages)
        │   └── widgets/               # Reusable UI components
        │       ├── app_bar.dart       # Custom app bar
        │       ├── product_card.dart
        │       ├── table_grid.dart
        │       ├── quantity_selector.dart
        │       └── ... (15+ widgets)
        ├── android/                   # Android-specific code
        ├── ios/                       # iOS-specific code
        ├── web/                       # Web PWA assets
        ├── pubspec.yaml               # Dependencies
        ├── analysis_options.yaml      # Linting rules
        └── devtools_options.yaml      # Debug tools config
```

---

## 🎬 Architecture Pattern

```
┌──────────────────────────────────────┐
│         Presentation Layer           │
│  (Pages, Widgets, UI Components)     │
├──────────────────────────────────────┤
│         Business Logic Layer         │
│  (Services: API, Database, Auth)     │
├──────────────────────────────────────┤
│         Data Layer                   │
│  ├─ Remote: FastAPI REST API         │
│  └─ Local: SharedPreferences + cache │
└──────────────────────────────────────┘
```

**Key Principles:**
- ✅ **Separation of Concerns** – Pages don't talk directly to API
- ✅ **Reusable Widgets** – DRY principle with custom components
- ✅ **Type Safety** – Strong typing with Dart & Flutter
- ✅ **Responsive Design** – Adapts from phone to tablet to web
- ✅ **Offline First** – Local cache + sync on reconnect

---

## 🚀 Getting Started

### Prerequisites

```bash
# Check versions
flutter --version     # Should be 3.19+
dart --version       # Should be 3.x
```

### Installation

```bash
# 1. Navigate to frontend
cd Frontend/src/v1.2

# 2. Get dependencies
flutter pub get

# 3. Configure backend URL
# Edit lib/services/api_service.dart
# Change: String baseUrl = "http://localhost:8000"
# To your actual backend URL
```

### Running the App

**Web (Chrome/Edge):**
```bash
flutter run -d chrome
```

**Android:**
```bash
flutter run
```

**iOS (macOS only):**
```bash
flutter run
```

---

## 🎨 Data Models

All models directly correspond to the SQL Server database tables:

**Sales & Orders:**
- `Mesa` – Table information
- `Pedido` – Order records
- `PedidoItem` – Order line items

**Products & Inventory:**
- `Produto` – Product catalog
- `Categoria` – Product categories
- `Fornecedor` – Supplier information
- `Estoque` – Inventory levels
- `EntradaEstoque` – Stock receipts
- `AjusteEstoque` – Stock adjustments

**Recipes & Production:**
- `Receita` – Recipe/formula
- `ReceitaIngrediente` – Recipe ingredients
- `ProducaoCaseira` – In-house batches
- `ProducaoIngrediente` – Batch ingredients

**Business:**
- `Funcionario` – Employee records
- `Fatura` – Invoice records
- `EventoEspecial` – Special events

---

## 🔌 Database Structure Reference

All models use proper type conversion for SQL Server:

- `INT` fields → `int` in Dart
- `DECIMAL(10,2)` → `double` in Dart
- `BIT` → `bool` in Dart (converted to 1/0 when sending)
- `DATE/DATETIME` → `DateTime` in Dart (with formatting)
- `NVARCHAR` → `String` in Dart

---

## 🎨 Theme & Styling

### Material Design 3 Implementation

The app uses Flutter's Material 3 design system with a custom color palette inspired by Brazilian bar aesthetics:

```dart
// theme.dart highlights:
ColorScheme lightColorScheme = ColorScheme(
  primary: Color(0xFFF4A460),      // Sandy brown (beer)
  secondary: Color(0xFF8B4513),    // Saddle brown (wood)
  tertiary: Color(0xFFD4AF37),     // Gold (festive)
);
```

**Features:**
- 🌓 Automatic light/dark switching
- 🎭 Material color tones (container, on-surface, etc.)
- 📱 Responsive typography
- ♿ High contrast mode support

---

## 🔌 API Integration

### ApiService Pattern

```dart
// Usage example:
final apiService = ApiService();

// Fetch products
List<Produto> products = await apiService.getProdutos();

// Create order
Pedido pedido = await apiService.criarPedido(
  mesaId: 1,
  itens: [PedidoItem(produtoId: 5, quantidade: 2)],
);

// Auto-handles:
// ✓ JWT token refresh
// ✓ Request timeouts
// ✓ Error handling
// ✓ Offline caching
```

### Endpoints Consumed

| Endpoint | Method | Purpose |
|:---------|:-------|:--------|
| `/auth/login` | POST | User authentication |
| `/produtos/` | GET | List products |
| `/estoque/` | GET | Inventory snapshot |
| `/pedidos/` | POST/GET | Create/retrieve orders |
| `/faturas/mesa/{id}` | POST | Close table & invoice |
| `/funcionarios/` | GET | Employee data |
| `/receitas/` | GET | Recipe details |

---

## 💾 Local Data Management

### SharedPreferences Strategy

**Stored Locally:**
- User authentication token
- User preferences (theme, language)
- Cached product list (demo/offline)
- Last sync timestamp

```dart
// Example:
final prefs = await SharedPreferences.getInstance();
await prefs.setString('auth_token', token);
String? token = prefs.getString('auth_token');
```

**Future:** Migration to Isar for large datasets (100k+ products)

---

## 🎯 Key Pages & Workflows

### Dashboard Page
- Total sales (today, this week)
- Active table count
- Stock alerts
- Quick action buttons

### Tables Page
- Grid view of all tables
- Tap to open/close orders
- Add items from catalog
- Finalize & invoice

### Products Page
- Search by name
- Filter by category
- Display stock & price
- Add to cart

### Inventory Page
- Current stock levels
- Manual adjustments
- Low-stock alerts
- Historical movements

### Reports Page
- Daily/weekly/monthly revenue
- Top 10 products
- Expense breakdown

---

## 🧪 Testing

**Manual Checklist:**
- [ ] Login with credentials
- [ ] Create order from table
- [ ] Add multiple items
- [ ] Close table & invoice
- [ ] View products
- [ ] Adjust stock
- [ ] Toggle dark/light theme
- [ ] Test offline mode
- [ ] Sync on reconnect

**Debug Mode:**
```bash
flutter run --verbose        # Debug logging
# Press 'r' for hot reload
# Press 'R' for hot restart
```

---

## 📱 Platform-Specific Notes

**Android:**
- Min SDK: 21 (Android 5.0)
- Target SDK: 34 (Android 14)

**iOS:**
- Min iOS: 11.0
- Requires Xcode 14+

**Web:**
- PWA support (installable)
- Offline-capable with service worker

---

## 🌍 Localization

**Portuguese (Brazil):**
- Currency: R$ formatting
- Dates: dd/MM/yyyy
- Numbers: . for decimal, , for thousands

```dart
initializeDateFormatting('pt_BR');
print(DateFormat('dd/MM/yyyy', 'pt_BR').format(DateTime.now()));
```

---

## 🚀 Build & Deployment

**Android Release:**
```bash
flutter build apk --release
# Output: build/app/outputs/flutter-app.apk
```

**iOS Release:**
```bash
flutter build ios --release
# Submit to App Store via Xcode
```

**Web Deployment:**
```bash
flutter build web --release
# Deploy 'build/web/' to any static host
```

---

## 🐛 Troubleshooting

| Issue | Fix |
|:------|:----|
| API connection fails | Check backend URL in ApiService |
| SharedPreferences error | Clear app cache & reinstall |
| Theme not switching | Check system Dark/Light setting |
| Offline sync stalls | Check internet connection & API availability |

---

## 📚 Additional Resources

- **[Material Design 3](https://m3.material.io/)** – Design system
- **[Flutter Docs](https://docs.flutter.dev)** – Official documentation
- **[Dart Language](https://dart.dev/guides)** – Language reference
- **[Backend README](../../../Backend/README.md)** – API documentation

---

## 🤝 Contributing

Found a UI bug? Help us fix it:

1. Describe the issue & steps to reproduce
2. Provide screenshots for visual issues
3. Test on multiple devices
4. Submit a PR with clear description

---

**Polished with care by Marcelo Santos**

> *"Great UI is invisible. Users just get things done."* – **Boteco PRO Frontend**
