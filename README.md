# React Frontend

Vite + React frontend for Patient Management.

## Features

- Login (`POST /auth/login`)
- Add User (ADMIN only, `POST /auth/admin/users`)
- Add Patient (`POST /patients`)
- Get Patients (`GET /patients`)
- Update Patient (`PUT /patients/{id}`)
- Delete Patient (`DELETE /patients/{id}`)

## Run

```powershell
npm install
npm run dev
```

Open `http://localhost:5173`.

## Config

Optional env var:

- `VITE_API_BASE` (default: same-origin, for example `/auth` and `/patients`)
- `VITE_DEV_API_TARGET` (dev-server proxy target, default: `http://localhost:4004`)

## Jenkins CI

This repository includes a dedicated `Jenkinsfile` for frontend CI.

### Jenkins Agent Requirements

- Docker Engine installed and running
- Permission for Jenkins agent user to run Docker commands

### Pipeline Stages

1. Checkout repository from SCM
2. Validate Docker availability
3. Build frontend image with `docker build`
