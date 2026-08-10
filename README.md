<p align="center">
  <img src="assets/course-evaluation-banner.png" alt="Course Evaluation System Banner" width="100%">
</p>

# University Course Evaluation System

A secure full-stack web application for collecting, managing, and analyzing university course evaluations.

<p align="center">
  <strong>React • TypeScript • Node.js • Express • PostgreSQL • Prisma</strong>
</p>

## About

The **University Course Evaluation System** digitizes the university course evaluation process. Students can securely access enrolled courses and submit anonymous evaluations during active evaluation periods, while administrators can manage evaluation windows, monitor participation, analyze aggregated results, and export evaluation data.

The project was developed with **IBM Bob** as an AI-assisted development tool across the software development lifecycle, including requirements interpretation, implementation, debugging, testing, review, and documentation.

## Key Features

### Student Portal
- Secure student authentication
- View enrolled courses
- View open and submitted evaluation states
- Submit Likert-scale course evaluations
- Add optional written feedback
- Duplicate-submission prevention
- Anonymous evaluation responses

### Administrator Dashboard
- Secure administrator authentication
- View courses and filter by semester
- Create and manage evaluation windows
- Monitor enrollment and response counts
- Automatic response-rate calculation
- Aggregated Likert-scale analytics
- Anonymous written feedback
- CSV export

## Anonymous by Design

Student privacy is enforced structurally.

- `SubmissionRecord` records whether a student submitted an evaluation.
- `Response` and `ResponseAnswer` store the evaluation content.
- Evaluation responses contain **no `studentId` field**.

This allows duplicate-submission prevention without directly linking evaluation answers to individual students.

## Architecture

```text
┌─────────────────────┐       HTTP / REST       ┌──────────────────────┐
│   React Frontend    │ ──────────────────────► │   Express Backend    │
│   Vite + Tailwind   │ ◄────────────────────── │ TypeScript + Prisma  │
│   Port 5173         │       JSON / JWT        │   Port 3001          │
└─────────────────────┘                         └──────────┬───────────┘
                                                         │ Prisma ORM
                                              ┌──────────▼───────────┐
                                              │ PostgreSQL Database  │
                                              │ Port 5432            │
                                              └──────────────────────┘
```

## Technology Stack

**Frontend**
- React 18
- TypeScript
- Vite
- Tailwind CSS
- React Router
- TanStack Query
- Axios

**Backend**
- Node.js
- Express.js
- TypeScript
- Prisma ORM
- JWT
- bcrypt
- Zod

**Database & Documentation**
- PostgreSQL
- Swagger / OpenAPI
- Git & GitHub
- IBM Bob

## IBM Bob & Human Review

IBM Bob supported requirements interpretation, frontend and backend implementation, database integration, debugging, testing, and documentation.

AI output was not accepted automatically. The application was manually tested and reviewed, including:
- Correcting duplicate course cards
- Fixing an invalid **500% response rate**
- Correcting response counts
- Re-testing the complete Student → Database → Admin flow
- Aligning seeded data with actual enrollment
- Updating README documentation after final corrections

Human review remained the final quality gate.

## Responsible AI

Responsible AI considerations included:

- **Privacy:** evaluation answers are separated from student identity.
- **Human oversight:** AI-generated work was manually reviewed and tested.
- **Security:** JWT authentication, bcrypt password hashing, backend validation, role-based authorization, and environment-based configuration.
- **Bias awareness:** course-evaluation results may be influenced by response bias, cultural interpretation, and participation rates.
- **Accessibility:** the application uses semantic and responsive UI practices; a production deployment should undergo a full WCAG 2.1 AA audit.

## Database

The application uses PostgreSQL with Prisma ORM.

The schema covers:
- Users
- Courses
- Enrollments
- Evaluation windows
- Questions
- Responses
- Submission records

Database migrations and seed data are included.

## API Documentation

Swagger UI is available while the backend is running:

```text
http://localhost:3001/api/docs
```

| Group | Base Path | Access |
|---|---|---|
| Authentication | `/api/auth` | Public / Authenticated |
| Student Evaluations | `/api/student/evaluations` | Student |
| Administration | `/api/admin` | Administrator |

## Getting Started

### Prerequisites

- Node.js 18+
- npm 9+
- PostgreSQL 14+ or Docker

### Clone

```bash
git clone https://github.com/judebingadeer/university-course-evaluation-system.git
cd university-course-evaluation-system
```

### Install Dependencies

```bash
npm install
```

### Configure Environment

```bash
cd backend
cp .env.example .env
```

Example:

```env
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/course_eval_db"
JWT_SECRET="YOUR_SECURE_SECRET"
PORT=3001
NODE_ENV=development
```

> Do not commit your real `.env` file to GitHub.

### Prepare Database

```bash
npx prisma migrate dev
npx prisma db seed
```

### Run Backend

```bash
npm run dev
```

Backend:
```text
http://localhost:3001
```

### Run Frontend

Open another terminal:

```bash
cd frontend
npm run dev
```

Frontend:
```text
http://localhost:5173
```

## Demo Accounts

| Role | Username | Password |
|---|---|---|
| Administrator | `admin` | `admin123` |
| Student | `student01` | `password123` |

## Testing

Backend:
```bash
cd backend
npm test
```

Frontend:
```bash
cd frontend
npm test
```

## Project Structure

```text
course-evaluation-system/
├── backend/
│   ├── prisma/
│   │   ├── schema.prisma
│   │   ├── migrations/
│   │   └── seed.ts
│   └── src/
│       ├── controllers/
│       ├── middleware/
│       ├── routes/
│       ├── services/
│       ├── utils/
│       └── __tests__/
├── frontend/
│   └── src/
│       ├── api/
│       ├── components/
│       ├── context/
│       ├── hooks/
│       ├── pages/
│       ├── router/
│       └── types/
├── README.md
├── package.json
└── package-lock.json
```

## Security

- JWT-based authentication
- Role-based authorization
- bcrypt password hashing
- Zod request validation
- Protected routes
- Duplicate-submission prevention
- Anonymous response architecture
- Environment-variable configuration

## Future Improvements

- Advanced analytics dashboards
- Email notifications and reminders
- Multi-university support
- Expanded reporting
- Accessibility improvements
- Production deployment
- Automated data-retention policies

## Project Link

**GitHub:** https://github.com/judebingadeer/university-course-evaluation-system

## Author

**Jude Bin Ghadir**  
Software Engineering Student  
King Saud University

---

<p align="center">
  <strong>Better Feedback. Better Learning.</strong><br>
  Empowering Education Through Data.
</p>
