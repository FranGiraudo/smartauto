# SmartAuto - Monorepo

Plataforma inteligente de compra, venta y subasta de vehículos usados con asistencia de Inteligencia Artificial (tasación de precios de mercado, análisis de daños en imágenes y recomendación comparativa). Desarrollado para la cátedra de **Ingeniería Web II (2026)**.

---

## 🏛️ Estructura del Monorepo

El proyecto está organizado como un **Monorepo** con npm workspaces:

```text
smartauto/
├── backend/                  # API REST construida con NestJS & Prisma ORM
│   ├── prisma/               # Esquema de base de datos y seeds
│   ├── src/                  # Módulos: auth, cars, auctions, ai, reviews, notifications, etc.
│   ├── .env.example          # Plantilla de variables de entorno del backend
│   └── package.json          # Dependencias y scripts de backend
├── frontend/                 # Aplicación web cliente (Vanilla JS modular y CSS moderno)
│   ├── components/           # Componentes HTML reusables (header, modals, etc.)
│   ├── css/                  # Hojas de estilo modulares (home, detail, profile, publish, etc.)
│   ├── js/                   # Controladores e integración con API REST y WebSockets
│   ├── pages/                # Vistas principales (login, detail, profile, publish)
│   ├── .env.example          # Plantilla de configuración del frontend
│   └── package.json          # Servidor y scripts de frontend
├── docker-compose.yml        # Orquestación de servicios locales (PostgreSQL)
├── package.json              # Configuración de workspaces y scripts unificados
└── README.md                 # Documentación global del proyecto
```

---

## 🚀 Tecnologías Principales

### Backend
* **Framework:** [NestJS](https://nestjs.com/) (TypeScript)
* **ORM:** [Prisma](https://www.prisma.io/) con base de datos PostgreSQL
* **Inteligencia Artificial:** Google Gemini AI (`@google/genai`) y Groq SDK
* **Autenticación:** JWT con Passport y encriptación bcryptjs
* **Subida de Archivos:** Cloudinary con optimización WebP (Sharp)
* **WebSockets:** Socket.io para notificaciones y subastas en tiempo real
* **Seguridad:** Helmet, Throttler (rate limiting) y Class Validator

### Frontend
* **Tecnología:** HTML5, CSS3 modular (con CSS Custom Properties) y JavaScript ES6+
* **Conectividad:** Fetch API asíncrona, Socket.io client y manejo dinámico de estados
* **Servidor estático:** `serve` para ejecución cross-platform

---

## ⚙️ Requisitos Previos

* **Node.js** >= 18.x
* **npm** >= 9.x
* **Docker & Docker Compose** (opcional, para levantar PostgreSQL localmente)

---

## 🛠️ Instalación y Configuración

### 1. Clonar el repositorio y configurar dependencias

```bash
# Instalar dependencias en todo el monorepo
npm install
```

### 2. Variables de Entorno

#### Backend (`backend/.env`):
Copia `backend/.env.example` a `backend/.env` y completa los valores requeridos:
```bash
cp backend/.env.example backend/.env
```
Campos clave:
- `DATABASE_URL`: Conexión PostgreSQL (local o Railway).
- `JWT_SECRET`: Llave secreta para generación de tokens.
- `CLOUDINARY_*`: Credenciales para subida de imágenes.
- `GEMINI_API_KEY`: Clave de API de Google Gemini para tasaciones y comparativas.

#### Frontend (`frontend/.env`):
Copia `frontend/.env.example` a `frontend/.env`:
```bash
cp frontend/.env.example frontend/.env
```
- `API_BASE_URL`: URL del backend (por defecto `http://localhost:3000/api` para entorno local).

### 3. Base de Datos Local con Docker

Si deseas correr PostgreSQL localmente:
```bash
docker compose up -d postgres
```

Luego ejecuta las migraciones y seeds en el backend:
```bash
# Generar cliente de Prisma y sincronizar esquema
npx --workspace=backend prisma db push

# Poblar con datos de prueba iniciales
npx --workspace=backend prisma db seed
```

---

## ▶️ Ejecución en Desarrollo

Puedes ejecutar los servicios individualmente desde la raíz del monorepo mediante los scripts unificados:

```bash
# Iniciar el backend en modo desarrollo (watch mode)
npm run dev:backend

# Iniciar el frontend en un servidor local
npm run dev:frontend
```

---

## 📦 Scripts Disponibles en el Monorepo

| Comando | Descripción |
| :--- | :--- |
| `npm run dev:backend` | Inicia el backend NestJS en modo observador (`nest start --watch`) |
| `npm run dev:frontend` | Inicia el servidor estático del frontend |
| `npm run build:backend` | Compila el backend TypeScript a `dist/` |
| `npm run build:frontend` | Prepara las variables de entorno para el frontend |
| `npm run build` | Compila backend y frontend en un solo paso |
| `npm run test:backend` | Ejecuta la suite de pruebas unitarias del backend |
| `npm run lint:backend` | Ejecuta ESLint con autofix sobre el backend |

---

## 👥 Autores y Créditos

Proyecto desarrollado por **Francisco Giraudo** y equipo para la cátedra de **Ingeniería Web II**.
