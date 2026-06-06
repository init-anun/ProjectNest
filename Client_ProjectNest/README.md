# ProjectNest Client 🌐

This is the frontend React client for **ProjectNest**, bootstrapped with **React**, **Vite**, and **Tailwind CSS**. It provides a fully interactive interface for managing online group tasks and workspaces.

## 🛠️ Tech Stack & Key Libraries
- **Bundler & Tooling**: Vite
- **UI Framework**: React (v18)
- **Styling**: Tailwind CSS, PostCSS
- **State Management & Contexts**:
  - `userContext` for authentication state and user details.
  - `ProjectContext` for handling project-related states.
  - `socketContext` for managing real-time WebSocket connection to the server.
- **Routing**: React Router DOM (v6) with Protected Routes and Role-based Gatekeeping.
- **Data Fetching**: Axios
- **Real-time Engine**: Socket.io Client
- **Progress Visualization**: React Circular Progressbar
- **Interactive UI**: React Icons, Tailwind Datepicker, tsParticles

---

## 📂 Project Structure

Within the `src/` directory, code is organized as follows:

- **`components/`**: Modular, reusable UI components.
  - `Admin/`: Specific workspace admin components.
  - `student/`: Group Member (Member role) dashboard views, proposal forms, task checkers, document lists, and logsheet editors.
  - `supervisor/`: Project Manager (Manager role) panels, task assigners, logsheet verifiers, and chat components.
  - `Login/`: Authentication UI.
  - Common components like `NavBar`, `Profile`, `SearchBar`, and `Calendar`.
- **`contexts/`**: Context Providers (`ProjectContext`, `socketContext`, `userContext`) to manage global states.
- **`pages/`**: Primary page screens mapped to routes (e.g. `LoginPage`, `StudentDashboard` / Member Dashboard, `SupervisorDashboard` / Manager Dashboard, `AdminPage`, `ProjectPage`).
- **`utils/`**: Helper files, authentication routing filters (`ProtectedRoutes.jsx` and `RoleProtectedRoutes.jsx`).

---

## 🚀 Running the Client

### 1. Installation
Navigate to this directory and install required npm modules:
```bash
npm install
```

### 2. Running in Development Mode
To start the React development server:
```bash
npm run dev
```
By default, this launches the client on `http://localhost:5173`.

### 3. Running with Mock Data (JSON-Server)
The frontend includes a mock JSON-server integration that reads from `data/projects.json` on port `9000`. You can start this service for isolated testing:
```bash
npm run server
```

### 4. Build for Production
To bundle the frontend application for production:
```bash
npm run build
```
The output files will be compiled into the `dist/` directory.

---

## 💡 Key Routing Map
- `/login`: The landing page where users authenticate.
- `/app/student`: Main hub for Group Members (Member role).
- `/app/student/project/:projectId`: Main project workspace for group members, with tabs for:
  - `stdtasks`: View progress and status of assigned tasks.
  - `stdmember`: Browse team members and contact information.
  - `stdlogsheets`: Log and submit meeting updates/agendas.
  - `stdchats`: Real-time group chat.
  - `stddocuments`: View, upload, and download project files and reports.
- `/app/supervisor`: Dashboard containing active workspaces managed by the Group Leader (Manager role).
- `/app/supervisor/projects/:projectId`: Workspace for Project Managers to assign tasks, check meeting logs, review files, and chat with the group.
- `/app/admin`: Central admin panel containing workspace requests, active/deleted archives, and project details.
