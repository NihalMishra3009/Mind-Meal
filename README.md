# MindMeal

MindMeal is a meal-planning web app with a static frontend, a FastAPI backend, and JSON-backed data files.

## Project Overview

MindMeal helps users turn a few pantry ingredients into practical meal ideas. The app accepts ingredients, finds matching recipes, shows what is missing, suggests healthy swaps, and can generate recipe images through an external AI image API.

The project is intentionally lightweight:
- The frontend is plain HTML, CSS, and JavaScript.
- The backend is FastAPI.
- Recipe data is stored in local JSON files.
- Pantry items are persisted in a JSON file on the backend side.

This makes the codebase easy to understand in a recruiter review because the moving parts are separated clearly and the request flow is simple.

## Features

- Ingredient-based recipe suggestions
- Vegetarian and non-vegetarian recipe filters
- Healthy swap lookup
- Pantry list saving and downloading
- Recipe detail modal with steps and nutrition
- AI-generated or fallback recipe imagery
- Responsive UI with dark mode support

## Tech Stack

- Frontend: HTML, CSS, Vanilla JavaScript
- Backend: FastAPI, Uvicorn
- Data: JSON files
- AI image generation: FAL API
- Deployment: Cloudflare Pages for frontend, Railway for backend

## Architecture

The application follows a simple two-part architecture:

1. Frontend
   - Lives in [`frontend/`](c:/Repo/Mind-Meal/frontend/index.html)
   - Renders the interface and handles all user interactions
   - Sends HTTP requests to the backend using `fetch`

2. Backend
   - Lives in [`Backend/main.py`](c:/Repo/Mind-Meal/Backend/main.py)
   - Exposes API endpoints for suggestions, recipe filtering, image generation, pantry storage, and downloads
   - Reads recipe data from [`database/recipes.json`](c:/Repo/Mind-Meal/database/recipes.json)
   - Writes pantry data to [`database/pantry.json`](c:/Repo/Mind-Meal/database/pantry.json)

### Request Flow

- User enters ingredients in the frontend
- Frontend calls `GET /suggest_meal`
- Backend normalizes the ingredients and returns matching recipes
- Frontend renders recipe cards
- When the user opens a recipe, frontend calls `GET /generate_image`
- Backend returns a generated image URL or a fallback image

The veg and non-veg filters work in the same pattern:
- Frontend calls `GET /recipes?type=veg` or `GET /recipes?type=non-veg`
- Backend returns recipe objects in the format the UI expects

## Installation

### Local Setup

Backend:

```bash
pip install -r Backend/requirements.txt
```

Run the API from the repository root:

```bash
uvicorn Backend.main:app --reload
```

Frontend:

- Open [`frontend/index.html`](c:/Repo/Mind-Meal/frontend/index.html) directly in a browser for local testing.
- For a better local dev experience, you can serve the frontend with any static server.

### Environment Variables

For image generation, set:

```env
FAL_KEY=your_full_fal_secret_here
```

The backend also supports `FAL_API_KEY` as a fallback name.

## Deployment

### Frontend

The frontend is designed for Cloudflare Pages as a static site.

Deployment notes:
- Publish the `frontend/` folder
- The frontend points to the Railway backend through the `BASE_URL` constant in [`frontend/script.js`](c:/Repo/Mind-Meal/frontend/script.js)

### Backend

The backend is deployed on Railway.

Recommended Railway settings:
- Root directory: repository root
- Start command:

```bash
uvicorn Backend.main:app --host 0.0.0.0 --port $PORT
```

Required backend environment variables:
- `FAL_KEY`

### CORS

The backend allows local development origins and Cloudflare Pages preview domains. The CORS configuration lives in [`Backend/main.py`](c:/Repo/Mind-Meal/Backend/main.py).

## Screenshots

<a href="https://your-live-website-link-here" target="_blank" rel="noopener noreferrer">
  <img src="docs/screenshots/homepage.png" alt="MindMeal homepage screenshot" />
</a>

## Future Improvements

- Move pantry persistence from JSON to PostgreSQL
- Store recipes in a structured database table
- Replace fallback image generation with curated recipe images
- Add search history and saved meal plans
- Add authentication for personal pantry and favorites
- Split the frontend into a Vite app if the UI grows further
