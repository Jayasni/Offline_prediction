# Offline Field Inspection Management System

An offline-first field inspection management application designed to help organizations manage field assignments, conduct inspections, capture photographic evidence, and monitor inspection progress — even when internet connectivity is unavailable.

The application allows Field Staff to complete inspections offline and synchronize their data with the backend when connectivity is restored. Administrators can manage users and assignments, monitor inspection progress, and review submitted inspection reports.

## Key Features

### 1. Authentication and User Management
- Secure user authentication.
- JWT-based authentication.
- Role-based access control.
- Admin and Field Staff access.
- User management and account status management.

### 2. Assignment Management
- Admin can create and manage inspection assignments.
- Assign inspections to Field Staff.
- View assignment details and assigned staff.
- Track assignment and inspection statuses.

### 3. Field Inspection Management
- Field Staff can view assigned inspections.
- Start and complete inspections.
- Fill inspection checklists.
- Add inspection remarks.
- Save inspection drafts locally.
- Submit completed inspections for Admin review.

### 4. Offline-First Functionality
- Store inspection drafts in browser IndexedDB.
- Continue working without an internet connection.
- Preserve locally saved inspection data.
- Store pending operations in a synchronization outbox.
- Automatically attempt synchronization when internet connectivity returns.
- Retain local data when synchronization fails.

### 5. Photo Capture and Management
- Capture or select inspection photographs.
- Store image files locally as Blob data in IndexedDB.
- Associate photographs with inspection records.
- Upload pending photographs when connectivity is restored.
- Preserve local photographs until successful synchronization.

### 6. Automatic Data Synchronization
- Synchronize pending inspection operations with the backend.
- Synchronize inspection photographs separately.
- Use stable operation IDs for duplicate-request protection.
- Handle version conflicts.
- Mark local records as synchronized after server acknowledgement.

### 7. Admin Inspection Management
- View inspection assignments in one dashboard.
- Monitor inspection progress.
- Identify inspections that have not started.
- View submitted inspections.
- Review inspection remarks and evidence.
- Approve or reject inspections.
- Request corrections from Field Staff.
- Initiate revisits when required.

### 8. Inspection Status Workflow

| Status | Description |
|---|---|
| Assigned | Inspection assigned to Field Staff |
| In Progress | Field Staff has started the inspection |
| Submitted | Inspection submitted for review |
| Approved | Admin approved the inspection |
| Correction Requested | Admin requested changes |
| Rejected | Inspection rejected by Admin |
| Revisit Required | Another inspection visit is required |

## Application Workflow

1. Admin logs into the application.
2. Admin creates an inspection assignment.
3. Admin assigns the inspection to Field Staff.
4. Field Staff logs in and views assigned inspections.
5. Field Staff starts the inspection.
6. Checklist responses, remarks and photographs are saved locally.
7. Field Staff submits the completed inspection.
8. Pending inspection data and photographs synchronize with the backend when connectivity is available.
9. Admin views the submitted inspection.
10. Admin reviews the inspection and approves, rejects or requests corrections.
11. If necessary, Admin requests a revisit.

## Technology Stack

### Frontend
- React.js
- TypeScript
- Vite
- React Router
- Dexie.js
- IndexedDB
- HTML5
- CSS3
- Progressive Web App (PWA)

### Backend
- Python
- FastAPI
- SQLAlchemy 2
- Pydantic
- JWT Authentication
- Password Hashing

### Database
- PostgreSQL

### Offline Storage
- IndexedDB
- Dexie.js
- Browser Local Storage where applicable

### Development and Deployment
- Git
- GitHub
- Docker
- Docker Compose
- Pytest
- Vitest

## System Architecture

```text
                  React Frontend
                       |
             ----------------------
             |                    |
        Online Mode           Offline Mode
             |                    |
             |               IndexedDB
             |                    |
             |               Local Outbox
             |                    |
             -----------|----------
                        |
                 FastAPI Backend
                        |
               Authentication
                        |
                Business Logic
                        |
                 PostgreSQL
                        |
              Inspection Records
                        |
                Photo Storage
```

## Project Structure

```text
offline-field-inspection/
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── api.ts
│   │   ├── db.ts
│   │   ├── types.ts
│   │   └── App.tsx
│   ├── package.json
│   └── vite.config.ts
│
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── models.py
│   │   ├── schemas.py
│   │   └── security.py
│   └── requirements.txt
│
├── docs/
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

*The structure above is illustrative; actual folders and filenames may vary in the repository.*

## Installation and Setup

### Prerequisites

Install the following tools:

- Python 3.10+
- Node.js and npm
- PostgreSQL
- Git
- Docker Desktop (optional)

### 1. Clone the Repository

```bash
git clone https://github.com/Jayasni/Offline_prediction.git

cd Offline_prediction
```

### 2. Backend Setup

```bash
cd backend

python -m venv .venv
```

Activate the virtual environment.

Windows:

```powershell
.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Configure your database connection and environment variables.

Start the backend:

```bash
uvicorn app.main:app --reload --port 8000
```

Backend API:

```text
http://localhost:8000
```

API documentation:

```text
http://localhost:8000/docs
```

### 3. Frontend Setup

Open another terminal:

```bash
cd frontend

npm install

npm run dev
```

Frontend:

```text
http://localhost:5173
```

### 4. Run Using Docker

If Docker Compose is configured in your project:

```bash
docker compose up --build
```

Configure your environment variables before starting the application.

## Offline Synchronization Workflow

The application is designed to protect inspection data during network interruptions.

**When offline:**
- Inspection details are stored in IndexedDB.
- Checklist answers and remarks are saved locally.
- Photographs are stored as Blob objects.
- Pending operations remain in the local outbox.

**When online:**
- The application attempts to synchronize pending inspection operations.
- The backend validates incoming data.
- Photo uploads are processed.
- Local records are marked synchronized after successful acknowledgement.

**Important:** Browser storage is device-local. Clearing browser data or losing the device can result in data loss. Regular backups and production-grade storage policies are necessary.

## API Documentation

FastAPI provides interactive API documentation.

After starting the backend, open:

```text
http://localhost:8000/docs
```

The API includes functionality for:

- Authentication
- User management
- Assignment management
- Inspection management
- Photo uploads
- Offline synchronization
- Inspection review
- Revisit management

Refer to the interactive API documentation for the actual available endpoints and request schemas.

## Testing

Backend:

```bash
cd backend

pytest
```

Frontend:

```bash
cd frontend

npm run test
```

Run the tests supported by your current project configuration. Record actual test results before describing the application as fully tested.

## Security Considerations

- Use strong JWT secrets.
- Change default credentials.
- Keep API keys and database passwords out of GitHub.
- Configure HTTPS in production.
- Enforce backend authorization and inspection ownership checks.
- Protect uploaded photographs and inspection data.
- Configure database backups.
- Establish data retention and recovery policies.

Never commit `.env` files or sensitive credentials to the repository.

## Future Improvements

- Advanced inspection analytics.
- Dashboard reporting and export.
- Improved offline conflict resolution.
- Push notifications.
- Image compression and upload optimization.
- Advanced audit logging.
- Production deployment and monitoring.

## Project Purpose

The main objective of this project is to simplify field inspection operations by combining offline data collection, digital inspection workflows, photographic evidence, and centralized administrative monitoring.

The system helps field teams continue their work without depending on continuous internet connectivity while allowing administrators to monitor and review inspection activities after synchronization.

## Repository

GitHub: https://github.com/Jayasni/Offline_prediction

---

**Offline Field Inspection Management System**

*Inspect Offline. Sync Automatically. Manage Efficiently.*
