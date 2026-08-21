# CivicPulse

CivicPulse is a full-stack web application that gives residents a simple way to report local civic problems — potholes, overflowing garbage bins, broken streetlights, water leaks, and similar issues — and lets local administrators track and resolve them from one dashboard.

Citizens report a problem; admins see it and update its status. Both sides can check on the same issue at any point.

## What it does

**For residents (citizens):**
- Create an account and sign in securely
- Submit a new issue with a title, description, category, and photo evidence
- Pin the exact location of the issue on an interactive map
- Track the status of submitted issues (Reported → In Progress → Resolved/Rejected)
- View and manage a personal profile and issue history

**For administrators:**
- Sign in to a dedicated admin dashboard
- View all reported issues across the area, with filtering by type and status
- Update the status of an issue as it moves through the resolution pipeline
- See the full history of status changes on each issue
- Manage an admin profile

## How it's built

The project is split into two independently deployable pieces:

```
CivicPulse-rebranded/
├── backend/     Express + TypeScript API, MongoDB via Mongoose
├── frontend/    React + TypeScript client, built with Vite
└── Assets/      Reference UI mockups
```

### Backend

- **Runtime/Framework:** Node.js, Express 5, TypeScript
- **Database:** MongoDB with Mongoose ODM
- **Auth:** JWT-based authentication with cookie sessions, bcrypt password hashing
- **Media storage:** Cloudinary, via Multer for upload handling
- **Validation:** Zod schemas on incoming requests

Core data models include citizens, admins, issues, issue status history, and multimedia attachments. Routes are split by responsibility: `citizen.routes.ts`, `admin.routes.ts`, and `issue.routes.ts`.

### Frontend

- **Framework:** React 19 with TypeScript, bundled by Vite
- **Styling/UI:** Tailwind CSS with shadcn/ui-style components (Radix primitives)
- **Data fetching:** TanStack Query + Axios
- **Forms:** React Hook Form with Zod validation
- **Maps:** Mapbox GL for pinning and displaying issue locations
- **Routing:** React Router
- **Motion/UX polish:** Framer Motion, Lottie animations, Sonner toasts

Pages cover the full citizen and admin experience: landing page, sign in/sign up, citizen home & profile, report-issue flow, admin home & profile, and a 404 fallback.

## Getting started

### Prerequisites

- Node.js (LTS recommended)
- A MongoDB connection string (local instance or Atlas)
- A Cloudinary account (for storing issue photos)
- A Mapbox access token (for the map/location picker)

### 1. Clone and install

```bash
git clone <your-repo-url>
cd CivicPulse-rebranded

# Backend
cd backend
npm install

# Frontend
cd ../frontend
npm install
```

### 2. Configure environment variables

**backend/.env**
```
DATABASE_URL=your_mongodb_connection_string
JWT_PASSWORD=your_jwt_secret
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
CORS_ORIGIN=http://localhost:5173
PORT=5000
```

**frontend/.env**
```
VITE_MAPBOXGL_ACCESS_TOKEN=your_mapbox_access_token
```

### 3. Run in development

```bash
# Terminal 1 — backend
cd backend
npm run dev

# Terminal 2 — frontend
cd frontend
npm run dev
```

The frontend will typically be available at `http://localhost:5173`, and the API at `http://localhost:5000`.

### 4. Build for production

```bash
# Backend
cd backend
npm run build
npm start

# Frontend
cd frontend
npm run build
npm run preview
```

## Issue lifecycle

Every reported issue moves through a set of statuses, and each change is recorded in its status history:

`Reported` → `Pending` / `In Progress` → `Resolved` or `Rejected`

## License

See the `LICENSE` file in this repository for details.

## Contributing

Issues and pull requests are welcome. If you're proposing a larger change, please open an issue first to discuss what you'd like to change.
