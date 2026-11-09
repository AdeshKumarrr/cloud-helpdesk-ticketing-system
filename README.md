# Cloud-Based Helpdesk / Ticketing System

A cloud-ready support portal where users submit support requests and administrators manage, prioritize, reply to, and resolve tickets.

## Features
- User registration and login with bcrypt password hashing
- User and administrator roles
- Ticket creation with category, description and priority
- Unique ticket reference numbers
- Status workflow: Open, In Progress, Resolved and Closed
- Admin ticket management and status/priority updates
- Ticket replies and conversation history
- Dashboard statistics
- Optional email notifications using SMTP
- PostgreSQL storage and PostgreSQL-backed sessions
- Health endpoint: `/api/health`

## Stack
HTML, CSS, JavaScript, Node.js, Express.js, PostgreSQL, Express Session, bcryptjs and Nodemailer.

## Run locally
1. Install Node.js 20+ and PostgreSQL.
2. Create a database named `helpdesk`.
3. Copy `.env.example` to `.env` and configure `DATABASE_URL` and `SESSION_SECRET`.
4. Run `npm install` and `npm start`.
5. Open `http://localhost:3000`.

The initial administrator is created from `ADMIN_NAME`, `ADMIN_EMAIL` and `ADMIN_PASSWORD` if that email does not exist. Two demo accounts are also seeded automatically if they do not already exist:\n\n| Role | Email | Password |\n|---|---|---|\n| Admin | `admin.demo@helpdesk.test` | `Admin@12345` |\n| User | `user.demo@helpdesk.test` | `User@12345` |\n\nThese demo credentials are intentionally visible for internship evaluation only. Do not use them for real or sensitive data. Remove the demo seed block or change the credentials before production use. Never commit `.env`.

## Render deployment
1. Create a PostgreSQL database in Render.
2. Create a Web Service connected to this repository.
3. Build command: `npm install`; Start command: `npm start`.
4. Add `NODE_ENV=production`, `DATABASE_URL` (Render PostgreSQL URL), `SESSION_SECRET` (long random value), `ADMIN_NAME`, `ADMIN_EMAIL` and `ADMIN_PASSWORD`.
5. Deploy and check `/api/health`.

Optional SMTP settings: `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASSWORD`, `SMTP_FROM`. Notifications are skipped until SMTP is configured.

## API overview
`POST /api/auth/register`, `POST /api/auth/login`, `POST /api/auth/logout`, `GET /api/profile`, `GET /api/dashboard`, `GET /api/tickets`, `POST /api/tickets`, `GET /api/tickets/:id`, `POST /api/tickets/:id/replies`, `PATCH /api/tickets/:id` (admin only), `GET /api/health`.

This is an internship learning project. Before production use, add rate limiting, CSRF protection, audit logging, automated tests, attachment scanning and a privacy policy.
