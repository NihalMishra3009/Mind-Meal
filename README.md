# MindMeal

MindMeal is a meal-planning web app with a clean split between frontend, backend, and data storage.

## Project Structure

- `frontend/` - static UI files
- `backend/` - FastAPI server
- `database/` - JSON storage used by the backend
- `frontend/assets/images/` - app images and icons

## Key Files

- `frontend/index.html`
- `frontend/style.css`
- `frontend/script.js`
- `backend/main.py`
- `backend/requirements.txt`
- `database/recipes.json`
- `database/pantry.json`

## Run the Backend

```bash
pip install -r backend/requirements.txt
uvicorn backend.main:app --reload
```

Or, if you prefer to work from inside the backend folder:

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

## Open the Frontend

Open `index.html` at the repo root, which redirects to `frontend/index.html`.

If you prefer, you can also open `frontend/index.html` directly.

## Notes

- The backend now reads recipe and pantry data from `database/`.
- Frontend asset paths now point to `frontend/assets/images/`.
