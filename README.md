# Secure Password Manager — Web

Next.js and TypeScript client for the Secure Password Manager: sign-up and login, a protected dashboard, and step-up verification (emailed one-time code or face check) before saved passwords are revealed.

**Backend API:** [secure-password-manager-api](https://github.com/bbramadhikari/secure-password-manager-api)

## Overview

The web client talks to a Django REST Framework API over JWT. After logging in, users can register a face image from their webcam, save credentials, and view their vault — but only after passing a second check: a one-time code sent to their email, or a live face capture that the API verifies.

## Features

- Sign-up and login pages, with tokens kept client-side and refreshed through the API
- Auth state shared across pages with a React context (`AuthContext`)
- Dashboard showing the user's profile and registered face image, with webcam capture to upload one
- Add-password form for new vault entries
- Password view gated behind OTP or face verification
- Webcam capture (`useFaceId` hook) and in-browser face detection with `face-api.js`
- Toast notifications for success and error states

## Tech stack

| Layer | Choice |
|---|---|
| Framework | Next.js (App Router), React |
| Language | TypeScript |
| UI | Material UI, Tailwind CSS, React Icons |
| Face detection | face-api.js |
| Feedback | react-hot-toast |

## Project structure

```
src/
├── app/
│   ├── auth/            # login and signup pages
│   ├── dashboard/       # profile, face registration
│   ├── password/
│   │   ├── add/         # create a vault entry
│   │   └── show/        # OTP / face verification, then the vault
│   └── hooks/
│       └── useFaceId.tsx  # webcam access + face detection
└── context/
    └── AuthContext.tsx  # shared auth state
```

## Getting started

**Prerequisites:** Node.js 18+, and the [API](https://github.com/bbramadhikari/secure-password-manager-api) running on `http://127.0.0.1:8000`

```bash
git clone https://github.com/bbramadhikari/secure-password-manager-web.git
cd secure-password-manager-web
npm install
npm run dev        # http://localhost:3000
```

The API address is currently set in the page components as `http://127.0.0.1:8000`.

## Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start the development server |
| `npm run build` | Production build |
| `npm run start` | Serve the production build |
| `npm run lint` | Run ESLint |

## Roadmap

- Move the API base URL into an environment variable (`NEXT_PUBLIC_API_URL`)
- Store tokens in HTTP-only cookies instead of browser storage
- Edit and delete vault entries
- Component and end-to-end tests
- Screenshots and a short demo in this README
