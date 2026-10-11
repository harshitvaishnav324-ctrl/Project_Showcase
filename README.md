
[README.md](https://github.com/user-attachments/files/33304785/README.md)
# 🎓 Project Showcase System

### A web-based platform for showcasing student projects, team collaboration, faculty review, and academic insights.

The **Project Showcase System** is an academic web application designed to bring student project submissions, collaboration, review, and discovery into one place. Students can create or join groups and submit projects for faculty review. Approved submissions appear in a searchable project catalogue, while discussions and analytics support academic engagement and oversight.

> **Project status:** Academic prototype. The repository's database schema, authorization policies, and deployment setup must be verified and completed before institutional or production use.

## ✨ Features

### 👨‍🎓 Students
- Register, sign in, and sign out.
- Create groups or join existing groups using an invitation mechanism.
- Submit projects associated with a group.
- View project information and team attribution.
- Explore approved projects and filter by title or department.
- Create forum discussions, reply to posts, and like discussions.

### 👩‍🏫 Faculty
- View submitted projects through a review interface.
- Approve or reject projects.
- Access project-related analytics when permitted by the interface.

### 📊 Project discovery and insights
- Approved-project catalogue and project-detail pages.
- Department and submission-status summaries.
- Monthly project-submission visualizations.
- Faculty directory interface (currently populated with demonstration data).

## 🛠️ Tech Stack

| Layer | Technology |
| --- | --- |
| Frontend | React 19, JavaScript, JSX, CSS |
| Routing | React Router 7 |
| Build tool | Vite 7 |
| Authentication and data | Supabase and `@supabase/supabase-js` |
| Charts | Recharts |
| Icons | Lucide React |
| Linting | ESLint |
| Supporting API scaffold | Python, FastAPI, Uvicorn, Pydantic |

## 🏗️ Architecture

The implemented frontend uses a **React → Supabase** data path for authentication and database operations. Its main workflow is:

```text
Student registers/signs in
          ↓
Creates or joins a group
          ↓
Submits a project (pending)
          ↓
Faculty reviews the submission
          ↓
   Approved / Rejected
          ↓
Approved projects appear in the catalogue
```

A separate FastAPI scaffold is included in the project archive, but the reviewed React pages do not call its endpoints. Its data-persistence operations are not yet implemented.

## 🚀 Getting Started

### Prerequisites

- Node.js and npm compatible with the project's Vite version
- A Supabase project
- Git (optional, for cloning)

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

Alternatively, download the repository as a ZIP and extract it.

### 2. Install dependencies

From the directory containing `package.json`:

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file in the frontend project directory:

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_public_anon_key
```

The frontend reads these variables through its shared Supabase client in `src/lib/supabase.js`.

**Important:** Only use a browser-safe Supabase public/anon key here. Never put a service-role key or other privileged secret in `VITE_` variables. Keep `.env` out of Git, and configure Supabase Row Level Security (RLS) and trusted role assignment before allowing real users to access data.

### 4. Configure the database

The reviewed project archive does **not** include database migrations or verified access policies. Before the full workflow can work, create the required Supabase tables, relationships, and policies corresponding to the application's queries. Refer to the project source and academic report for the intended data model.

Referenced data entities include:

- `projects`
- `groups`
- `group_members`
- `discussions`
- `discussion_comments`
- `discussion_likes`

Do not assume the application is secure or functional simply because the frontend starts.

### 5. Start the frontend

```bash
npm run dev
```

Open the local URL displayed by Vite in your terminal.

### Other frontend commands

```bash
npm run build    # Generate production frontend assets
npm run preview  # Preview the production build locally
npm run lint     # Run configured ESLint checks
```

## 🐍 Optional FastAPI Scaffold

The project also contains a supporting Python API scaffold under `backend/`. It exposes project and review endpoint definitions but does not yet provide working persistent storage for them.

If you want to explore this component, install its requirements in a Python virtual environment:

```bash
cd backend
python -m venv .venv
```

Activate the environment and run:

```bash
pip install -r requirements.txt
uvicorn main:app --reload
```

The backend optionally accepts `FRONTEND_URL` for CORS configuration. **Running this service is not required by the inspected React-to-Supabase workflow.**

## 📌 Current Limitations

The source review identified several areas that require additional work:

- Missing reproducible database migration scripts and verified RLS policies.
- Faculty privileges depend partly on frontend/user metadata; privileged roles need trusted server-side enforcement.
- Project image selection does not implement image uploading and storage.
- The faculty directory currently uses demonstration profiles rather than persistent records.
- Faculty review changes project status without a full review audit history.
- The FastAPI scaffold returns placeholder data rather than writing to persistent storage.
- Automated tests and production performance results were not supplied in the reviewed archive.

## 🔮 Future Enhancements

- Database schema migrations, constraints, and comprehensive Row Level Security.
- Verified faculty onboarding and role-based authorization.
- Project attachments and image uploads using managed storage.
- Review history with reviewer identity, feedback, and timestamps.
- Improved validation, error handling, and concurrent-update protection.
- Automated unit, integration, and access-control tests.
- Pagination, server-side analytics, and performance monitoring.
- Persistent faculty profiles and discussion moderation.

## 🎯 Project Objective

The goal of the Project Showcase System is to replace fragmented project submissions and informal review channels with a structured platform for student collaboration, transparent project status, and discoverable academic work.

## 📄 Documentation

For more information about the design, requirements, conceptual database model, testing plan, and implementation findings, see the **Project Showcase System Academic Project Report**.

---

**Built as an academic project to support student innovation, collaboration, and project discovery.**
