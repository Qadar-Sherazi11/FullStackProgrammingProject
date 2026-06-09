# Nexus CRM - MERN + Next.js

A full-featured Customer Relationship Management system built with MongoDB, Express.js, React (Next.js), and Node.js.

## Project Structure

```text
nexus-crm/
  backend/          Express.js + MongoDB API
    models/         Mongoose schemas (User, Customer, Invoice)
    routes/         API routes (auth, customers, invoices, dashboard)
    middleware/     JWT auth middleware
    server.js       Express entry point
    seed.js         Database seeder
  frontend/         Next.js app
    pages/          Login, register, dashboard, customers, invoices, settings
    components/     Layout, Chatbot, CustomerForm, withAuth HOC
    context/        AuthContext (JWT management)
    lib/            Axios API client
    styles/         Global CSS
```

## Features

| Feature | Status |
|---|---|
| JWT authentication (register/login/logout) | Done |
| Protected routes | Done |
| Customer CRUD (add, view, edit, delete) | Done |
| Seeded customer records | Done |
| Search customers by name | Done |
| Filter by status (Lead/Active/Inactive) | Done |
| Invoice generation with PDF download | Done |
| Toast notifications | Done |
| Rule-based chatbot assistant | Done |
| Dashboard with stats | Done |
| Responsive UI | Done |

## Prerequisites

- Node.js 18+
- MongoDB (local or MongoDB Atlas)
- npm

## Setup

From the project root:

```bash
cd nexus-crm
```

Install dependencies:

```bash
npm run install:all
```

Create `backend/.env` from `backend/.env.example`:

```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/nexus-crm
JWT_SECRET=replace_this_with_a_secure_secret
JWT_EXPIRE=7d
FRONTEND_URL=http://localhost:3000
```

Create `frontend/.env.local` from `frontend/.env.local.example`:

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

Seed the database:

```bash
npm run seed
```

Start the backend:

```bash
npm run dev:backend
```

Start the frontend in another terminal:

```bash
npm run dev:frontend
```

Backend: http://localhost:5000
Frontend: http://localhost:3000

## Demo Login

After seeding, use:

| Field | Value |
|---|---|
| Email | admin@nexuscrm.com |
| Password | admin123 |

## API Endpoints

### Auth

- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login
- `GET /api/auth/me` - Get the current user (protected)

### Customers

- `GET /api/customers` - List customers, supports `?search=&status=&page=&limit=`
- `GET /api/customers/:id` - Get one customer
- `POST /api/customers` - Create a customer
- `PUT /api/customers/:id` - Update a customer
- `DELETE /api/customers/:id` - Delete a customer

### Invoices

- `GET /api/invoices` - List invoices
- `GET /api/invoices/:id` - Get one invoice
- `POST /api/invoices` - Create an invoice
- `DELETE /api/invoices/:id` - Delete an invoice
- `GET /api/invoices/:id/pdf` - Download a PDF invoice

### Dashboard

- `GET /api/dashboard/stats` - Get summary stats

## Chatbot Commands

The built-in rule-based assistant responds to:

| Command | Action |
|---|---|
| `hello` / `hi` | Greeting |
| `help` | Show all commands |
| `show customers` | Navigate to customers |
| `add customer` | Open add customer form |
| `create invoice` | Open invoice page |
| `dashboard` | Navigate to dashboard |
| `customer count` | Show customer stats |
| `show invoices` | Navigate to invoices |

## Notes

- Protected API routes require a bearer JWT.
- Passwords are hashed with bcryptjs.
- Customer emails are unique.
- Invoice numbers are generated without relying on document counts.
- PDF generation is server-side using PDFKit.
- Tax is calculated at 10% automatically.
