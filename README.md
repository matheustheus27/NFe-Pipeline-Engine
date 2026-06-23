# NFe Pipeline Engine — Laravel SPED Integration 🧾⚡

A production-ready enterprise solution built with Laravel designed to orchestrate, sign, validate, and emit Brazilian Electronic Fiscal Documents (NF-e). The application integrates directly with the standard `sped-nfe` and `sped-da` libraries to handle complex SEFAZ XML architectures and generate fiscal representation PDFs (DANFE).

---

## 🛠️ Software Architecture & System Layout

The platform follows an extended Layered MVC design pattern natively supported by Laravel, isolating external API business components into dedicated runtime layers.

```text
├── app/
│   ├── Console/           # Scheduled automation routines and artisan tasks
│   ├── Exceptions/        # SEFAZ API error handling interceptors
│   ├── Http/              # Controllers and Request payload validation rules
│   ├── Models/            # Database relational data mapping models
│   ├── Providers/         # Custom SPED service bindings
│   └── Services/          # Core fiscal business logic (XML parsing & signing)
├── bootstrap/             # Framework initialization scripts and cache engine
├── config/                # Centralized service settings (Database, Mail, Queue, Apps)
├── database/              # Schema management containers
│   ├── factories/  \| migrations/  \| seeds/
├── public/                # Webserver entry points (index.php, .htaccess)
├── resources/             # Raw frontend templates (Blade views, Sass, JS)
├── routes/                # Architectural URI mappings (api.php, web.php)
├── storage/               # Volatile logs, generated XML batches, and DANFE PDFs
└── tests/                 # Automated Unit and Integration test suites
```

### Core Architecture Breakdown:
* Fiscal Services (`app/Services/`): Dedicated layer encapsulating SEFAZ transmission behaviors, digital certificate signing handling, status polling, and validation rule decoupling.
* Storage Matrix (`storage/`): Manages historical signed XML pipelines and temporary cached schemas required for validation scripts.
* Worker Queue (`config/queue.php`): Configured to execute background emission attempts asynchronously, mitigating SEFAZ transmission latency bottlenecks.

## ⚙️ Core Technical Capabilities
* XML Serialization & Digital Signing: Programmatic assembly of fiscal payload payloads, automatically appending A1/A3 digital certificates.
* DANFE Generation: Dynamic rendering of standard financial overview layouts mapped onto PDF printing matrices.
* SEFAZ Handshake Resiliency: Modular exceptions handling setup designed to elegantly process timeout states and unexpected government rejection arrays.

## 🚀 Local Deployment Guide
1. Prerequisites
Ensure you have PHP 8.x, Composer, and a relational database engine (e.g., MySQL / PostgreSQL) configured on your local platform host.

2. Dependency Resolution
Clone the codebase repository into your system, enter the root directory, and execute the installation engine:
```bash
composer install
npm install && npm run dev
```

3. Environment Configuration
Duplicate the structural configuration file template to assemble your active runtime environment settings:
```bash
cp .env.example .env
```
⚠️ Important: Open your newly created `.env` file and configure your targeted database credentials, queue drivers, and path variables pointing to your fiscal digital certificates.

4. Database Setup & Encryption Binding
Generate your local application security hash token and run database migrations to seed default tables:
```bash
python artisan key:generate
php artisan migrate
```

5. Launching the Local Instance
Initialize the local background runtime worker and start the built-in development server context:
```bash
php artisan serve
```
The integration gateway interface will run locally at `http://127.0.0.1:8000/`.

## 🔧 Core Tech Stack
* Framework Engine: Laravel (PHP)
* Fiscal Library Wrappers: `sped-nfe` & `sped-da`
* Dependency Automations: Composer (Backend) & NPM (Frontend pipeline)
