# Notes Manager

A personal **note-taking web app** built with **Laravel 11**, **Blade**, **Tailwind CSS**, and **Alpine.js**. Each user gets a private space to organize notes into categories, search them, and manage their account. Authentication is scaffolded with **Laravel Breeze**.

## Features

- **Authentication** (Laravel Breeze): register, login, logout, password reset, email verification
- **Profile management**: update name, email, and password, or delete the account
- **Categories**: create, search, and delete your own categories
- **Notes**: create, search, update, and delete notes, each assigned to a category
- **Per-user data isolation**: users only ever see their own categories and notes
- Cascade deletes: removing a category removes its notes
- Responsive UI with Tailwind CSS and Alpine.js

## Tech Stack

| Layer     | Technology |
| --------- | ---------- |
| Backend   | PHP 8.2+, Laravel 11 |
| Auth      | Laravel Breeze |
| Frontend  | Blade templates, Tailwind CSS 3, Alpine.js |
| Build     | Vite |
| Database  | MySQL or SQLite |

## Data Model

```
User ──< Category ──< Note
  └───────────────────<┘
```

| Table        | Key fields |
| ------------ | ---------- |
| `categories` | `name`, `user_id` |
| `notes`      | `title`, `content`, `user_id`, `category_id` |

## Project Structure (highlights)

```
app/Http/Controllers/
├── CategoryController.php     # list/search, store, destroy
├── NoteController.php         # list/search, store, update, destroy
└── ProfileController.php
resources/views/
├── dashboard.blade.php        # Categories overview
├── categories/index.blade.php
├── notes/index.blade.php
└── auth/, profile/, layouts/, components/   # Breeze scaffolding
routes/web.php                 # Resource routes for categories & notes
```

## Getting Started

### Prerequisites

- PHP 8.2+ and [Composer](https://getcomposer.org/)
- [Node.js](https://nodejs.org/) and npm
- MySQL (or SQLite)

### Installation

```bash
git clone https://github.com/SifeYassine/notes-manager.git
cd notes-manager

composer install
npm install

cp .env.example .env
php artisan key:generate
```

### Configure the database

By default `.env.example` uses SQLite. To use MySQL instead:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=notes_manager
DB_USERNAME=root
DB_PASSWORD=
```

### Migrate and seed

```bash
php artisan migrate
php artisan db:seed    # optional: creates a test user (test@example.com / password)
```

### Run

Run the frontend build and the Laravel server in two terminals:

```bash
npm run dev
```

```bash
php artisan serve
```

Open <http://127.0.0.1:8000>, register an account, and start organizing your notes.

## Routes

| Method | URI                   | Action |
| ------ | --------------------- | ------ |
| GET    | `/dashboard`          | Categories overview (auth) |
| GET    | `/categories`         | List / search categories |
| POST   | `/categories`         | Create a category |
| DELETE | `/categories/{id}`    | Delete a category |
| GET    | `/notes`              | List / search notes |
| POST   | `/notes`              | Create a note |
| PUT    | `/notes/{id}`         | Update a note |
| DELETE | `/notes/{id}`         | Delete a note |
| GET/PATCH/DELETE | `/profile`  | Manage profile |

## Author

**Sifeddine Yassine** · [@SifeYassine](https://github.com/SifeYassine)
