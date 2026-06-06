# ProjectNest Server ⚙️

This is the backend server for **ProjectNest**, built using **Node.js**, **Express**, **MongoDB** (with Mongoose), and **Socket.io** for real-time collaboration.

## 🛠️ Tech Stack & Key Modules
- **Runtime Environment**: Node.js
- **Web Framework**: Express
- **Database ODM**: Mongoose (MongoDB)
- **Real-time WebSockets**: Socket.io
- **Security & Auth**:
  - `bcrypt` / `bcryptjs` for secure password hashing.
  - `jsonwebtoken` (JWT) for secure, stateless token authentication.
- **Middleware & Utility**:
  - `multer` for managing multi-part form data (used for PDF uploads and profile images).
  - `morgan` for HTTP request logging.
  - `validator` for input sanity checks (e.g., emails).

---

## 🗺️ API Routes Overview

All routes are prefix-configured in `app.js` under `/api/v2`:

### 1. Authentication & Users (`/api/v2/user`)
- `POST /login`: Log in user and generate JWT token.
- `POST /signup` *(Admin only)*: Register new team member or manager accounts.
- `POST /update-my-password`: Update authenticated user's password.
- `PATCH /update-my-info`: Update user info (e.g. name).
- `POST /:id/assign-role`: Assign different access roles (Team Member, Project Manager, Administrator).

### 2. Project Requests / Workspace Proposals (`/api/v2/projectreq`)
Handles the request workflow where team members propose new project workspaces, and managers or admins approve them:
- `GET /`: Retrieve all workspace proposals.
- `POST /`: Submit a new workspace proposal.
- `PATCH /:id`: Update proposal status (e.g. approve/reject).

### 3. Projects (`/api/v2/project`)
Core resource representing ongoing workspaces/group tasks:
- `GET /my-projects`: Fetch all projects belonging to the logged-in user.
- `GET /:id`: Details of a specific project workspace.
- `POST /:id/task`: Assign a new task to team members.
- `PATCH /:id/task/review`: Project Manager reviews and approves completed tasks.
- `GET /:id/log-sheet`: Retrieve meeting logs / progress notes.
- `POST /:id/log-sheet/:date`: Log progress updates or meeting minutes.
- `PATCH /:id/proposal` / `PATCH /:id/report`: Upload project files/documents via Multer.

### 4. Events / Logs (`/api/v2/event`)
Manage workspace events and timeline alerts.

---

## 💬 Socket.io Integration
The application listens on port `8001` for real-time events. Key events supported:
- `join-room`: Groups socket clients into rooms defined by their `projectId`.
- `send-message` & `receive-message`: Facilitates real-time group chat inside project workspaces.

---

## 🚀 Running the Server

### 1. Environment Configurations
Create a `config.env` file in this directory based on the variables listed in `config.env.template`:
```env
PORT=3000
MONGODB_URI=mongodb://localhost:27017/projectnest
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPRIES_IN=90d
JWT_COOKIE_EXPIRES_IN=90
NODE_ENV=development
```

### 2. Installation
Install all dependencies:
```bash
npm install
```

### 3. Execution
- **Development mode** (with nodemon hot-reloading and `--env-file` integration):
  ```bash
  npm run dev
  ```
- **Production mode**:
  ```bash
  npm run start
  ```
