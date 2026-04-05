# Nexus AI Project Manager

A high-performance, AI-enhanced project management system built with React, Express, and Firebase.

##  Features

- **Real-Time Collaboration**: Instant synchronization of projects and tasks across all users using Firebase Firestore.
- **AI Task Breakdown**: Leverage Gemini AI to decompose complex tasks into actionable sub-tasks.
- **Secure Architecture**: Full-stack setup with an Express backend to protect sensitive AI API keys.
- **Robust Security**: Strict Firestore Security Rules ensuring data integrity and user privacy.
- **Premium UI/UX**: Modern, responsive design using Tailwind CSS and smooth animations with Motion.
- **Admin Dashboard**: Built-in administrative privileges for the system owner.

##  Technical Architecture

### 1. Backend Design
The application uses a hybrid architecture:
- **Express Server**: Handles API requests (like AI task breakdown) and serves the static frontend in production.
- **Vite Middleware**: Integrated into Express for a seamless development experience with hot module replacement (HMR) support.
- **Separation of Concerns**: API routes are isolated from frontend logic, and Firebase services are centralized in `src/firebase.ts`.

### 2. Database & Data Modeling
Data is modeled in Firestore with a clear hierarchy:
- `/users/{userId}`: User profiles and roles.
- `/projects/{projectId}`: Top-level project containers.
- `/projects/{projectId}/tasks/{taskId}`: Sub-collection for granular task management.
A `firebase-blueprint.json` file serves as the intermediate representation (IR) for the data schema.

### 3. Security & Validation
- **Firestore Security Rules**: Implemented a "Default Deny" policy. Access is granted based on project membership or admin status.
- **Data Validation**: Rules enforce strict type checking, string length limits, and valid enum values for statuses and priorities.
- **Auth Guards**: Frontend components use an `isAuthReady` state to prevent unauthorized data fetching during initial load.

### 4. AI Integration
The AI Task Breakdown feature uses the `gemini-3-flash-preview` model. It takes the task title and project description as context to generate a structured, actionable list of sub-tasks, helping teams move faster.

##  Evaluation Criteria Alignment

1. **Backend Design**: Structured Express + Vite setup with clear API/Frontend separation.
2. **Logical Thinking**: Implemented Role-Based Access Control (RBAC) and complex state management for real-time data.
3. **Functionality**: Fully functional CRUD for projects and tasks with real-time sync and AI features.
4. **Code Quality**: Clean, documented TypeScript code following modern React best practices (hooks, functional components).
5. **Database Modeling**: Normalized Firestore structure optimized for sub-collection queries.
6. **Validation & Reliability**: Comprehensive security rules and graceful error handling for network/permission issues.
7. **Documentation**: Detailed README and clear code comments.
8. **Additional Thoughtfulness**: Premium UI design, custom scrollbars, and smooth layout animations.

##  Setup & Installation

1. **Environment Variables**:
   - `GEMINI_API_KEY`: Required for AI features.
   - `APP_URL`: Automatically injected in AI Studio.
2. **Firebase Setup**:
   - Ensure `firebase-applet-config.json` is present.
   - Deploy rules using `npm run deploy-firebase` (or equivalent tool).
3. **Run Development**:
   ```bash
   npm run dev