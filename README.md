# MindMeal

MindMeal is a meal-planning web app with a static frontend, a FastAPI backend, and JSON-backed data files.

## Current Structure

```text
Mind-Meal/
  frontend/
    index.html
    script.js
    style.css
    assets/images/
  backend/
    main.py
    requirements.txt
    .env.example
  database/
    recipes.json
    pantry.json
```

## What Was Cleaned Up

- Removed the redundant root `index.html` redirect.
- Ignored local virtual environments and Python bytecode.
- Ignored local backend logs and environment files.

## Run Locally

```bash
pip install -r backend/requirements.txt
uvicorn backend.main:app --reload
```

If you want to run from inside `backend/`:

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

Open `frontend/index.html` directly for the UI.

## Deployment Note

This repo is not yet Cloudflare-ready as-is because the backend still uses local JSON files. For Cloudflare Workers + Neon, the backend needs a database migration first.
