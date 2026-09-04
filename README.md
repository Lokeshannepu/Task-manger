# Task Manager — MERN Stack CRUD App

A full-stack task management application built with MongoDB, Express.js, React, and Node.js. Users can create, view, update, and delete tasks, each with a title, description, and status (pending / in-progress / completed).

## Features

- User registration and login with hashed passwords (bcrypt) and JWT-based authentication
- Tasks are scoped per user — each user only sees and manages their own tasks
- RESTful API built with Express and Mongoose
- Full CRUD operations (Create, Read, Update, Delete) on tasks
- React frontend with component-based architecture (`AuthForm`, `TaskForm`, `TaskList`)
- Axios-based API layer with an interceptor that attaches the JWT to every request
- MongoDB schema validation (required title, enum-restricted status)
- Environment-based configuration for both frontend and backend

## Tech Stack

| Layer      | Technology                  |
|------------|------------------------------|
| Frontend   | React, Axios, CSS            |
| Backend    | Node.js, Express.js          |
| Database   | MongoDB, Mongoose            |

## Project Structure

```
mern-task-manager/
├── backend/
│   ├── controllers/
│   │   ├── authController.js
│   │   └── taskController.js
│   ├── middleware/
│   │   └── auth.js
│   ├── models/
│   │   ├── Task.js
│   │   └── User.js
│   ├── routes/
│   │   ├── auth.js
│   │   └── tasks.js
│   ├── server.js
│   ├── package.json
│   └── .env.example
└── frontend/
    ├── public/
    │   └── index.html
    ├── src/
    │   ├── components/
    │   │   ├── AuthForm.js
    │   │   ├── TaskForm.js
    │   │   └── TaskList.js
    │   ├── services/
    │   │   └── api.js
    │   ├── App.js
    │   ├── App.css
    │   └── index.js
    ├── package.json
    └── .env.example
```

## Getting Started

### Prerequisites

- Node.js (v18 or higher recommended)
- MongoDB running locally, or a free MongoDB Atlas cluster

### 1. Clone and install

```bash
git clone https://github.com/<your-username>/mern-task-manager.git
cd mern-task-manager
```

### 2. Backend setup

```bash
cd backend
npm install
cp .env.example .env
# Edit .env if your MongoDB URI is different (e.g. an Atlas connection string)
npm run dev
```

The API runs on `http://localhost:5000` by default.

### 3. Frontend setup

Open a new terminal:

```bash
cd frontend
npm install
cp .env.example .env
npm start
```

The app runs on `http://localhost:3000` and talks to the backend API.

## API Endpoints

| Method | Endpoint            | Auth required | Description           |
|--------|----------------------|:--------------:|------------------------|
| POST   | /api/auth/register   | No             | Create a new account   |
| POST   | /api/auth/login      | No             | Log in, get a JWT      |
| GET    | /api/tasks           | Yes            | Get your tasks         |
| GET    | /api/tasks/:id       | Yes            | Get a single task      |
| POST   | /api/tasks           | Yes            | Create a new task      |
| PUT    | /api/tasks/:id       | Yes            | Update a task          |
| DELETE | /api/tasks/:id       | Yes            | Delete a task          |

Task routes require an `Authorization: Bearer <token>` header — the frontend handles this automatically once you're logged in.

**Important:** before running the backend, set `JWT_SECRET` in `backend/.env` to a long random string of your own (not the placeholder value in `.env.example`).

## What I Learned Building This

- Structuring an Express API using the MVC pattern (models / controllers / routes)
- Implementing JWT-based authentication: hashing passwords with bcrypt, issuing and verifying tokens, and protecting routes with middleware
- Connecting React to a Node/Express backend via a dedicated Axios service layer, including an interceptor that attaches auth tokens automatically
- Handling async state in React (loading, error, and success states)
- Designing MongoDB schemas with validation and relationships (tasks referencing their owning user) using Mongoose

## Possible Improvements

- Add user authentication (JWT) so tasks are scoped per user
- Add due-date sorting and filtering by status
- Deploy backend to Render/Railway and frontend to Vercel/Netlify
- Add unit tests (Jest + React Testing Library, Supertest for the API)

## License

MIT
