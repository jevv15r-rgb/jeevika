# FitBuddy – AI Fitness Plan Generator

FitBuddy is a FastAPI + Jinja2 + SQLite web application that uses Google's Gemini API to generate a structured 7-day activity plan, a nutrition/recovery tip, and a revised plan from user feedback.

## Project structure

```text
FitBuddy/
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── config.py
│   ├── database.py
│   ├── schemas.py
│   ├── gemini_client.py
│   ├── gemini_generator.py
│   ├── gemini_flash_generator.py
│   ├── updated_plan.py
│   ├── routes.py
│   ├── templates/
│   │   ├── index.html
│   │   ├── result.html
│   │   ├── admin_login.html
│   │   └── all_users.html
│   └── static/
│       └── css/
│           └── style.css
├── tests/
│   └── test_app.py
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

## 1. Open in VS Code

Extract/open the `FitBuddy` folder in VS Code.

Install Python 3.11+ and select the Python interpreter in VS Code.

## 2. Create and activate a virtual environment

### Windows PowerShell

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, use Command Prompt:

```bat
venv\Scripts\activate
```

### macOS/Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

## 3. Install packages

```bash
pip install -r requirements.txt
```

## 4. Configure Gemini

Copy `.env.example` to `.env`.

Put your Gemini API key into:

```env
GEMINI_API_KEY=your_real_key
```

For a no-key UI test, temporarily use:

```env
DEMO_MODE=true
```

Do not commit `.env` to Git.

## 5. Run the application

From the project root:

```bash
uvicorn app.main:app --reload
```

Open:

- http://127.0.0.1:8000
- http://127.0.0.1:8000/docs
- http://127.0.0.1:8000/view-all-users

## 6. Test the main flow

1. Open the home page.
2. Enter a unique User ID.
3. Enter the requested profile information.
4. Select a goal and intensity.
5. Click Generate My Plan.
6. Review the 7-day plan and nutrition/recovery tip.
7. Enter feedback.
8. Click Update Plan with AI.
9. Open Admin and enter the `ADMIN_KEY`.
10. Confirm the original and updated plans are stored.

## 7. Run tests

With the virtual environment active:

```bash
pytest -q
```

## API endpoints

- `GET /` – web home page
- `POST /generate-workout` – generate and save a plan
- `POST /submit-feedback` – update an existing plan
- `GET /view-all-users` – protected admin dashboard
- `POST /delete-user` – protected user deletion
- `GET /docs` – FastAPI Swagger UI

## Notes

The original project document referenced Gemini 1.5 Pro and Gemini Flash. The implementation uses the current Google GenAI Python SDK and configurable current model names instead of hard-coding an older model identifier. If a model is unavailable for your API account, change `GEMINI_WORKOUT_MODEL` and `GEMINI_TIP_MODEL` in `.env`.

The app intentionally treats AI output as general educational wellness guidance. It should not be used as a medical diagnosis or as a substitute for professional advice.

For production deployment, add proper authentication/authorization, HTTPS, CSRF protection, rate limiting, audit logging, stronger secret management, database migrations, and secure admin sessions.
