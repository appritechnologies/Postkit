## 📦 **Project Specification: PostKit**

### 🔧 **Overview**

**PostKit** is a CLI tool designed to streamline the setup process for backend applications using the Appri open-source stack. It helps developers scaffold the file structure, initialize database migrations, and prepare project environments with best practices.

The stack includes:

* **PostgreSQL** – Core database
* **PostgREST** – Auto-generated REST API
* **Keycloak** – Authentication and authorization
* **Graphile Worker** – Background job processing
* **Appri Function Runtime** – Serverless-style JS/TS function handler
* **PG-Storage** – Supabase Storage fork

---

### 🎯 **Goals**

* Scaffold project folder with all required structure and configuration
* Bootstrap a Postgres database with initial migrations
* Configure connections for PostgREST, Keycloak, and Graphile Worker
* Simplify onboarding for new projects and new developers

---

### 🧰 **Core Features**

#### 1. **CLI Initialization**

```bash
postkit init my-app
```

* Creates the full project directory
* Prompts user for:

  * Project name
  * Database URL
  * Keycloak URL and credentials
  * Runtime language (JS/TS)
  * Enable optional components (e.g., Graphile Worker, PG-Storage)

#### 2. **File Structure Generation**

Creates a modular backend structure:

```
my-app/
├── db/
│   ├── migrations/
│   └── seed/
├── functions/              # Appri runtime functions
├── jobs/                   # Graphile worker jobs
├── config/
│   ├── postgrest.config
│   ├── keycloak.json
│   └── .env
├── storage/                # PG-Storage setup
└── scripts/
    └── start.sh
```

#### 3. **Initial Database Migrations**

* Generates a default schema migration with:

  * Users table (linked to Keycloak)
  * Roles and permissions
  * Basic audit fields (created\_at, updated\_at)
* Includes sample tables for common use cases

```bash
postkit db:init
```

* Sets up:

  * SQL migrations via `sqitch` or `dbmate`
  * Optional seeding support

#### 4. **PostgREST Configuration**

* Auto-generates `postgrest.config` file
* Maps environment variables
* Supports RLS template scaffolding

#### 5. **Keycloak Integration**

* Adds Keycloak service user config
* Prepares example Keycloak realm and client config files
* Optional auto-import of realm via Keycloak Admin API

#### 6. **Graphile Worker Support**

* Optional flag `--with-worker`
* Adds job runner scaffolding
* Includes sample job: `send_email`, `audit_log`

#### 7. **Function Runtime Bootstrap**

* Creates base `functions/hello.js` or `.ts`
* Includes routing template and `request`/`response` interfaces

---

### 🚀 **Planned Commands**

| Command                   | Description                         |
| ------------------------- | ----------------------------------- |
| `postkit init <name>`     | Scaffold a new project              |
| `postkit db:init`         | Run initial database migration      |
| `postkit db:seed`         | Seed sample data                    |
| `postkit config:env`      | Generate `.env` and inject defaults |
| `postkit keycloak:import` | Import default realm/client setup   |
| `postkit function:add`    | Add a new function file             |
| `postkit job:add`         | Add a new Graphile worker job       |

---

### 🧱 **Dependencies**

* Node.js (CLI runtime)
* Docker (recommended for database and services)
* PostgreSQL CLI (`psql`)
* `dbmate` for migrations
* Keycloak Admin CLI

